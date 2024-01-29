---
title:  "[Docker] 🐋 이미지 공유 (Sharing Docker Image)"
excerpt: "Docker CS 지식 정리"
categories:
  - Docker
tags:
  - [CS, Docker]

toc: true
toc_sticky: true
 
date: 2024-01-28
last_modified_at: 2024-01-28
---

## 📖 도커 이미지 참조

도커 플랫폼은 소프트웨어 배포 기능을 내장하고 있으며, Docker Hub 같은 페이지가 유명하다.  
위 사이트에서 이미지를 내려받기 위해서는 참조 주소가 필요한데 이는 다음과 같다.  

**[도메인]/[이름]/[레포지토리 이름]:[이미지 태그]**

 - 도메인은 `www.naver.com`와 같은 일반적으로 dockerhub를 사용한다면, `hub.docker.com`
   - 이미지가 저장된 레지스트리의 도메인을 의미한다
 - 이름은 이미지 작성자의 계정이름, 개인 혹은 단체의 이름
 - 레포지토리 이름은 application의 이름을 의미한다.  

<br>

## 📖 도커 이미지 푸시

이미지를 도커허브에 푸시하기 위해서는 기본적으로 도커 허브 계정이 필요하다.  
계정 생성 후,  `docker login --username [ID]`로 로그인하면 된다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/2743cd15-df57-412d-852a-94487810383f)

이후 다음과 같이 기존 이미지에 새로운 이미지 참조를 부여해 주었다.  
기존 이미지는 내용은 다음과 같다

 - [DockerFile 코드](https://github.com/sixeyed/diamol/tree/master/ch04/exercises/image-gallery)  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/9e4af6ed-63d1-439e-b1cf-7a588f352479)

v1 이미지를 레포지토리에 푸시하였다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/5e920e8e-f69b-417c-83bc-cb4f134a75d7)

이후 내 dockerHub에 들어가서 확인해 본 결과 레포지토리애 이미지가 push된 것을 확인할 수 있었다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/a7714d9b-cdca-4e09-b65d-fc956fc59c02)

<br>

### 🍄 Image-Share

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁