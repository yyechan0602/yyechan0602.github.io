---
title:  "[Docker] 🐋 도커 Lifecycle"
excerpt: "Docker CS 지식 정리"
categories:
  - Docker
tags:
  - [CS, Docker]

toc: true
toc_sticky: true
 
date: 2024-01-23
last_modified_at: 2024-01-23
---

## 📖 도커 Lifecycle

도커의 생애주기는 다음과 같이 `create, start, rm, stop` 4가지로 이루어져 있다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/48ff1369-7d7a-4422-b701-96f10f790d81)

이때, 중요한 점은 동작 중인 컨테이너는 삭제가 불가능하다.  
따라서, 동작 중인 컨테이너를 삭제하기 위해서는 정지 후 삭제하여야 한다.  

<br>

### 🍄 docker run

`docker run` 은 다음 3가지 명령을 합친 명령어이다.  

 - docker pull
 - docker create
 - docker start

이를 실행하면 docker hub에서 이미지를 다운받은 후, 이미지를 생성하고 이를 실행시킨다.  

<br>

### 🍄 docker stop

`docker stop 컨테이너 이름` 을 통해서 컨테이너를 종료시킨다.

<br>

### 🍄 docker rm

`docker rm 컨테이너 이름` 을 통해서 컨테이너를 삭제시킨다.

<br>

### 🍄 docker ps

`docker ps` 을 통해서 현재 실행하는 컨테이너 목록을 출력한다.  
옵션으로 `-a`를 추가하여 현재 존재하는 컨테이너 목록을 출력한다.  

위 명령을 사실 축약형으로 `docker container ls`로도 사용할 수 있다.  

<br>

## 📖 도커 생성 후 삭제

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/4c9e494c-48ae-4361-922e-67b30c2c0855)

`docker run` 을 통해 `httpd` 이미지로 `apaServer` 를 생성하였다.  
이후 `docker ps`를 사용하여 실행하는 컨테이너 목록을 출력하였다.  

`docker stop` 을 사용하여 컨테이너 종료 후, `docker ps -a`로 출력하는 것을 확인하였다.  
`docker rm` 후 더 이상 컨테이너가 존재하지 않는 것을 확인했다.  

<br>

## 📖 아파치 서버

위에서 사용한 `httpd` 이미지 파일이 바로 `Apache`로 `웹 서버 기능을 제공하는 소프트웨어`이다.  
위에서 실행한 웹 서버에 접속하기 위해서 포트 연결이 필요하다.  
이를 위해서 `-p host-PortNum:Container-PortNum`을 통해서 호스트의 포트와 Container의 포트를 연결하여 이를 통한 접속이 가능하다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/4febacde-44b8-4074-b1b9-1df5f7a12437)

따라서, 다음과 같이 포트 번호를 붙여서 연결해주면, 내 `IP주소의 8080 Port`를 통해서 접속이 가능하다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/ddf905e0-c570-4229-bf69-2ea71da2a369)

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/cdba9225-99c1-4411-a7d5-59f9b7f5524b)

<br>

## 📖 이미지 삭제

위에서 `run` 명령어를 사용하면서 저장한 이미지는 사라지지 않고 컴퓨터에 저장되어 있다.  
이를 삭제하기 위해서는 `docker image rm`를 사용하면 된다.  

삭제할 이미지 파일의 ID를 확인하기 위하여 `docker image ls`를 입력해준다.  
이후, `docker image rm`을 사용하여 삭제해 주었다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/de62ce41-2807-4820-ab0e-49c30e0ebc4e)

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁