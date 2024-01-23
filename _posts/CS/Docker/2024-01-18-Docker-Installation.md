---
title:  "[Docker] 🐋 도커 설치"
excerpt: "Docker CS 지식 정리"
categories:
  - Docker
tags:
  - [CS, Docker]

toc: true
toc_sticky: true
 
date: 2024-01-18
last_modified_at: 2024-01-18
---

## 📖 도커 설치

도커는 리눅스 위에서 작동하므로, 윈도우에서 실행시키기 위해서는 크게 2가지 방법이 있다.  
 - VMWare와 같은 가상환경 위에 리눅스를 설치 후, 그 위에 도커를 설치하는 방법
 - HyperVisor를 사용하여 윈도우 환경에 설치하는 방법이 있다.

이번 실습은 `docker-desktop`을 사용하여 진행할 것이다.  
도커를 사용하기 위한 최소한의 조건이 있는데 이는 64bit 이상 운영체제에서만 작동한다는 것이다.

[https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)

위의 페이지에서 다운받으면 된다.  

<br>

### 🍄 docker desktop

이후, 설치후 실행시 다음과 같은 화면이 나온다.  
이는 `GUI`로 현재 `Docker Container`를 보여주는 화면으로써, 이후 실습은 `cmd`창에서 실시한다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/8e4f0353-ac16-4d97-9c50-5f9e0180a3fc)

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁