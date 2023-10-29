---
title:  "[Java] ☕ ClassPath"
excerpt: "JAVA CS 지식 관련 정리"
categories:
  - Java
tags:
  - [JUnit, CS, Java]

toc: true
toc_sticky: true
 
date: 2023-10-29
last_modified_at: 2023-10-29
---


## 📖 Package

패키지란 자바 클래스를 모아놓은 디렉토리이다.  
패키지를 사용하는 이유는 클래스명의 고유성을 보장하기 위해서인데, 이를 통해서 같은 이름의 클래스라도 다른 패키지에 있어서 클래스 이름이 충돌하는 것을 방지할 수 있다.  

```java
package School

public class Student{

}
```

<br>

## 📖 import

`import`는 자바 패키지내에 있는 다른 클래스를 불러오는 키워드이다.  
다음과 같은 방식으로 사용이 가능하다.  

```java
import java.util.*;
```

하지만, `*`을 사용한다는 의미는 하위 패키지의 모든 클래스를 포함한다는 것은 아니다.  

<br>

### 🍄 import static

자바에서 `import static` 이라는 생소한 문법도 제공한다.  
이는 기본적으로 다른 패키지의 메소드를 부르기 위해서는 그 `패키지명.메소드` 와 같은 식으로 처리해야 한다.  
하지만 위 방법을 통해서 바로 메소드를 사용가능하다.  

```java
System.out.println(Math.abs(-3));

System.out.println(abs(-3));

```


<br>

### 🍄 테스트



***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁