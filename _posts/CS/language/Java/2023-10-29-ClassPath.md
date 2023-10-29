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

## 📖 ClassPath

클래스패스란 클래스를 찾기 위한 경로로써, JVM이 프로그램을 실행할 떄, 클래스파일을 찾는데 기준이 되는 파일 경로를 의미한다.  
java runtime은 이 classpath에 지정된 경로를 모두 검색해서 특정 클래스에 대한 코드가 포함된 `.class` 파일을 찾는다.  
`set classpath`를 통해서 직접 설정해줘도 되고, 파일별로 다음의 classPath로 설정해줘도 된다.  

<br>

### 🍄 ClassPath 옵션

컴파일시 파일 경로를 직접 지정해주는 방법이다.  
`javac -classpath {클래스파일이 있는 디렉토리} {외부 라이브러리}`
그냥 실행시 현재 디렉토리가 기본 클래스패스로 지정된다.  

<br>

## 📖 접근 지시자

접근지정자(Access modifier)은 클래스의 외부에서 접근할 수 있는 범위를 지정하는 방법이다.  
이 접근지시자들을 사용하여 객체 지향 프로그램밍의 캡슐화를 구현할 수 있다.  
특히, 클래스의 변수를 `private`을 사용하여 직접 접근을 막고, `get/set` 메소드를 이용하여 무결성 유지 및 오류 방지를 할 수 있다.  

- public
  - 모든 패키지에서 접근이 가능
- protected
  - 같은 패키지에서 접근이 가능
  - 상속을 받은 클래스 내부에서도 사용 가능
- defualt(package private)
  - 같은 패키지 내에서만 접근이 가능
- private
  - 동일 클래스에서만 접근 가능



<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁