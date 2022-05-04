# 1. 도커컴포즈란?

<details markdown="1">
<summary>1. 설치</summary>

## 설치

### docker 설치
```
curl -fsSL https://get.docker.com/ | sudo sh

sudo usermod -aG docker $USER
```

### docker-compose 설치
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose
```

</details>
</br>

<details markdown="1">
<summary>2. 도커 컴포즈의 장점</summary>

## 도커 컴포즈의 장점(사용하는 이유)

### 1. docker 실행 명령어를 일일이 입력하기가 복잡해서
1. 예시 1) nginx 컨테이너 실행
```dockerfile
docker run -it nginx
```

2. 예시 2) nginx 컨테이너 실행 + 호스트의 8080 포트 연결
```dockerfile
docker run -it -p 8080:80 nginx
```

3. 예시 3) nginx 컨테이너 실행 + 호스트의 8080 포트 연결 + 컨테이너 종료시 자동 삭제
```dockerfile
docker run -it -p 8080:80 --rm nginx
```

4. 예시 4) nginx 컨테이너 실행 + 호스트의 8080 포트 연결 + 컨테이너 종료시 자동 삭제 + 호스트의 디렉터리를 컨테이너 안에 링크
```html
# ~/project/nginx/index.html
<html>
<body>
<h1>Hello Docker-Compose</h1>
</body>
</html>
```

```dockerfile
docker run -it -p 8080:80 --rm -v $(pwd):/usr/share/nginx/html/ nginx
```

### 2. 컨테이너끼리 연결하기 편해서
- 준비) django-sample 이미지를 빌드합니다
```dockerfile
git clone https://github.com/raccoonyy/django-sample-for-docker-compose.git django-sample

cd django-sample

docker build -t django-sample .
```

1. 예시 1) django 컨테이너 실행 + postgres 컨테이너 실행
```dockerfile
docker run --rm -d --name django \
  -p 8000:8000 \
  django-sample
​
docker run --rm -d --name postgres \
  -e POSTGRES_DB=djangosample \
  -e POSTGRES_USER=sampleuser \
  -e POSTGRES_PASSWORD=samplesecret \
  postgres
```

2. 예시 2) postgres 컨테이너 실행 + django 컨테이너 실행 + 서로 연결하기
```dockerfile
docker run --rm -d --name postgres \
  -e POSTGRES_DB=djangosample \
  -e POSTGRES_USER=sampleuser \
  -e POSTGRES_PASSWORD=samplesecret \
  postgres
​
docker run -d --rm \
  -p 8000:8000 \
  -e DJANGO_DB_HOST=db \
  --link postgres:db \
  django-sample
```

### 3. 특정 컨테이너끼리만 통신할 수 있는 가상 네트워크 환경을 편리하게 관리하고 싶어서
1. 예시 1) postgres 컨테이너 실행 + django1 컨테이너 연결
```dockerfile
docker run --rm -d --name postgres \
  -e POSTGRES_DB=djangosample \
  -e POSTGRES_USER=sampleuser \
  -e POSTGRES_PASSWORD=samplesecret \
  postgres
​
docker run -d --rm --name django1 \
  -p 8000:8000 \
  -e DJANGO_DB_HOST=db \
  --link postgres:db \
  django-sample
```

2. 예시 2) postgres 컨테이너는 호스트의 다른 컨테이너들이 모두 접근할 수 있음
```dockerfile
docker run -d --rm --name django2 \
  -p 8001:8000 \
  -e DJANGO_DB_HOST=db \
  --link postgres:db \
  django-sample
```

3. 예시 3) postgres 컨테이너 + django1 컨테이너만 통신할 수 있는 가상 네트워크 만들기
```dockerfile
# 도커 네트워크 살펴보기
docker network ls
```

```dockerfile
# 도커 네트워크 생성하기
docker network create --driver bridge web-service
​
docker network ls
```

```dockerfile
# 컨테이너 실행하기
docker run --rm -d --name postgres \
  --network web-service \
  -e POSTGRES_DB=djangosample \
  -e POSTGRES_USER=sampleuser \
  -e POSTGRES_PASSWORD=samplesecret \
  postgres
​
docker run -d --rm --name django1 \
  --network web-service \
  -p 8000:8000 \
  -e DJANGO_DB_HOST=db \
  --link postgres:db \
  django-sample
​
docker run -d --rm --name django2 \
  -p 8001:8000 \
  -e DJANGO_DB_HOST=db \
  --link postgres:db \
  django-sample
```
- docker의 네트워크 모드 종류
  - bridge: 해당 네트워크 안에서만 통신 가능
  - host: 호스트와 똑같은 네트워크 환경
  - none: 아무 네트워크도 사용하지 않음

### 4. 이 모든 것을 간단한 명령어로 관리하고 싶어서
```dockerfile
# 실행 명령어와 종료 명령어
docker network create --driver bridge web-service
​
docker run --rm -d --name postgres \
  --network web-service \
  -p 5432:5432 \
  -e POSTGRES_DB=djangosample \
  -e POSTGRES_USER=sampleuser \
  -e POSTGRES_PASSWORD=samplesecret \
  postgres
​
docker run -d --rm --name django1 \
  --network web-service \
  -p 8000:8000 \
  -e DJANGO_DB_HOST=db \
  --link postgres:db \
  django-sample
​
docker kill django1 postgres
​
docker network rm web-service

```

- docker-compose.yml
```dockerfile
version: '3'
​
volumes:
  postgres_data: {}
​
services:
  db:
    image: postgres
    volumes:
      - postgres_data:/var/lib/postgres/data
    environment:
      - POSTGRES_DB=djangosample
      - POSTGRES_USER=sampleuser
      - POSTGRES_PASSWORD=samplesecret
​
  django:
    build:
      context: .
      dockerfile: ./compose/django/Dockerfile-dev
    volumes:
      - ./:/app/
    command: ["./manage.py", "runserver", "0:8000"]
    environment:
     - DJANGO_DB_HOST=db
    depends_on:
      - db
    restart: always
    ports:
      - 8000:8000
```

-  도커 컴포즈로 실행하고 종료하는 방법
```dockerfile
docker-compose up -d
​
docker-compose down
```
</details>
</br>

<details markdown="1">
<summary> 실습 - NGINX 서버를 도커 컴포즈로 실행하기 </summary>

## 실습 - NGINX 서버를 도커 컴포즈로 실행하기
- Ghost시스템 앞단에 NGINX 웹서버 달기
  - 처리 성능을 높이거나 여타 다른기능을 사용할 수 있다.
### 도커로 NGINX 컨테이너 실행하기
#### docker로 ghost 이미지 실행하기
- dockerfile
```dockerfile
docker run -it --name blog --rm -p 2368:2368 ghost
```
- 컨테이너 종료
```dockerfile
docker run --rm -p 2368:2368 --name blog ghost
```
- ghost란 간단한 블로깅 시스템

- 블로그 데이터는 영속적이어야하므로, 데이터가 로컬 디렉토리에 저장되게 해보기
```
# 디렉토리 만들기
mkdir content
```

```dockerfile
docker run --rm -p 2368:2368 --name blog -v $(pwd)/content:/var/lib/ghost/content ghost
```

#### docker-compose로 변환하기
```dockerfile
version: '3'

volumes: 
  ghost_data: {}

services:
  ghost:
    image: ghost
    ports:
      - "2368:2368"
    volumes:
      - ghost_data:/var/lib/ghost/content
```

### Ghost 시스템과 NGINX 연결하기
```docker
# docker-compose.yml
version: '3'

volumes: 
  ghost_data: {}

services:
  ghost:
    image: ghost
    volumes:
      - ghost_data:/var/lib/ghost/content
    environment:
      - 0
  nginx:
    image: nginx
    volumes: 
      - ./nginx.conf:/etc/nginx/nginx.conf
    ports:
      - 8000:80
```

- nginx.conf 파일 생성
```docker
# nginx.conf
events {
  worker_connections 1024;
}

http {
  upstream ghost {
    server ghost:2368;
  }
  
  server {
    listen 80;
    server_name _;

    location / {
      proxy_pass http://ghost;
    }
  }
}
```
</details>
</br>