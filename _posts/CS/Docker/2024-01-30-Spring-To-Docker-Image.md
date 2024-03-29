---
title:  "[Docker] 🐋 Spring 서버를 Docker로 띄우기"
excerpt: "Docker CS 지식 정리"
categories:
  - Docker
tags:
  - [CS, Docker]

toc: true
toc_sticky: true
 
date: 2024-01-30
last_modified_at: 2024-01-30
---

## 📖 SpringBoot Server

연습을 위하여 간단하게 `demo/hello` API와 get형식의 `demo/demo`를 가지고 있는 `Demo Server`를 올렸다.  
스프링부트는 IntelliJ에서 진행할 예정이며, 자바는 `JDK-17`/ 스프링부트 버전은 `3.2.2`을 사용하였다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/8d5414b8-b467-41f8-89b4-be6dfaa1bba5)

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/651d6cf4-6d82-4cd6-af84-8261705c2167)

위와 같이 프로젝트를 만들어 주었다.  
아래는 MVC모델로 구현한 소스코드이다.  

<br>

### 🍄 소스 코드

<details>
<summary>Controller</summary>
<div markdown="1">

```java
package com.example.demo.Controller;

import com.example.demo.Service.DemoService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("demo")
public class DemoController {

    private final DemoService demoService;

    @Autowired
    public DemoController(DemoService demoService) {
        this.demoService = demoService;
    }

    @RequestMapping("/hello")
    public String hello() {
        return "hello";
    }

    @GetMapping()
    public String getName(int index) {
        System.out.println(index);
        return demoService.DemoDTO(index);
    }
}
```

</div>
</details>

<br>

<details>
<summary>DTO</summary>
<div markdown="1">

```java
package com.example.demo.DTO;

public class DemoDTO {
    String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

```

</div>
</details>

<br>

<details>
<summary>Entity</summary>
<div markdown="1">

```java
package com.example.demo.entity;

import jakarta.persistence.*;
import lombok.AllArgsConstructor;
import lombok.Getter;
import lombok.NoArgsConstructor;
import lombok.Setter;

@Entity
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
@Table(name = "Demo")
public class Demo {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int index;

    @Column(nullable = false)
    private String name;
}

```

</div>
</details>

<br>

<details>
<summary>Repository</summary>
<div markdown="1">

```java
package com.example.demo.Repository;

import com.example.demo.DTO.DemoDTO;
import com.example.demo.entity.Demo;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface DemoRepository extends JpaRepository<Demo, Integer> {
}

```

</div>
</details>

<br>

<details>
<summary>Service</summary>
<div markdown="1">

```java
package com.example.demo.Service;

import com.example.demo.DTO.DemoDTO;
import com.example.demo.Repository.DemoRepository;
import com.example.demo.entity.Demo;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Repository;
import org.springframework.stereotype.Service;

@Service
public class DemoService {
    private final DemoRepository demoRepository;

    @Autowired
    public DemoService(DemoRepository demoRepository) {
        this.demoRepository = demoRepository;
    }

    public String DemoDTO(int index) {
        Demo demo = demoRepository.findById(index).get();

        return demo.getName();
    }
}
```

</div>
</details>  

<br>

<details>
<summary>Repository</summary>
<div markdown="1">

```java
package com.example.demo.Repository;

import com.example.demo.DTO.DemoDTO;
import com.example.demo.entity.Demo;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface DemoRepository extends JpaRepository<Demo, Integer> {
}

```

</div>
</details>

<br>

<details>
<summary>application.yml</summary>
<div markdown="1">

기존에 있던 application.properties 파일을 삭제하고, application.yml로 변경해주었다.  
이때 `local db`를 사용하였는데, 이를 위하여 docker에서 기본적으로 설정되어 있는 `host` network에 접속하기 위하여 `host.docker.internal`를 지정해주었다.  

![image1](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/2f658b66-556f-4a40-9aab-31e083012d61)


```yml
spring:
  datasource:
    url: jdbc:mariadb://host.docker.internal:3306/demo
    driver-class-name: org.mariadb.jdbc.Driver
    username: 'root'
    password: '1234'
  jpa:
    open-in-view: false
    generate-ddl: true
    show-sql: true
    hibernate:
      ddl-auto: update
  application:
    name: demo
  profiles:
    active: dev

server:
  port: 8080

```

</div>
</details>

<br>

<details>
<summary>의존성 주입</summary>
<div markdown="1">

build.gradle에 있는 dependencies 

```
//swagger
    implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.0.2'
    //Database
    runtimeOnly 'org.mariadb.jdbc:mariadb-java-client' // MariaDB
```

</div>
</details>

<br>

## 📖 docker 이미지 만들기

아래와 같이 오른쪽의 Gradle 항목에서 `build/bootJar`을 클릭하여 파일 빌드를 해준다.  
그러면 `build/libs` 아래에 `.jar`파일이 생성되게 된다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/d0103143-e104-4483-a17b-aa2a4765e7fc)

`dockerfile`이라는 이름의 파일을 프로젝트 root폴더 아래에 만들어준다.  
아래와 같이 내용을 적어준다.  

- dockerfile
```dockerfile
FROM openjdk:11
ARG JAR_FILE=*.jar
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```

<br>

### 🍄 실습

아래와 같이 하면 도커 이미지를 빌드해주고, `Docker Hub`에 이를 올린다.  

```
docker build -t [도커허브 ID]/[Repository 이름] .
docker push [도커허브 ID]/[Repository 이름]
```

아래와 같이 `docker Hub`에서 이미지를 다운받아서 실행시켰다.  

```
docker run -d -i -p 8080:8080 [도커 허브 ID/이미지 이름]
```

아래는 실행 화면들이다.  

![demo](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/1ff74e51-60cc-468a-97e1-4fb44dbfd12e)


![swagger](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/90f4be09-c230-43c5-be28-2c5f4c59fdef)

![get](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/369e0500-eb05-449e-866c-1d754bb6cbf2)

<br>

## 📖 멀티 스테이지를 통해 이미지 만들기

기존과 동일한 코드에서 `Dockerfile`을 변경해주면 된다.  

```
# build
FROM gradle:8.5 AS builder
WORKDIR /build

COPY build.gradle settings.gradle /build/
RUN gradle build -x test --parallel --continue > /dev/null 2>&1 || true

COPY . /build
RUN gradle build -x test --parallel


# app
FROM openjdk:17

WORKDIR /app

COPY --from=builder /build/build/libs/*-SNAPSHOT.jar ./app.jar

ENTRYPOINT ["java","-jar","app.jar"]

EXPOSE 8080
```

이때, builder의 버전을 확인해 주어야 하는데, 이는 `gradle/wrapper/gradle-wrapper.properties` 파일에 있는 `distributionUrl`에서 확인할 수 있다.  

<br>

### 🍄 실습

```
docker build -t [도커허브 ID]/[Repository 이름] .
docker push [도커허브 ID]/[Repository 이름]
```

기존과 똑같이 build 후 push해주었다.  
기존과 달라진 점은 Dockerfile에서 환경을 만들어주기 때문에, `bootJar`를 실행시켜줄 필요는 없다.  

```
docker run -d -i -p 8080:8080 [도커 허브 ID/이미지 이름]
```

이전과 같이 잘 작동하는 것을 볼 수 있다.  

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁