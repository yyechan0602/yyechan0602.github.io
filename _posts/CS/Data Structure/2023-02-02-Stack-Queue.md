---
title:  "[Data Structure] 📂 Stack과 Queue"
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

<br>

## 📘 Queue 의 정의

 - `Queue`이란 제한적으로 접근할 수 있는 나열 구조
 - 선입선출 즉, `FIFO` 형식의 자료구조

<br>



## 📘 DP 알고리즘의 사용 조건

 - `Overlapping Subproblems`
 - `Optimal Substructure`

<br>

### 📌 Overlapping Subproblems

돌일한 작은 문제들이 반복하여 나타나는 경우

### 📌 Optimal Substructure

부분 문제의 최적 결과값을 사용해 전체 문제의 최적 결과를 낼 수 있는 경우

<br>


## 📘 구현방법

### 📌 Bottom-Up 방식

재귀함수와 똑같은 방식으로 작동하지만, "Memoization"을 활용하여, 이전에 계산한 값을 다시 반복하는 것이 아니라 단순히 가져오는 방식으로 처리함으로써, 시간복잡도를 줄이는 방식이다.  

### 📌 Top-Down 방식

dp[0]부터 dp[n]까지를 점화식을 이용하여, 아래에서부터 위까지 누적하여 전체 큰 문제를 해결하는 방식이다.

### 📌 중요!!!

2가지 방법 중 2가지를 전부 사용하지 못하고, 하나만 사용할 수 있는 문제도 존재한다.  
따라서 여러가지 문제를 다각도로 풀어보는 경험이 중요하다.


<br>

## 📖 관련 예시


tag:DP



<br>


***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁