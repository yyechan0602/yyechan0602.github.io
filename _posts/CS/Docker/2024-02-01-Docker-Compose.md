---
title:  "[Docker] 🐋 도커 컴포즈 (Docker Compose)"
excerpt: "Docker CS 지식 정리"
categories:
  - Docker
tags:
  - [CS, Docker]

toc: true
toc_sticky: true
 
date: 2024-02-01
last_modified_at: 2024-02-01
---

## 📖 도커 컴포즈

`LAMP`와 같은 구조를 다룰 때, 여러 컨테이너를 함께 사용하게 된다.  
이때 여러 컨테이너와 이미지 및 볼륨을 생성, 삭제, 종료, 폐기와 같은 일들을 해줘야 하는데, 이를 일일이 ps 커맨드로 확인하기는 수고스럽다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/2dd17151-0c3f-4ca0-bae9-b2d30e838f39)

따라서 위와 같이 `시스템 구축과 관련된 명령어를 하나의 텍스트파일(정의 파일)에 기재해 명령어 한번에 시스템 전체를 실행하고 종료와 폐기까지 한번에 하는 도구`가 바로 `도커 컴포즈`이다.  

도커 컴포즈는 시스템 구축에 필요한 파일을 `YAML(YAML Ain't a Markup Language)` 포맷으로 기재한 정의 파일을 이용해 전체 시스템을 일괄 실행/ 일괄 종료 및 삭제를 할 수 있는 도구이다.  
도커 컴포즈는 도커 엔진과 별개의 소프트웨어로 이는 쿠버네티스 또한 동일하다.  

<br>

<div class="notice--warning" markdown="1">
도커 컴포즈와 쿠버네티스의 차이점  

 - 도커 컴포즈는 컨테이너를 생성하고 삭제하는 기능을 가진다.
 - 쿠버네티스는 컨테이너 관리까지 가능하다.
</div>

도커 컴포즈를 사용하기 위해서는 `Dockerfile` 스크립트로 이미지를 빌드할 때처럼 호스트 컴퓨터에 폴더를 만들고 이 폴더에 정의 파일(YAML)을 배치한다.  

<br>

### 🍄 컴포즈 파일(정의 파일) 작성법

`YAML` 형식을 따르며 확장자는 `.yml`이다.  
파일 이름은 무조건 `docker-compose.yml` 이여야 하며, 이를 바꾸기 위해서는 `-f`옵션을 사용하여야 한다.  
공백에 따라 의미가 달라지므로, 처음 사용한 공백 개수만큼 뒤에도 동일하게 맞춰줘야 한다.  

```yml
version: "3"
services:
  컨테이너_이름:
    image: 이미지_이름
    networks:
      - 네트워크_이름
    ports:
      - 포트_설정
    ...

  컨테이너_이름2:
    image: 이미지_이름
    networks:
      - 네트워크_이름
    ...  

networks:
  네트워크_이름:

volumes:
  볼륨_이름1:
  볼륨_이름2:
  ...
```

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁