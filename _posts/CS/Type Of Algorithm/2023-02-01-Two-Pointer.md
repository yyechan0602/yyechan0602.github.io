---
title:  "[Algorithm] 📈 Two Pointer 알고리즘"
excerpt: "제한된 공간과 시간안에서 어떻게 데이터를 처리할지에 대한 알고리즘을 알아보자"
categories:
  - Type Of Algorithm
tags:
  - [Two Pointer, Dynamic Programming, Algorithm, Algorithm1]

toc: true
toc_sticky: true
 
date: 2023-02-01
last_modified_at: 2023-02-03
---

## 📘 Two Pointer 알고리즘이란

다음은 `Two Pointer`의 사전적 정의이다.  

두 개의 포인터를 사용해 문제를 해결하는 알고리즘
{: .notice} 

투 포인터 알고리즘은 리스트나 배열에 접근할 때, 2개의 포인터의 위치를 기록하면서 처리하느 알고리즘이다.  
보통 `S(Start)`, `E(End)`와 같은 방식으로 이름을 붙인다.  

다음은 `Two Pointer`와 관련된 간단한 예시이다.  

<br>

## 📘 Two Pointer 예시

`Two Pointer`와 관련된 간단한 문제를 알아보자

<br>

다음과 같이 5개의 재료를 주고, 차가 2라고 하자.  
단순하게 이것을 뽑아내기 위해서는 처음 5와 나머지 4개를 비교한 후, 2도 나머지와 비교하는 완전 탐색을 해야한다.  

![image](https://user-images.githubusercontent.com/37824506/216514383-88345250-42ac-4c83-8431-d7146119e4a2.png)

하지만 이 배열을 다음과 같이 정렬을 한 후, `S`의 값을 증가시키면서 차가 2가 될 때까지 증가시킨다.  

![image](https://user-images.githubusercontent.com/37824506/216513146-d8475920-eea9-488b-a11e-6820f65e623c.png)

![image](https://user-images.githubusercontent.com/37824506/216532893-352f0a55-0f71-4f44-9872-d0500d555368.png)

![image](https://user-images.githubusercontent.com/37824506/216533028-79bca0f6-cbf9-4204-94f1-fddc9f63ebe8.png)

이후 차가 2보다 커지면 `E`의 값을 증가시킨다.  

![image](https://user-images.githubusercontent.com/37824506/216533186-3bb6da69-7654-4ded-bd98-7160d817f55b.png)

이후 다시 2가되면 이를 반복하면서 찾아내는 방식이다.  

<br>

이러한 `Two Pointer`방식은 `S`가 처음부터 끝까지, `E`가 처음부터 끝까지 가는 알고리즘이므로 `완전탐색`의 O(n^2)에 비해 O(2n)정도로 매우 줄어들게 된다.  

<br>

## 📖 관련 예시


tag:Two Pointer


<br>


***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁