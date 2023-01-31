---
title:  "[Algorithm] Greedy 알고리즘"
excerpt: "제한된 공간과 시간안에서 어떻게 데이터를 처리할지에 대한 알고리즘을 알아보자"
categories:
  - Algorithm Lesson 1
tags:
  - [Greedy, 탐욕, Algorithm, Algorithm1]

toc: true
toc_sticky: true
 
date: 2023-01-31
last_modified_at: 2023-01-31
---

## 📘 Greedy Algorithm (탐욕 알고리즘)이란

다음은 `Greedy Algorithm`의 사전적 정의이다.  

탐욕 알고리즘은 최적해를 구하는 데에 사용되는 근사적인 방법으로, 여러 경우 중 하나를 결정해야 할 때마다 그 순간에 최적이라고 생각되는 것을 선택해 나가는 방식으로 진행하여 최종적인 해답에 도달한다.
{: .notice} 

`Greedy` 즉 탐욕스럽게 바로 앞의 상황만 보는 알고리즘이다.  
즉, `Greedy Algorithm`이란 매 부분의 최적해를 찾아서 결론을 도출하는 알고리즘이다.  
하지만 1차, 2차함수를 제외한 다른 함수들은 극값이 곧 최대/최소값이 아니듯, 그리드 알고리즘으로 나온 결과값도 항상 그 문제의 최적해는 아니다.  

따라서 `Greedy Algorithm`이 잘 작동하기 위해서는 다음 두가지 특징을 따라야한다.

 - `Greedy choice property`
 - `Optimal substructure`

<br>

### 📌 Greedy Choice Property

각 부분에서의 최적해가 결국 최종 답을 구하기 위한 최적해인 경우

### 📌 Optimal Substructure

문제에 대한 최적해가 하위 문제에 대한 최적해를 포함하는 경우

<br>

![image](https://user-images.githubusercontent.com/37824506/215640395-ece44c6e-41bc-4f24-89cd-887b6e87bef9.png)

위의 그림에서와 같이 a값에서 시작한후 가장 y값이 높은 곳을 찾을때, 기울기가 가장 가파른 왼쪽으로 간다면 결국에는 최종적으로는 가장 높은 y값을 얻을 수 없게된다.  

따라서, `Greed Algorithm`을 사용하기 위해서는 이 알고리즘으로 해결이 되는 문제인지 검토해 보는 것이 중요하다.

<br>

## 📖 관련 예시


tag:Greedy



<br>


***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁