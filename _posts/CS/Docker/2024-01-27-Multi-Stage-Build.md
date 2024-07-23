---
title:  "[Docker] 🐋 멀티스테이지 빌드 (Multi-Stage Build)"
excerpt: "Docker CS 지식 정리"
categories:
  - Docker
tags:
  - [CS, Docker]

toc: true
toc_sticky: true
 
date: 2024-01-27
last_modified_at: 2024-01-27
---

## 📖 Multi-Stage Build

애플리케이션 개발시 개발 환경에서 사용한 라이브러리가 실제 app에서 전부 다 사용되는 것은 아니다.  
app을 실행하기 위해서 필요한 실행 모듈만 배치하는 것이 리스스 관리 측면에서 효율적이다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/4287053b-ceda-4d27-8d2e-835b2cb8b22e)


### 🍄 Multi-Stage Build 정의

**컨테이너 이미지를 만들면서 빌드 등에는 필요하지만, 최종 컨테이너 이미지에는 필요 없는 환경을 제거할 수 있도록 단계를 나누어 기반 이미지를 만드는 방법**

<br>

### 🍄 3가지 장점

 - 표준화
   - 사용자가 어떤 운영체제를 사용하든, 로컬 컴퓨터에 어떤 도구가 설치되었는지와 상관없이, 모든 빌드 과정은 도커 컨테이너 내부에서 진행된다.  
 - 성능 향상
   - 멀티 스테이지 빌드의 각 단계는 자신만의 캐시를 따로 갖는다.
   - 도커는 빌드 중에 각 인스트럭션에 해당하는 레이어 캐시를 찾는다.
   - 이를 다시 재활용하면 90% 이상의 성능향상을 노려볼 수 있다.
 - 최종 산출물인 이미지를 가능한 작게 유지할 수 있다.
   - 앞에서 말한 정의처럼 그 도구가 최종 app에서 사용되지 않는다면 빼버릴 수 있다.
   - 예를 들어 `curl`과 같은 이미지 다운 도구는 이미지를 다 다운받은 후에는 필요가 없으므로, 최종 app 이미지에서는 포함시키지 않아도 된다.  

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁