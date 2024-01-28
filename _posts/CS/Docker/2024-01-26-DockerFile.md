---
title:  "[Docker] 🐋 Dockerfile"
excerpt: "Docker CS 지식 정리"
categories:
  - Docker
tags:
  - [CS, Docker]

toc: true
toc_sticky: true
 
date: 2024-01-26
last_modified_at: 2024-01-26
---

## 📖 Dockerfile이 있는데 빌드 서버가 필요할까?

 - 개인 개발이나 작은 규모의 경우 상관없다.  
 - 하지만 협업을 통하여 서로의 버전을 맞춰줘야 하는 경우에는 중요하다.  

실제로 나같은 경우에는 `CI/CD`을 지원하는 `github`를 통하여, 어떤 환경에서 블로그 파일에 접속하든지 똑같은 환경을 보장받고, 코드를 `commit 후 push`하면 자동으로 `build 후 deployment`까지 되는 깃 블로그를 운영하고 있다.  

[내 블로그 github](https://github.com/yyechan0602/yyechan0602.github.io)

![블로그 1](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/f30132e2-547e-45b3-a279-7abf9a7f16b4)

![블로그 2](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/8999087e-0528-4545-b4e5-b08438160cca)

<br>

## 📖 자바 소스 코드로 애플리케이션 빌드

실습은 도커교과서의 4장을 참고하였다.  

### 🍄 메이븐을 사용하여 자바 애플리케이션을 빌드하는 Dockerfile 스크립트


아래 코드는 NASA의 오늘의 천문 사진 서비스에서 오늘자 사진을 받아오는 간단한 REST API이다.  

 - [DockerFile 코드](https://github.com/sixeyed/diamol)  

```dockerfile
FROM diamol/maven AS builder

WORKDIR /usr/src/iotd
COPY pom.xml .
RUN mvn -B dependency:go-offline

COPY . .
RUN mvn package

# app
FROM diamol/openjdk

WORKDIR /app
COPY --from=builder /usr/src/iotd/target/iotd-service-0.1.0.jar .

EXPOSE 80
ENTRYPOINT ["java", "-jar", "/app/iotd-service-0.1.0.jar"]
```

Dockerfile은 일련의 인스트럭션으로 구성되어 있는데, 이를 실행한 결과로 도커 이미지가 만들어진다.  

 - FROM
   - 모든 이미지는 다른 이미지에서 출발하는데, 이 이미지는 diamol/maven을 시작점으로 지정했다.  
   - AS를 사용해 이름을 붙일 수도 있다.  
 - WORKDIR 
   - 컨테이너 이미지 파일 시스템에 디렉터리를 만들고, 해당 디렉터리를 작업 디렉터리로 지정하는 인스트럭션. 
   - 리눅스에서는 /usr/src/iotd
   - 윈도우에서는 C:\usr\src\iotd
 - COPY
   - 로컬 파일 시스템의 파일 혹은 디렉터리를 컨테이너 이미지로 복사하는 인스트럭션
   - --from 인자를 사용해 해당 파일이 호스트 컴퓨터의 파일 시스템이 아니라 앞선 빌드 단계의 파일 시스템에 있는 파일을 알려줄 수 있다.  
   - COPY [원본경로] [복사경로]
   - 위 코드에서는 로컬 파일 시스템에 있는 `pom.xml`파일을 이미지의 작업 디렉토리로 복사하였다.  
 - RUN
   - 빌드 중에 컨테이너 안에서 명령을 실행한 다음 그 결과를 이미지 레이어에 저장하는 기능

이 builder 단계가 끝나고 애플리케이션 이미지를 생성하게 된다.  

<br>

### 🍄 이미지 빌드

아래와 같이 `cd (파일위치)` 이후, `docker image build -t image-of-the-day .`를 실행해 주었다.  
`docker image build -t [이미지의 이름] [이미지가 들어갈 디렉토리]` 으로 `.`을 빼먹으면 안된다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/acf1d84e-adc4-48a5-a226-2b574cfde32f)  

꽤 많은 로그가 찍히며 이는 의존 모듈을 다운받고, 자바 빌드을 실행하라는 내용이다.  
이제 아래와 같이 컨테이너간 통신에 사용되는 도커 네트워크를 생성해주고, 80번 포트를 호스트 컴퓨터를 통해 공개하고, nat 네트워크에 컨테이너를 접속해 주었다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/293a5dbf-809c-469c-b432-c7d3e8638b20)  

이후, 웹 브라우저에서 [http://localhost:800/](http://localhost:800/)에 접속해주면 `NASA`에서 제공해주는 오늘 사진에 대한 정보를 `JSON`으로 받을 수 있다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/4a09c397-351f-44e0-9464-a99e315becf9)  

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁