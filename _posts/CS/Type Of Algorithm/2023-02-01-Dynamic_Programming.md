---
title:  "[Algorithm] 📈 DP 알고리즘"
excerpt: "제한된 공간과 시간안에서 어떻게 데이터를 처리할지에 대한 알고리즘을 알아보자"
categories:
  - Type Of Algorithm
tags:
  - [DP, 동적 계획법, Dynamic Programming, Algorithm, Algorithm1]

toc: true
toc_sticky: true
 
date: 2023-02-01
last_modified_at: 2023-02-01
---

## 📘 DP 알고리즘 (Dynamic Algorithm) 이란

다음은 `Dynamic Algorithm`의 사전적 정의이다.  

복잡한 문제를 간단한 여러 개의 문제로 나누어 푸는 방법을 말한다. 이것은 부분 문제 반복과 최적 부분 구조를 가지고 있는 알고리즘을 일반적인 방법에 비해 더욱 적은 시간 내에 풀 때 사용한다.
{: .notice} 

일반적으로 재귀를 통해 풀 수 있는 문제의 시간복잡도는 O(n^2)이다.  
하지만 다음 그림과 같이 재귀는 여러가지 겹치는 동일한 연산들이 발생한다.  
이를 DP알고리즘을 통해 개선하면 O(f(n))정도로 개선이 가능하다.  

![image](https://user-images.githubusercontent.com/37824506/215921835-44ca02f1-4eba-42a9-8069-1f8900e451fd.png)

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