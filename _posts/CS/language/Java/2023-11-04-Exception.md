---
title:  "[Java] ☕ Exception"
excerpt: "JAVA CS 지식 관련 정리"
categories:
  - Java
tags:
  - [JUnit, CS, Java]

toc: true
toc_sticky: true
 
date: 2023-11-04
last_modified_at: 2023-11-04
---


## 📖 예외 처리

자바에서 예외처리는 try-catch를 통한 바로 처리와, throws를 통해서 상속받는 함수에게 넘기는 방법 2가지가 존재한다.  

### 🍄 try-catch, throw

```java
try{
  // 예외가 일어날 만한 코드
} catch(Exception e){
  throw new Exception(); // throw를 통한 원하는 예외 발생 코드
  // 예외 처리 코드
} final{
  // 예외가 발생하든 안하든 무조건 작동하는 코드
}
```

<br>

### 🍄 throws

```java
public void err() throw Exception{ // 에러를 메소드 호출하는 곳에서 처리하도록 에러를 전달한다.
  // 에러발생 가능한 코드
}
```

## 📖 자바의 예외 계층 구조

`RE`를 제외한 `Exception`은 무조건 `throws`나 `try-catch`를 통한 예외처리 코드를 작성해 주어야 한다.  
`RE`는 따로 코드를 작성하지 않아도 되며, `NullPointException`과 같은 오류들이다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/b12829d9-ffa5-46e8-9434-45249a23c89a)


***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁