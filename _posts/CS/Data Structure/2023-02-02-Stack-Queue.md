---
title:  "[Data Structure] 📂 Stack과 Queue에 대해서 알아보자"
excerpt: "제한된 공간과 시간안에서 어떻게 데이터를 처리할지에 대한 알고리즘을 알아보자"
categories:
  - Data Structure
tags:
  - [Stack, 스택, Data Structure, 자료구조]

toc: true
toc_sticky: true
 
date: 2023-02-02
last_modified_at: 2023-02-03
---


## 📘 Stack 정의 및 설명

 - `Stack`이란 제한적으로 접근할 수 있는 나열 구조
 - 후입선출 즉, `LIFO` 형식의 자료구조

스택은 객체들의 집합소로서 데이터를 저장하는 구조이다.  
항상 같은 구조와 크기의 자료를 정해진 방향으로만 쌓을 수 있다.  
스택에서 `Top`을 통해 삽입하는 연산을 `PUSH`, `Top`을 통해 삭제하는 연산을 `POP`이라고 한다.

![image](https://user-images.githubusercontent.com/37824506/216577140-b1e95836-6c38-4aa8-b907-011a7a7481e5.png)

<br>

## 📘 Queue 의 정의

 - `Queue`이란 제한적으로 접근할 수 있는 나열 구조
 - 선입선출 즉, `FIFO` 형식의 자료구조

![image](https://user-images.githubusercontent.com/37824506/216576185-14231e7a-d201-474f-b484-4fd69b1bd04f.png)

큐는 객체들의 집합소로써 데이터를 저장하는 구조이다.  
항상 같은 구조와 크기의 자료를 정해진 방향으로만 넣을 수 있다.  
삽입연산이 이루어지는 곳을 `rear`, 삭제연산이 이루어지는 곳을 `front`라고 한다.  
큐에서 `front`를 통해 삽입하는 연산을 `enQueue` 라고 하고, 스택

<br>

## 📖 자바를 통한 구현

자바를 통해 위의 두가지를 구현하고 싶으면 다음 코드를 이용하면 된다.  

```java
    Stack<String> st = new Stack<>();
    Queue<String> que = new LinkedList<>();
```


## 📖 관련 예시


tag:Stack
tag:Queue


<br>


***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁