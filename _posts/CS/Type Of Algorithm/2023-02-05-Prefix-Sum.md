---
title:  "[Algorithm] 📈 누적 합 (Prefix Sum)"
excerpt: "제한된 공간과 시간안에서 어떻게 데이터를 처리할지에 대한 알고리즘을 알아보자"
categories:
  - Type Of Algorithm
tags:
  - [누적합, Prefix Sum, Algorithm, Algorithm1]

toc: true
toc_sticky: true
 
date: 2023-02-05
last_modified_at: 2023-02-05
---

## 📘 합을 구하는 법

`5, 4, 3, 2, 1` 의 5가지 값이 들어오고, `1-3`까지의 합을 구하는 방법은 다음과 같다.  
다음과 같이 들어온 값을 배열에 넣은 후, `1, 2, 3`의 주소에 있는 `5, 4, 3`을 더해주면 된다.

![image](https://user-images.githubusercontent.com/37824506/216810152-51b6ccc1-d7b0-4142-afd7-101b5be6abce.png)

하지만 이와 같은 경우는 `1-3`의 합, `1-5`의 합, `1-4`까지의 합을 계산후 `print`시킬시, `for문`이 3, 4, 5번 돌게 된다.  
따라서 N개의 숫자와 N번의 계산을 구하는 문제가 나왔을 시, 최악의 경우 `O(n^2)`의 시간복잡도가 되게 된다.

<br>

## 📖 누적 합 (Prefix Sum)

이를 해결하기 위해 등장한 개념이 바로 누적 합(Prefix Sum)이다.  
`Prefix Sum`말 그대로 미리 `Sum`을 한다는 뜻이다.  

개념은 매우 간단하다.  
처음에 배열에 값을 넣을 때, 바로 넣지 않고, 받은값과 이전값을 합쳐서 배열에 넣는다.  
따라서 `5, 4, 3, 2, 1`이라는 값이 들어왔을 때, 다음과 같이 값이 저장되게 된다.

![image](https://user-images.githubusercontent.com/37824506/216810182-a732cbbc-9b2a-4a78-9105-bc3087fc9090.png)

이중 `1-3`을 구하려면 단순하게 `3`의 주소값의 값에서 `1`보다 이전 주소값 하지만 없으므로, 즉 0을 빼면 된다.  

이렇게 누적합을 사용하므로써 위에서의 `o(n^2)`이라는 끔찍한 속도에서 `o(n)`으로 현저히 빨라지게 된다.  

<br>

## 🔗 관련 예시


tag:Prefix Sum


<br>


***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁