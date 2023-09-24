---
title:  "[Java] ☕ primitive type and reference type"
excerpt: "JAVA CS 지식 관련 정리"
categories:
  - Java
tags:
  - [CS, Java]

toc: true
toc_sticky: true
 
date: 2023-09-24
last_modified_at: 2023-09-24
---

## 📖 Primitive Type(원시 타입)

기본형 타입으로 사용되기 전에 반드시 선언되어야 한다.  
또한, 객체가 아니므로 null값을 가질 수 없으며, stack 메모리에 직접 값이 저장된다.

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/4153730b-c24b-43fb-855a-833698bf788e)

<br>

## 📖 Reference Type(참조 타입)

Primitive Type을 제외한 모든 타입들로 빈 객체를 의미하는 null이 존재한다.

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/575cb785-fca2-4718-9877-905409236b7b)

<br>

### 🍄 메모리 차이

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/8a889ea3-6bf4-435b-8737-986e1e418630)

reference type이 사용하는 메모리 양이 압도적으로 높다.


 - 가상 컴퓨터에서 돌아가는 실행 프로그램을 위한 이진 표현법이다.
 - 자바 바이트코드는 `JVM`이 이해할 수 있는 언어로 변환된 자바 소스코드로 1바이트로 이루어져 있다.
 - `.class` 파일을 의미한다. 

바이트 코드는 Interpreter 또는 JIT 컴파일러에 의해 바이너리 코드로 변환된다.

<br>

## 📖 배열 선언시 실제 저장 방법

Primitive type시 stack 메모리에 직접 값이 저장되고, reference type 시 heap에 저장이 된다.  
Reference type시 heap 메모리에 직접 값이 저장되며, stack영역의 실제 객체들의 주소를 저장한다.  

### 🍄 1차원 배열

다음과 같이 stack 영역에는 주소가 저장되며, heap 영역에는 실제 값이 들어간다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/9372ad13-a9d9-4b53-9208-ab8b33b82452)

<br>

### 🍄 2차원 배열

heap 영역에는 주소를 저장하는 영역과 실제 값이 저장하는 부분이 나누어져 존재한다. 

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/4370d2f0-34f6-4eeb-bfc3-71fe37e9c9e2)

[출처](https://www.notion.so/2-38b5d67c7f5a48238529bb8f1617ea0d)

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁