# Docker tutorial
--------------
## 도커 설치

```bash
$ curl -fsSL https://get.docker.com/ | sudo sh
```

#### 설치확인

```bash
$ docker version
```
Client와 Server 정보가 출력되면 설치 완료

## 도커 기본 명령어
#### 컨테이너 목록 확인
- detached mode로 실행중인 컨테이너 목록 출력
- `-a` : 종료된 컨테이너 포함하여 컨테이너 목록 출력

```bash
$ docker ps [OPTIONS]
```

#### 컨테이너 시작
- 중지된 컨테이너 시작

```bash
$ docker start [OPTIONS] CONTAINER [CONTAINER...]
```

#### 컨테이너 중지
- 실행중인 컨테이너 중지

```bash
$ docker stop [OPTIONS] CONTAINER [CONTAINER...]
```

#### 컨테이너 제거
- 종료된 컨테이너를 완전히 제거

```bash
$ docker rm [OPTIONS] CONTAINER [CONTAINER...]

$ docker rm -v $(docker ps -a -q -f status=exited) # 중지된 컨테이너들을 한번에 제게
```

#### 이미지 목록 출력
- 도커가 다운로드한 이미지 목록 출력

```bash
$ docker images [OPTIONS] [REPOSITORY]
```

#### 이미지 다운
- 이미지 다운로드
- 이미 존재하는 이미지가 업데이트 되었을 때 새 버전을 다운 받을 수 있음

```bash
$ docker pull [OPTIONS] NAME [:TAG|@DIGEST]
```

#### 이미지 삭제
- 이미지 삭제

```bash
$ docker rmi [OPTIONS] IMAGE [IMAGE...]
```

#### 컨테이너 로그 출력
- -f : 실시간으로 로그 출력

```bash
$ docker logs [OPTIONS] CONTAINER
```

#### 컨테이너 명령어 실행
- `run` 명령어와 유사하지만 `run`명령어는 새로운 컨테이너를 만들어서 실행
- `exec` 명령어는 실행중인 컨테이너에 명령

```bash
$ docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
```

## 컨테이너 실행

#### 도커 실행 명령어
```bash
$ docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]
```

#### 자주 사용하는 옵션
|옵션|설명|
|---|---|
|-d|detached mode(백그라운드 모드)|
|-p|호스트와 컨테이너의 포트를 연결(포워딩)|
|-v|호스트와 컨테이너의 디렉토리를 연결(마운트)|
|-e|컨테이너 내에서 사용할 환경변수 설정|
|-name|컨테이너 이름 설정|
|-rm|프로세스 종료시 컨테이너 자동 제거|
|-it|-i와 -t를 동시에 사용한 것으로 터미널 입력을 위한 옵션|
|-link|컨테이녀 연결|

#### 컨테이너 생성
```bash
$ docker run ununtu:16.04
```

#### 컨테이너 실행
```bash
$ docker run --rm -it ubuntu:16.04 /bin/bash
```

#### 컨테이너 종료
```bash
$ exit
```

## Redis 컨테이너
- `Redis`는 메모리 기반의 다양한 기능을 가진 스토리지
- `6379` 포트로 통신하며 `telnet`명령어로 테스트 가능
- `detached mode`로 실행하기 위해 `-d`옵션을 추가하고 `-p`옵션을 추가하여 컨테이너의 포트를 호스트의 포트로 연결

#### Redis 컨테이너 실행
```bash
$ docker run -d -p 1234:6379 redis

# redis test
$ telnet localhost 1234
set str redisTest
+OK
get str
$9
resdisTest
```

## MySQL 5.7 컨테이너
- `-e`옵션을 사용하여 환경변수 설정
- `--name` 옵션을 사용하여 컨테이너의 ID 대신 쉬운 별칭 부여

#### MySQL 컨테이너 실행

```bash
$ docker run -d -p 3306:3306 \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
  --name mysql \
  mysql:5.7

# MySQL test
$ mysql -h127.0.0.1 -uroot

mysql> show databases; # result : DB리스트 출력
```

## WordPress 컨테이너 실행
- --link : 환경변수와 IP정보를 공유

```bash
# create mysql database
$ mysql -h127.0.0.1 -uroot

mysql> create database study CHARACTER SET utf8;
mysql> grant all privileges on wp.* to wp@'%' identified by 'wp';
mysql> flush privileges;
mysql> quit

# run wordpress container
docker run -d -p 8080:80 \
  --link mysql:mysql \
  -e WORDPRESS_DB_HOST=mysql \
  -e WORDPRESS_DB_NAME=study \
  -e WORDPRESS_DB_USER=study \
  -e WORDPRESS_DB_PASSWORD=study \
  wordpress
```

- 'http://0.0.0.0:8080' 으로 접속

## 컨테이너 업데이트
1. 새 버전의 이미지 다운(pull)
2. 기존 컨테이너 삭제(stop, rm)
3. 새 컨테이너 실행(run)

#### 데이터 볼륨 설정

```bash
$ docker run -d -p 3306:3306 \
  -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
  --name mysql \
  -v /docker/data:/var/lib/mysql \ # Volume mount
  mysql:5.7
```

#### Dokcer Compose
- 복잡한 설정을 쉽게 관리하기 위해 `YAML` 방식의 설정 파일을 이용한 툴
- 설치

```bash
$ curl -L "https://github.com/docker/compose/releases/download/1.9.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose

# 설치 확인
docker-compose version
```

- wordpress 생성

```yml
version: '2'

services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: wordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     volumes:
       - wp_data:/var/www/html
     ports:
       - "8000:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_PASSWORD: wordpress
volumes:
    db_data:
    wp_data:
```
