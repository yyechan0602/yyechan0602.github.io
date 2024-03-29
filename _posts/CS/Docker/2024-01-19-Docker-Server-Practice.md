---
title:  "[Docker] 🐋 도커 실습 (Hello World, Httpd, Nginx)"
excerpt: "Docker CS 지식 정리"
categories:
  - Docker
tags:
  - [CS, Docker]

toc: true
toc_sticky: true
 
date: 2024-01-19
last_modified_at: 2024-01-19
---

## 📖 도커 명령어

도커의 명령어는 `docker ~`으로 시작한다.  
이후 붙은 명령어는 크게 12가지가 있다.  

`docker run hello-world`와 같은 방식으로 수행도 가능하지만, 실제로 이는 `docker container run`의 축약형이다.  
또, `docker ps == docker container ls`로써 현재 컨테이너를 보여주는 명령어로 많이 사용한다.  

 - container
   - start
   - stop
   - create
   - run
   - exec
   - ...
 - image
   - pull
   - search
   - ...
 - volume
   - create
   - rm
   - ...
 - network
   - create
   - rm
   - ...

### 🍄 컨테이너로 Hello World 실행하기

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/e63a6cd8-9630-4a46-92e0-8d2c622aeccd)

 - Docker 클라이언트가 Docker 데몬과 통신했다.
 - Docker 데몬이 hello-world이미지를 Docker Hub에서 pull 했다
 - Docker 데몬이 hello-world이미지에 해당하는 컨테이너를 생성했다.
 - 이와 같은 메시지를 출력하기 위해 docker 데몬이 -a 옵션으로 표준입출력에 붙어서 메세지를 출력했다

이때, 자바에서 봤던 `Daemon`이 나왔는데, 이는 자바에서의 `Daemon`은 주 스레드의 작업을 돕는 보조적인 역할을 수행하는 스레드로써, 주 스레드가 종료되면 강제적으로 자동 종료되는 스레드를 의미했었다.  

도커를 사용할때, docker라는 명령어를 맨 앞에 붙인다.  
그리고 실제 docker는 user/bin/docker에 위치한다.  
하지만, 실제 프로세스는 /user/bin/dockerd 파일로 실행된다.  

도커의 구조는 크게 2가지로 나누어지는데 하나는 클라이언트로써의 도커이고, 나머지는 서버로써의 도커이다.  
실제로 컨테이너 생성 및 도커 이미지 관리는 서버도커이며, 서버관리를 하는 도커를 `도커 데몬` 이라고 한다.  

도커는 API에 따라서 도커 엔진을 수행하는데, 이 API를 사용가능하도록 CLI(Command Line Interface) 제공을 도커 클라이언트라 한다.  

<br>

### 🍄 Apache 서버로 웹페이지 출력하기  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/11408803-5385-451d-9e50-0e8d9982ca49)  

위에서 -d는 백그라운드에서 실행, -p `port:port`는 `호스트 Port:container Port`

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/93c0ee91-1a6e-4fa6-bcc4-485854a6f8d3)  

<br>

### 🍄 Nginx 서버로 웹페이지 출력하기  

위와 똑같이 `Nginx` 이미지를 사용하여, 다음과 같이 진행해 주었다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/ea33dbc4-1165-4acc-9207-314219d8d537)  

어 그러자 위와 같이 `nginxServer`를 `up`하는 과정에서 `Bind failed` 오류가 발생하였다.  
이는 위의 `ApacheServer`가 이미 `8080 Port`를 사용하고 있기 때문에 발생하는 오류이다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/505afb9b-a209-4f08-a8f5-046193a2783f)  

컴퓨터는 각 프로세스마다 Port를 배정하여 외부와 통신하게 된다.  
이때, `-p ComputerPortNum:DockerPort` 앞의 Num은 `호스트의 Port`, 뒤의 Num은 `Container의 Port`이다.  
따라서 호스트의 Port번호가 서로 겹치므로 이를 다음과 같이 수정해주면 된다.

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/a9e668f0-2fab-4962-9882-da14d5d06ab2)  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/ed10e868-78f0-4314-90f7-4e3ea1829902)  

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁