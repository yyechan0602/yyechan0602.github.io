---
title:  "[Docker] 🐋 Spring 서버를 Docker로 띄우기"
excerpt: "Docker CS 지식 정리"
categories:
  - Docker
tags:
  - [CS, Docker]

toc: true
toc_sticky: true
 
date: 2024-01-31
last_modified_at: 2024-01-31
---

## 📖 SpringBoot Server

연습을 위하여 간단하게 `demo/hello` API와 get형식의 `demo/demo`를 가지고 있는 `Demo Server`를 올렸다.  

<br>

### 🍄 Controller

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

<br>

### 🍄 DTO

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

<br>

### 🍄 Entity

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

<br>

<details>
<summary>🍄 Repository</summary>
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

### 🍄 Service

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

### 🍄 실습


<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁