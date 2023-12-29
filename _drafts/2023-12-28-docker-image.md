---
title: Docker Intro
date: 2023-12-27 15:00:00
categories:
  - Machine Learning
  - MLOps
tags:
  - mlops
  - machine-learning
  - backend
  - python
  - docker
  - devops
typora-root-url: ../
---





## Docker

> 개념 입문, 실습 공부노트

지난 글에서 도커에 대해 전반적으로 이해하고 여러 컨테이너를 실행해보는 시간을 가졌다. 이번 글에서는 이미지를 만들고 서버에 배포해보는 과정을 다룬다.



### Image

- 컨테이너 실행에 필요한 파일과 설정값 등을 포함하고 있는 것
- 도커는 컨테이너의 상태를 그대로 이미지로 저장함 (Dockerizing)
  - VM의 snapshot과 비슷한 방식




### Sample

- Sinatara: 가벼운 웹 프레임워크

  - 새로운 폴더에 `Gemfile`과 `app.rb` 작성

  - `Gemfile`: 패키지 관리

    - ```
      source 'https://rubygems.org'
      gem 'sinatra'
      ```

  - `app.rb`: 호스트명을 출력하는 웹 서버 생성

    - ```ruby
      require 'sinatra'
      require 'socket'
      
      get '/' do
        Socket.gethostname
      end
      ```

  - 패키지 설치 및 서버 실행

    ```
    bundle install
    bundle exec ruby app.rb
    ```

  - Docker를 활용해 ruby container를 실행

    - `docker run --rm -p 4567:4567 -v $PWD:/usr/src/app -w /usr/src/app ruby bash -c "bundle install && bundle exec ruby app.rb -o 0.0.0.0"`

    - 호스트의 디렉토리를 ruby container의 디렉토리에 mount하기만 하면 local 개발 환경 구축을 도커로 대신할 수 있음 (개발=테스트=운영)

  - ```
    Calling `DidYouMean::SPELL_CHECKERS.merge!(error_name => spell_checker)' has been deprecated. Please call `DidYouMean.correct_error(error_name, spell_checker)' instead.
    ```

    - 실습 과정에서 위의 에러가 발생. 버전문제인 것으로 

- 도커: 컨테이너 기반의 오픈소스 가상화 플랫폼
- 규격화: 다양한 프로그램, 실행 환경을 컨테이너로 추상화하고 동일한 인터페이스 제공
- 프로그램의 배포&관리 단순화
- 컨테이너: 격리된 공간에서 프로세스가 동작하는 기술
- 가상화
  - 기존엔 OS 가상화(무겁고 느리다)
  - 리눅스 컨테이너: 프로세스를 격리
  - 하나의 서버에 여러 개의 컨테이너를 실행하면 서로 영향x, 독립적으로 실행
- 이미지: 컨테이너 실행에 필요한 파일과 설정값 등을 포함하고 있는 것. (불변)
  - 컨테이너는 이미지를 실행한 상태.
  - 보통 용량이 수백메가, 기존 이미지에 변화가 생길 때 재 다운로드 과정이 비효율
- 레이어: 이 문제를 해결하기 위함
  - 기존 베이스 이미지를 제외한 추가 레이어만 다운로드
  - 컨테이너 생성 시에도 rw레이어만 추가, 실행 중 변화는 rw레이어에만 저장.
  - 가상화 특성상 이미지 용량 크고 여러 서버에 배포하는 것을 감안하면 단순하지만 매우 영리한 설계



### Installation

- Docker for Mac

- `docker version`

  - ```
    Client:
     Cloud integration: v1.0.35+desktop.5
     Version:           24.0.7
     API version:       1.43
     Go version:        go1.20.10
     Git commit:        afdd53b
     Built:             Thu Oct 26 09:04:20 2023
     OS/Arch:           darwin/amd64
     Context:           desktop-linux
    
    Server: Docker Desktop 4.26.1 (131620)
     Engine:
      Version:          24.0.7
      API version:      1.43 (minimum version 1.12)
      Go version:       go1.20.10
      Git commit:       311b9ff
      Built:            Thu Oct 26 09:08:02 2023
      OS/Arch:          linux/amd64
      Experimental:     false
     containerd:
      Version:          1.6.25
      GitCommit:        d8f198a4ed8892c764191ef7b3b06d8a2eeb5c7f
     runc:
      Version:          1.1.10
      GitCommit:        v1.1.10-0-g18a0cb0
     docker-init:
      Version:          0.19.0
      GitCommit:        de40ad0
    ```



### Run

`docker run [OPTIONS] IMAGE [:TAG|@DIGEST] [COMMAND] [ARG...]`

| 옵션  | 설명                                                   |
| :---- | :----------------------------------------------------- |
| -d    | detached mode 흔히 말하는 백그라운드 모드              |
| -p    | 호스트와 컨테이너의 포트를 연결 (포워딩)               |
| -v    | 호스트와 컨테이너의 디렉토리를 연결 (마운트)           |
| -e    | 컨테이너 내에서 사용할 환경변수 설정                   |
| –name | 컨테이너 이름 설정                                     |
| –rm   | 프로세스 종료시 컨테이너 자동 제거                     |
| -it   | -i와 -t를 동시에 사용한 것으로 터미널 입력을 위한 옵션 |
| –link | 컨테이너 연결 [컨테이너명:별칭]                        |

- ubuntu 16.04 container

  - `docker run ubuntu:16.04`
    - 이 경우 사용할 이미지인 ubuntu:16.04가 저장되어 있지 않으므로 `pull` - `create` - `start` 를 자동으로 수행
    - 컨테이너는 정상 실행되지만 명령어가 없으므로 생성되자마자 종료
    - 컨테이너는 프로세스이기 때문에 실행중인 프로세스가 없으면 종료

  - `docker run --rm -it ubuntu:16.04 /bin/bash`
    - bash 쉘 실행
    - `exit`으로 쉘을 종료하면 컨테이너도 함께 종료

- redis container

  - 메모리 기반의 다양한 기능을 가진 스토리지
  - 6379 포트 통신, `telnet` 명령어로 테스트 가능
  - `docker run -d -p 1234:6379 redis`
    - 컨테이너 실행 직후 쉘로 돌아왔지만, -d 옵션으로 백그라운드 모드로 동작중
    - 이 경우 컨테이너 id를 이용하여 제어 가능
    - `-p` 옵션으로 호스트의 1234 포트를 6379 포트로 연결함 (localhost 1234 포트 접속시 redis 사용 가능)
    - `telnet` command가 없어 brew install 후 실행
    - `telnet localhost 1234`, `set mykey hello`, `get mykey`

- MySQL 5.7 container

  - `docker run -d -p 3306:3306 -e MYSQL_ALLOW_EMPTY_PASSWORD=true --name mysql mysql:5.7`
  - test: `mysql -h127.0.0.1 -uroot`, `show databases;`

- WordPress container

  - `docker run -d -p 8080:80 --link mysql:mysql -e WORDPRESS_DB_HOST=mysql -e WORDPRESS_DB_NAME=wp -e WORDPRESS_DB_USER=wp -e WORDPRESS_DB_PASSWORD=wp wordpress`
  - `--link` 옵션을 통해 환경변수와 IP 정보를 공유하는데 링크한 컨테이너의 IP 정보를 `/etc/hosts`에 자동으로 입력
  - 워드프레스 컨테이너가 MySQL db의 정보를 알 수 있게 됨

- TensorFlow

  - `docker run -d -p 8888:8888 -p 6006:6006 teamlab/pydata-tensorflow:0.1`
  - 8888 포트로 들어가니 jupyter가, 6006포트는 TensorBoard가 나옴



### Major commands

- `docker ps [OPTIONS]`: 컨테이너 목록 확인
  - `docker ps`: 실행중인 컨테이너 목록
  - `docker ps -a`: 모든 컨테이너 목록
- `docker stop [OPTIONS] CONTAINER [CONTAINER...]`: 컨테이너 중지
  - 컨테이너 ID 혹은 이름 입력
  - 컨테이너 ID 전체 길이는 64자리지만 앞부분이 겹치지 않는다면 1-2자리만 입력해도 됨
- `docker rm [OPTIONS] CONTAINER [CONTAINER...]`: 컨테이너 제거
- `docker images [OPTIONS] [REPOSITORY[:TAG]]`: 다운로드한 이미지 목록
  - 이미지가 너무 많이 쌓이면 용량을 차지하므로 사용하지 않는 이미지는 지우는 것이 좋음
- `docker pull [OPTIONS] NAME[:TAG|@DIGEST]`: 이미지 다운로드
- `docker rmi [OPTIONS] IMAGE [IMAGE...]`: 이미지 삭제
- `docker logs [OPTIONS] CONTAINER`: 컨테이너 로그 확인
  - `docker logs CONTAINER`: 전체 로그 출력
  - `docker logs --tail 10 CONTAINER`: 마지막 10줄만 출력
  - `docker logs -f CONTAINER`: 실시간 로그 생성 확인
- `docker exec [OPTIONS] CONTAINER COMMAND [ARG...]`: 컨테이너 명령어 실행
  - `run`은 새로 컨테이너를 만들어 실행, `exec`는 실행중인 컨테이너에 명령



### Container updates

- Update container
  - pull: 새 버전 이미지 다운
  - stop, rm: 기존 컨테이너 삭제
  - run: 새 이미지 기반 새 컨테이너 실행
- 컨테이너 삭제 시 컨테이너에서 생성된 파일이 사라짐
  - 유지해야 할 데이터는 외부 스토리지에 저장해야 함
  - 클라우드 서비스(AWS S3, ...) or 데이터 볼륨을 컨테이너에 추가해서 사용(호스트 디렉토리 마운트)



### Docker compose

- 컨테이너 조합이 많아지고 여러 설정이 추가되면 명령어가 금방 복잡해짐

- 이를 해결하기 위한 YAML 방식의 config 파일을 이용

- 예시: wordpress

  - ```yaml
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





## Reference

- https://subicura.com/2017/01/19/docker-guide-for-beginners-1.html?utm_source=subicura.com&utm_medium=referral&utm_campaign=k8s



















