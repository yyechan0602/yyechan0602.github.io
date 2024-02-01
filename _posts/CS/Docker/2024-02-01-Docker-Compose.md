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

<br>

### 🍄 실습



<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁