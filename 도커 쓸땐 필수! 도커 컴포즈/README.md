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
```
docker run -it nginx
```

2. 예시 2) nginx 컨테이너 실행 + 호스트의 8080 포트 연결
```docker
docker run -it -p 8080:80 nginx
```

3. 예시 3) nginx 컨테이너 실행 + 호스트의 8080 포트 연결 + 컨테이너 종료시 자동 삭제
```docker
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

```docker
docker run -it -p 8080:80 --rm -v $(pwd):/usr/share/nginx/html/ nginx
```

### 2. 컨테이너끼리 연결하기 편해서
- 준비) django-sample 이미지를 빌드합니다
```docker
git clone https://github.com/raccoonyy/django-sample-for-docker-compose.git django-sample

cd django-sample

docker build -t django-sample .
```

1. 예시 1) django 컨테이너 실행 + postgres 컨테이너 실행
```docker
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
```docker
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
</details>
</br>