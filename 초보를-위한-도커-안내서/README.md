# 1. 도커란 무엇인가

<details markdown="1">
<summary>1. 서버를 관리한다는 것</summary>

## 1. 서버를 관리한다는것

### 개요
- 도커는 컨테이너 기반의 오픈소스 가상화 플랫폼
- 다른 도구와 마찬가지로 어떤 문제를 해결하기 위해 만들어졌고
그 방법이 많은 사람들에게 인기를 끌면서 널리 사용

</details>
</br>

<details markdown="1">
<summary>2. 도커 컨테이너 생성 데모</summary>

</details>
</br>

<details markdown="1">
<summary>3. 서버관리 방식의 변화</summary>

## 1. 서버관리 방식의 변화

- 가상머신처럼 독립적으로 실행되지만
- 가상머신보다 빠르고
- 가상머신보다 쉽고
- 가상머신보다 효율적입니다

</details>
</br>

<details markdown="1">
<summary>4. 도커의 등장</summary>

## 1. 도커의 등장

- 2013년에 DotCloud(현 Docker)에서 첫 공개
- 컨테이너: 격리된 환경에서 작동하는 프로세스
- 리눅스 커널의 여러 기술을 활용
- 하드웨어 가상화 기술보다 가벼움
- 이미지 단위로 프로세스 실행 환경을 구성

</details>
</br>

<details markdown="1">
<summary>5. 도커란?</summary>

## 5. 도커란?

### 도커의 특징 - 확장성/이식성
- 도커가 설치되어 있다면 어디서든 컨테이너를 실행할 수 있음
- 특정 회사나 서비스에 종속적이지 않음
- 쉽게 개발서버를 만들 수 있고 테스트서버 생성도 간편함

</br>

### 도커의 특징 - 표준성
- 도커를 사용하지 않는 경우 ruby, nodejs, go, php로 만든 서비스들의 배포 방식은
제각각 다름
- 컨테이너라는 표준으로 서버를 배포하므로 모든 서비스들의 배포과정이 동일해짐

</br>

### 도커의 특징 - 이미지
- 이미지에서 컨테이너를 생성하기 때문에 반드시 이미지를 만드는 과정이 필요
- Dockerfile을 이용하여 이미지를 만들고 처음부터 재현 가능
- 빌드 서버에서 이미지를 만들면 해당 이미지를 이미지 저장소에 저장하고 운영서버
에서 이미지를 불러옴

</br>

### 도커의 특징 - 설정관리
- 설정은 보통 환경변수로 제어함
- MYSQL_PASS=password와 같이 컨테이너를 띄울때 환경변수를 같이 지정
- 하나의 이미지가 환경변수에 따라 동적으로 설정파일을 생성하도록 만들어져야함

</br>

### 도커의 특징 - 자원관리
 컨테이너는 삭제 후 새로 만들면 모든 데이터가 초기화됨
- 업로드 파일을 외부 스토리지와 링크하여 사용하거나 S3같은 별도의 저장소가 필요
- 세션이나 캐시를 memcached나 redis와 같은 외부로 분리

</br>

### 도커가 가져온 변화
- 클라우드 이미지보다 관리하기 쉬움
- 다른 프로세스와 격리되어 가상머신처럼 사용하지만 성능저하 (거의) 없음
- 복잡한 기술(namespace, cgroups, network, ...)을 몰라도 사용할 수 있음
- 이미지 빌드 기록이 남음(깃을통해)
- 코드와 설정으로 관리 > 재현 및 수정 가능
- 오픈소스 > 특정 회사 기술에 종속적이지 않음
</details>
</br>

<details markdown="1">
<summary>6. 도커의 미래(컨테이너의 미래)</summary>

## 6. 도커의 미래(컨테이너의 미래)
- 여러대의 서버와 여러개의 서비스를 관리하기 쉽게
### 스케줄링
- 컨테이너를 적당한 서버에 배포해 주는 작업
- 여러 대의 서버 중 가장 할일 없는 서버에 배포하거나 그냥 차례대로 배포 또는 아예
랜덤하게 배포
- 컨테이너 개수를 여러 개로 늘리면 적당히 나눠서 배포하고 서버가 죽으면 실행 중
이던 컨테이너를 다른 서버에 띄워줌

</br>

### 클러스터링
- 여러 개의 서버를 하나의 서버처럼 사용
- 작게는 몇 개 안 되는 서버부터 많게는 수천 대의 서버를 하나의 클러스터로
- 여기저기 흩어져 있는 컨테이너도 가상 네트워크를 이용하여 마치 같은 서버에 있
는 것처럼 쉽게 통신

</br>

### 서비스 디스커버리
- 서비스를 찾아주는 기능
- 클러스터 환경에서 컨테이너는 어느 서버에 생성될지 알 수 없고 다른 서버로 이동
할 수도 있음
- 따라서 컨테이너와 통신을 하기 위해서 어느 서버에서 실행중인지 알아야 하고 컨테
이너가 생성되고 중지될 때 어딘가에 IP와 Port같은 정보를 업데이트해줘야 함
- 키-벨류 스토리지에 정보를 저장할 수도 있고 내부 DNS 서버를 이용

</details>
</br>

# 2. 도커 설치부터 실행
<details markdown="1">
<summary>1. 도커 설치하기</summary>

## 1. 도커 설치하기
### MacOS or Windows
- 도커는 기본적으로 linux를 지원하기 때문에 MacOS와 Windows에 설치되는
Docker는 가상머신에 설치됨
- MacOS는 xhyve를 사용하고 Windows는 Hyper-V 사용
- Windows Pro에서만 설치가 가능했으나 Windows WSL 2를 이용하여 Home
버전도 설치 가능
- 그 외에 Windows 사용자는 VirtualBox에 ubuntu 리눅스를 설치하여 실습

</details>
</br>

<details markdown="1">
<summary>2. 도커 기본 명령어(run)</summary>

## 2. 도커 기본 명령어(run)
### run -컨테이너 실행

```
docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]
```

|명령어|내용|
|------|---|
|-d|detached mode (백그라운드 모드)|
|-p|호스트와 컨테이너의 포트를 연결|
|-v|호스트와 컨테이너의 디렉토리를 연결|
|-e|컨테이너 내에서 사용할 환경변수 설정|
|--name|컨테이너 이름 설정|
|--rm|프로세스 종료시 컨테이너 자동 제거|
|-it|-i와 -t를 동시에 사용한 것으로 터미널 입력을 위한 옵션|
|--network|네트워크 연결|

</br>

### ubuntu 20.04 컨테이너 만들기
```
docker run ubuntu:20.04
```
- run 명령어를 사용하면 사용할 이미지가 저장되어 있는지 확인하고 없다면 다운로드
(pull) 한 후 컨테이너를 생성(create)하고 시작(start)합니다.
- 컨테이너는 정상적으로 실행됐지만 뭘 하라고 명령어를 전달하지 않았기 때문에 컨테
이너는 생성되자마자 종료됩니다. 
- 컨테이너는 프로세스이기 때문에 실행중인 프로세
스가 없으면 컨테이너는 종료됩니다.
- 조금 더 자세하게 설명하면 도커 이미지마다 컨테이너가 만들어질때 실행할 명령어를
지정할 수 있고 ubuntu:20.04는 "/bin/bash"가 지정되어 쉘이 실행되야 하지만, 입
력을 받을 수 있도록 "-it"옵션을 입력하지 않았기 때문에 바로 실행이 종료되었습니
다.

</br>

### /bin/sh 실행하기
```
docker run --rm -it ubuntu:20.04 /bin/sh
```

- 컨테이너 내부에 들어가기 위해 sh를 실행하고 키보드 입력을 위해 -it 옵션을 줍니다.
- 추가적으로 프로세스가 종료되면 컨테이너가 자동으로 삭제되도록 --rm 옵션도 추가
합니다.
- --rm 옵션이 없다면 컨테이너가 종료되더라도 삭제되지 않고 남아 있어 수동으로 삭제
해야 합니다.

</br>

### CentOS 실행하기
```
docker run --rm -it centos:8 /bin/sh
```

- 도커는 다양한 리눅스 배포판을 실행할 수 있습니다. 
- 공통점은 모두 동일한 커널을 사용한다는 점입니다.
- Ubuntu 또는 CentOS에 포함된 다양한 기본기능이 필요 없는 경우, Alpine 이라는 초
소형 (5MB) 이미지를 사용할 수도 있습니다.

</br>

### 웹 어플리케이션 실행하기
```
docker run --rm -p 5678:5678 hashicorp/http-echo -text="hello world"
```
- detached mode(백그라운드 모드)로 실행하기 위해 -d 옵션을 추가하고 -p 옵션을
추가하여 컨테이너 포트를 호스트의 포트로 연결하였습니다.
- 브라우저를 열고 localhost:5678에 접속하면 메시지를 볼 수 있습니다.

</br>

### Redis 실행하기
```
docker run --rm -p 1234:6379 redis
```
- Redis라는 메모리기반 데이터베이스를 실행합니다.
```
$ telnet localhost 1234 # telnet이 설치되어 있다면..
set hello world
+OK
get hello
$5
world
quit
```

</br>

### MySQL 실행하기
```
docker run -d -p 3306:3306 \
 -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
 --name mysql \
 mysql:5.7
```
- Mysql 실행
```
docker exec -it mysql mysql
create database wp CHARACTER SET utf8;
grant all privileges on wp.* to wp@'%' identified by 'wp';
flush privileges;
quit
```

</br>

### exec 명령어
- exec 명령어는 run 명령어와 달리 실행중인 도커 컨테이너에 접속할 때 사용하며 컨테
이너 안에 ssh server등을 설치하지 않고 exec 명령어로 접속합니다.

</br>

### 워드프레스 블로그 실행하기
```
docker run -d -p 8080:80 \
 -e WORDPRESS_DB_HOST=host.docker.internal \
 -e WORDPRESS_DB_NAME=wp \
 -e WORDPRESS_DB_USER=wp \
 -e WORDPRESS_DB_PASSWORD=wp \
 wordpress
```
- 앞에서 만든 MySQL을 실행한 상태에서 생성합니다.
- 웹브라우저 localhost:8080으로 접속합니다.
</details>
</br>

<details markdown="1">
<summary>3. 도커 기본 명령어(ps, stop, rm, logs, images,...)</summary>

## 3. 도커 기본 명령어(ps, stop, rm, logs, images,...)
### ps 명령어
```
docker ps
```
- 실행중인 컨테이너 목록을 확인하는 명령어 입니다.
```
docker ps -a
```
- 중지된 컨테이너도 확인하려면 -a 옵션을 붙입니다

</br>

### stop 명령어
```
docker stop [OPTIONS] CONTAINER [CONTAINER...]
```
- 실행중인 컨테이너를 중지하는 명령어 입니다.
- 실행중인 컨테이너를 하나 또는 여러개 (띄어쓰기) 중지할 수 있습니다.

</br>

### rm 명령어
```
docker rm [OPTIONS] CONTAINER [CONTAINER...]
```
- 종료된 컨테이너를 완전히 제거하는 명령어 입니다.
- mysql, wordpress를 제외한 컨테이너를 제거하세요.

</br>

### logs 명령어
```
docker logs [OPTIONS] CONTAINER
```
- 컨테이너가 정상적으로 동작하는지 확인하는 좋은 방법은 로그를 확인하는 것 입니다.
- 기본 옵션과 -f, --tail 옵션을 살펴보니다.

</br>

### images 명령어
```
docker images [OPTIONS] [REPOSITORY[:TAG]]
```
- 도커가 다운로드한 이미지 목록을 보는 명령어입니다.

</br>

### pull 명령어
```
docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```
- 이미지를 삭제하는 방법 입니다.
```
docker pull ubuntu:18.04
```

</br>

### rmi 명령어
```
docker rmi [OPTIONS] IMAGE [IMAGE...]
```
- 이미지를 삭제하는 방법입니다.
- images 명령어를 통해 얻는 이미지 목록에서 이미지 ID를 입력하면 삭제가 됩니다. 단,
컨테이너가 실행중인 이미지는 삭제되지 않습니다.

</br>

### network create 명령어
```
docker network create [OPTIONS] NETWORK
```
- 도커 컨테이너끼리 이름으로 통신할 수 있는 가상 네트워크를 만듭니다.
```
docker network create app-network
```
- app-network 라는 이름으로 wordpress와 mysql이 통신할 네트워크를 만듭니다.

</br>

### network connect 명령어
```
docker network connect [OPTIONS] NETWORK CONTAINER
```
- 기존에 생성된 컨테이너에 네트워크를 추가합니다.
```
docker network connect app-network mysql
```
- mysql 컨테이너에 네트워크를 추가합니다.

</br>

### network option 명령어
```
docker run -d -p 8080:80 \
 --network=app-network \
 -e WORDPRESS_DB_HOST=mysql \
 -e WORDPRESS_DB_NAME=wp \
 -e WORDPRESS_DB_USER=wp \
 -e WORDPRESS_DB_PASSWORD=wp \
 wordpress
```

- 워드프레스를 app-network에 속하게 하고 mysql을 이름으로 접근합니다.
</details>
</br>

<details markdown="1">
<summary>4. 도커 기본 명령어(volume)</summary>

## 4. 도커 기본 명령어(volume)
### volume mount (-v) 명령어
```
docker stop mysql
docker rm mysql
docker run -d -p 3306:3306 \
 -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
 --network=app-network \
 --name mysql \
 -v /Users/subicura/Workspace/github.com/subicura/docker-guide/ch02/mysql:/var/lib/mysql \
 mysql:5.7
```
- mysql을 삭제후에 다시 실행하면 데이터베이스 오류가 발생합니다.

```
-v /my/own/datadir:/var/lib/mysql
```

</details>
</br>

<details markdown="1">
<summary>5. 도커 컴포즈 (docker compose)</summary>

## 5. 도커 컴포즈 (docker compose)
### 설치 확인
```
$ docker-compose version
docker-compose version 1.26.2, build eefe0d31
docker-py version: 4.2.2
CPython version: 3.7.7
OpenSSL version: OpenSSL 1.1.1g 21 Apr 2020
```
- Linux는 다음 명령어로 설치합니다.
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/
docker-compose-$(uname -s)
sudo chmod +x /usr/local/bin/docker-compose
```

</br>

### docker-compose.yml
```
version: '2'
services:
  db:
    image: mysql:5.7
    volumes:
      - ./mysql:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: wordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
  wordpress:
    image: wordpress:latest
    volumes:
      - ./wp:/var/www/html
    ports:
      - "8000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_PASSWORD: wordpress
```

</br>

### up 명령어
```
docker-compose up -d
```
- docker compose를 이용하여 mysql과 wordpress를 실행합니다.

</br>

### down 명령어
```
docker-compose down
```
- docker compose를 이용하여 mysql과 wordpress를 종료합니다
</details>
</br>

<details markdown="1">
<summary>6. 도커 컴포즈 문법</summary>

## 6. 도커 컴포즈 문법
### version
```
version: '3'
```
- docker-compose.yml 파일의 명세 버전
- docker-compose.yml 버전에 따라 지원하는 도커 엔진 버전도 다름

</br>

### services
```
services:
 postgres:
 ...
 django:
 ...
```
- 실행할 컨테이너 정의
- docker run --name django과 같다고 생각할 수 있음

</br>

### image
```
services:
 django:
 image: django-sample
```
- 컨테이너에 사용할 이미지 이름과 태그
- 태그를 생략하면 latest
- 이미지가 없으면 자동으로 pull

</br>

### ports
```
services:
 django:
 ...
 ports:
 - "8000:8000"
```
- 컨테이너와 연결할 포트(들)
- {호스트 포트}:{컨테이너 포트}

</br>

### environment
```
services:
 mysql:
 ...
 environment:
 - MYSQL_ROOT_PASSWORD=somewordpress: '3'
```
- 컨테이너에서 사용할 환경변수(들)
- {환경변수 이름}:{값}

</br>

### volumes
```
services:
 django:
 ...
 volumes:
 - ./app:/app
```
- 마운트하려는 디렉터리(들)
- {호스트 디렉터리}:{컨테이너 디렉터리}

</br>

### restart
```
services:
 django:
 restart: always
```
- 재시작 정책
- restart: "no"
- restart: always
- restart: on-failure
- restart: unless-stopped

</br>

### build
```
django:
 build:
 context: .
 dockerfile: ./compose/django/Dockerfile-dev
```
- 이미지를 자체 빌드 후 사용
- image 속성 대신 사용함
- 여기에 사용할 별도의 도커 파일이 필요함
</details>
</br>

<details markdown="1">
<summary>7. 도커 컴포즈 명령어</summary>

## 7. 도커 컴포즈 명령어
### up
- docker-compose.yml에 정의된 컨테이너를 실행
  - docker-compose up
  - docker-compose up -d
    - docker run의 -d 옵션과 동일
  - docker-compose up --force-recreate
    - 컨테이너를 새로 만들기
  - docker-compose up --build
    - 도커 이미지를 다시 빌드(build로 선언했을 때만)

</br>

### start
- 멈춘 컨테이너를 재개
  - docker-compose start
  - docker-compose start wordpress
    - wordpress 컨테이너만 재개

</br>

### restart
- 컨테이너를 재시작
  - docker-compose restart
  - docker-compose restart wordpress
    - wordpress 컨테이너만 재시작

</br>

### stop
- 컨테이너 멈춤
  - docker-compose stop
  - docker-compose stop wordpress
    - wordpress 컨테이너만 멈춤

</br>

### down
- 컨테이너를 종료하고 삭제
- docker-compose down

</br>

### logs
- 컨테이너의 로그
  - docker-compose logs
  - docker-compose logs -f
    - 로그 follow

</br>

### ps
- 컨테이너 목록
  - docker-compose ps

</br>

### exec
- 실행 중인 컨테이너에서 명령어 실행
  - docker-compose exec {컨테이너 이름} {명령어}
  - docker-compose exec wordpress bash

</br>

### build
- 컨테이너 build 부분에 정의된 내용대로 빌드
  - build로 선언된 컨테이너만 빌드됨
  - docker-compose build
  - docker-compose build wordpress
    - wordpress 컨테이너만 build
</details>
</br>

<details markdown="1">
<summary>8. nginx 컨테이너 만들기</summary>

## 8. nginx 컨테이너 만들기

**index.html**

```
hello world
```

**run**

```
$ docker run -d --rm \
  -p 50000:80 \
  -v $(pwd)/index.html:/usr/share/nginx/html/index.html \
  nginx
```

</details>
</br>

<details markdown="1">
<summary>9. php cli 컨테이너 실행하기</summary>

## 9. php cli 컨테이너 실행하기
### Cli

**hello.php**

```
<?php phpinfo() ?>
```

**run**

```
$ docker run --rm \
  -v $(pwd)/hello.php:/app/hello.php \
  php:7 \
  php /app/hello.php

```

### docker-compose
```yml
version: '2'

services:
  app:
    image: php:7
    volumes:
      - ./hello.php:/app/hello.php
    command: "php /app/hello.php"
```

</details>
</br>

# 3. 도커 - 이미지 만들고 배포하기

<details markdown="1">
<summary>1. 도커 이미지 만들기 - 기본</summary>

## 1. 도커 이미지 만들기 - 기본

### 이미지란
- 도커는 레이어드 파일 시스템 기반
- AUFS, BTRFS, Overlayfs, ...
- 이미지는 프로세스가 실행되는 파일들의 집합(환경)
- 프로세스는 환경(파일)을 변경할 수 있음
- 이 환경을 저장해서 새로운 이미지를 만든다

### 예시 - Git 설치
```
$ docker run -it --name git ubuntu:latest bash
root@2f8bfff679f9:/# git
bash: git: command not found
root@2f8bfff679f9:/# apt-get update
root@2f8bfff679f9:/# apt-get install -y git
root@2f8bfff679f9:/# git --version
git version 2.17.1
```
- docker build -t subicura/ubuntu:git01.
-      명령어    이름공간/이미지이름/태그/빌드컨텍스트

### TDD 하듯이
- 한번에 성공하는 빌드는 없음
- 파란불(빌드 성공)이 뜰 때까지 많은 빨간불(빌드 실패)를 경험함
- 일단 파란불이 켜져도 리팩토링을 통해 더 최적화된 이미지 생성

### Dockerfile
|FROM|기본이미지|
|------|---|
|RUN|쉘 명령어 실행|
|CMD|컨테이너 기본 실행 명령어 (Entrypoint의 인자로 사용)|
|EXPOSE|오픈되는 포트 정보|
|ENV|환경변수 설정|
|ADD|파일 또는 디렉토리 추가. URL/ZIP 사용가능|
|COPY|파일 또는 디렉토리 추가|
|ENTRYPOINT|컨테이너 기본 실행 명령어|
|VOLUME|외부 마운트 포인트 생성|
|USER|RUN, CMD, ENTRYPOINT를 실행하는 사용자|
|WORKDIR|작업 디렉토리 설정|
|ARGS|빌드타임 환경변수 설정|
|LABEL|key - value 데이터|
|ONBUILD|다른 빌드의 베이스로 사용될때 사용하는 명령어|

### 이미지 빌드하기
```
docker build -t {이미지명:이미지태그} {빌드 컨텍스트}
$ docker build -t sample:1 .
```
- 현재 디렉토리의 Dockerfile로 빌드
  -f <Dockerfile 위치> 옵션을 사용해 다른 위치의 Dockerfile 파일 사용 가능
  -t 명령어로 도커 이미지 이름을 지정
  - {네임스페이스}/{이미지이름}:{태그} 형식
- 마지막에는 빌드 컨텍스트 위치를 지정
  - 현재 디렉터리를 의미하는 점(.)을 주로 사용
  - 필요한 경우 다른 디렉터리를 지정할 수도 있음

### .dockerignore
-.gitignore와 비슷한 역할
- 도커 빌드 컨텍스트에서 지정된 패턴의 파일을 무시
- .git이나 민감한 정보를 제외하는 용도로 주로 사용
- .git이나 에셋 디렉터리만 제외시켜도 빌드 속도 개선
이미지 빌드 시에 사용하는 파일은 제외시키면 안 됨

### Git을 설치한 ubuntu 이미지
```
FROM ubuntu:latest
RUN apt-get update
RUN apt-get install -y git
```
- Dockerfile 을 만들고 빌드합니다.
```
$ docker build -t ubuntu:git-dockerfile .
$ docker images | grep ubuntu
```
</details>
</br>

<details markdown="1">
<summary>2. 도커 이미지 만들기 - 웹 애플리케이션 (nodejs)</summary>

## 2. 도커 이미지 만들기 - 웹 애플리케이션 (nodejs)

### Nodejs 웹 애플리케이션
```
$ npm init
$ npm i fastify --save
```
- https://www.fastify.io/docs/latest/Getting-Started/
- 소스 파일 복사 > COPY 명령어
- node_modules 제외 > .dockerignore

- app.js
```js
// Require the framework and instantiate it
const fastify = require('fastify')({
 logger: true
})
// Declare a route
fastify.get('/', function (request, reply) {
 reply.send({ hello: 'world' })
})
// Run the server!
fastify.listen(3000, '0.0.0.0', function (err, address) {
 if (err) {
 fastify.log.error(err)
 process.exit(1)
 }
 fastify.log.info(`server listening on ${address}`)
})

```

</br>

- Dockerfile
```
# 1. node 설치
FROM ubuntu:20.04
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y nodejs npm
# 2. 소스 복사
COPY . /usr/src/app
# 3. Nodejs 패키지 설치
WORKDIR /usr/src/app
RUN npm install
# 4. WEB 서버 실행 (Listen 포트 정의)
EXPOSE 3000
CMD node app.js
```


- .dockerignore
```
node_modules/*
```

- 이미지 빌드하기
```
docker build -t subicura/app .
```

- 컨테이너 실행하기
```
docker run --rm -d -p 3000:3000 subicura/app
```

</br>

- Dockerfile(v2)
```
# 1. node 이미지 사용
FROM node:12
# 2. 소스 복사
COPY . /usr/src/app
# 3. Nodejs 패키지 설치
WORKDIR /usr/src/app
RUN npm install
# 4. WEB 서버 실행 (Listen 포트 정의)
EXPOSE 3000
CMD node app.js
```

</br>

- Dockerfile(v3)
```
# 1. node 이미지 사용
FROM node:12
# 2. 패키지 우선 복사
COPY ./package* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
# 3. 소스 복사
COPY . /usr/src/app
# 4. WEB 서버 실행 (Listen 포트 정의)
EXPOSE 3000
CMD node app.js
```

</br>

- Dockerfile(v4)
```
# 1. node 이미지 사용
FROM node:12-alpine
# 2. 패키지 우선 복사
COPY ./package* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
# 3. 소스 복사
COPY . /usr/src/app
# 4. WEB 서버 실행 (Listen 포트 정의)
EXPOSE 3000
CMD node app.js
```

</br>

### FROM
```
FROM [--platform=<platform>] <image>[:<tag>] [AS <name>]
```
- 베이스 이미지 지정
- FROM ubuntu:latest
- FROM node:12
- FROM python:3

</br>

### COPY
```
COPY [--chown=<user>:<group>] <src>... <dest>
```
- 파일 또는 디렉토리 추가
- COPY index.html /var/www/html/
- COPY ./app /usr/src/app

</br>

### RUN
```
RUN <command>
```
- 명령어 실행
- RUN apt-get update
- RUN npm install

</br>

### WORKDIR
```
WORKDIR /path/to/workdir
```
- 작업 디렉토리 변경
- WORKDIR /app

</br>

### EXPOSE
```
WORKDIR /path/to/workdir
```
- 컨테이너에서 사용하는 포트 정보
- EXPOSE 8000

</br>

### CMD
```
CMD ["executable","param1","param2"]
CMD command param1 param2
```
- 컨테이너 생성시 실행할 명령어
- CMD ["node", "app.js"]
- CMD node app.js

</details>
</br>

<details markdown="1">
<summary>3. 이미지 저장소</summary>

## 3. 이미지 저장소
### 이미지 저장 명령어
- docker login
- docker push {ID}/example
- docker pull {ID}/example


</br>

### docker hub
- hub.docker.com
- 내이미지를 도커허브에 올리고 누구나 받을수 있다. 
  - 깃허브 처름 private이 있으나 무료버전은 하나밖에 사용불가

  </details>

</br>

  <details markdown="1">
<summary>4. 도커 배포 기본</summary>

## 4. 도커 배포 기본
### 배포하기
```
docker run -d -p 3000:3000 subicura/app
```
- 컨테이너 실행 = 이미지 pull + 컨테이너 start
- 도커 허브에 올리는 순간 아무나 사용할수있다. (public 한정)
  </details>

  </br>
  
  <details markdown="1">
<summary>5. Nginx를 이용한 정적 페이지 서버 만들기</summary>

## 5. Nginx를 이용한 정적 페이지 서버 만들기
### 실습한파일
**index.html**

```
<html>
  <head>
    <title>도커 이미지 예제</title>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
  </head>
  <body>
    <h1>Nginx 서버를 도커 이미지로 만들었습니다.</h1>
  </body>
</html>
```

**Dockerfile**

```
FROM nginx
COPY index.html /usr/share/nginx/html/index.html
```

**run**

```
$ docker build -t lab02/exam1 .
$ docker run -d --rm \
  -p 50000:80 \
  lab02/exam1
```
</details>
</br>

<details markdown="1">
<summary>6. Hellonode 실습</summary>

## 6. Hellonode 실습
### 실습한파일
**server.js**

```js
const http = require('http');
const os = require('os');

const port = process.env.PORT || 8080;

process.on('SIGINT', function() {
  console.log('shutting down...');
  process.exit(1);
});

var handleRequest = function(request, response) {
  console.log(`Received request for URL: ${request.url}`);
  response.writeHead(200);
  response.end(`Hello, World!\nHostname: ${os.hostname()}\n`);
};

var www = http.createServer(handleRequest);
www.listen(port, () => {
  console.log(`server listening on port ${port}`);
});
```

</br>

**Dockerfile**

```
FROM   node:12-alpine
COPY   server.js /app/
EXPOSE 8080
CMD    ["node", "/app/server.js"]
```

</br>

**run**

```
$ docker build -t hellonode .
$ docker run --rm -d \
  -p 60000:8080 \
  hellonode
```
</details>
</br>

<details markdown="1">
<summary>7. ghost 블로그 컨테이너 생성</summary>

## 7. ghost 블로그 컨테이너 생성
### 실습한파일
- 문제
```
- Ghost 블로그를 컨테이너로 실행하고 외부에서 접속가능하게 포트를 노출합니다.

- 참고링크
  - https://hub.docker.com/_/ghost
- 컨테이너 이미지 정보
  - 이미지: ghost:latest
  - 리스닝포트: 2368
  - 데이터저장: /var/lib/ghost/content
- 실습내용
  - 60000 포트로 오픈합니다.
  - 업로드 데이터가 유실되지 않게 볼륨을 마운트 합니다.
  - 관리자에서 미리보기 페이지가 정상작동하도록 환경변수를 설정합니다.
  - docker-compose.yml 파일로 작성합니다.
```

**Dockerfile**

```
version: '3'

services:
  ghost:
    image: ghost
    ports:
      - "60000:2368"
    volumes:
      - ./ghost_data:/var/lib/ghost/content
    environment:
      url: http://localhost:60000

```


</details>
</br>

<details markdown="1">
<summary>8. guestBook 배포</summary>

## 8. guestBook 배포
### 실습한파일


**Dockerfile**

```
version: '3'
services:
  frontend:
    image: subicura/guestbook-frontend:latest
    environment:
      PORT: 8000
      GUESTBOOK_API_ADDR: backend:8000
    ports:
      - "62000:8000"
  backend:
    image: subicura/guestbook-backend:latest
    environment:
      PORT: 8000
      GUESTBOOK_DB_ADDR: mongodb:27017
    restart: always
  mongodb:
    image: mongo:4


```


</details>
</br>

<details markdown="1">
<summary>9. workshop-voting 생성(여러개의 서비스 하나의 docker파일로 생성)</summary>

## 9. workshop-voting 생성(여러개의 서비스 하나의 docker파일로 생성)
### 실습한파일


**Dockerfile**

```
# $ cd vote
# $ docker build -t voting-vote .
# $ cd worker
# $ docker build -t voting-worker .
# $ cd result
# $ docker build -t voting-result .

version: '3'

services:
  vote:
    image: voting-vote
    ports:
      - "60001:80"
  redis:
    image: redis:alpine
  worker:
    image: voting-worker
  db:
    image: postgres:9.4
    environment:
      POSTGRES_HOST_AUTH_METHOD: trust
  result:
    image: voting-result
    ports:
      - "60002:80"



```


</details>
</br>

<details markdown="1">
<summary>10. workshop-chatapp 생성</summary>

## 10. workshop-chatapp 생성
### 실습한파일


**Dockerfile**

```
# $ vi src/index.js # (HASURA_GRAPHQL_ENGINE_HOSTNAME 수정 ex-localhost:60004)
# $ docker build -t chatapp .

version: '3.6'

services:
  chatapp:
    image: chatapp
    ports:
    - "60003:8080"
  postgres:
    image: postgres
    restart: always
    volumes:
    - db_data:/var/lib/postgresql/data
    environment:
      POSTGRES_HOST_AUTH_METHOD: trust
  graphql-engine:
    image: hasura/graphql-engine:latest.cli-migrations
    ports:
    - "60004:8080"
    depends_on:
    - "postgres"
    volumes:
    - ./hasura/migrations:/hasura-migrations
    restart: always
    environment:
      HASURA_GRAPHQL_DATABASE_URL: postgres://postgres:@postgres:5432/postgres
      HASURA_GRAPHQL_ENABLE_CONSOLE: "true" # set to "false" to disable console
      HASURA_GRAPHQL_ENABLED_LOG_TYPES: startup, http-log, webhook-log, websocket-log, query-log
      ## uncomment next line to set an admin secret
      # HASURA_GRAPHQL_ADMIN_SECRET: myadminsecretkey
volumes:
  db_data:


```


</details>
</br>