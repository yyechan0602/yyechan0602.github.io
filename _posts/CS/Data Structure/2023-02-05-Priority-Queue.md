---
title:  "[Data Structure] 📂 우선순위 큐와 힙 (Priority Queue & Heap)"
excerpt: "제한된 공간과 시간안에서 어떻게 데이터를 처리할지에 대한 알고리즘을 알아보자"
categories:
  - Data Structure
tags:
  - [우선순위큐, 힙, Priority Queue, Heap, Data Structure, 자료구조]

toc: true
toc_sticky: true
 
date: 2023-02-13
last_modified_at: 2023-02-16
---

## 📘 우선순위큐(priority Queue)란?

큐는 선입선출(FIFO)구조로써, 먼저 들어온 값이 먼저 나가게 된다.  
따라서 새로운 값이 들어오거나 뺄 때는 단순하게 **o(1)** 의 시간복잡도를 가지지만, 어떤 값이 들어있는지 검사하거나 비교하기 위해서는 `Queue` 의 모든 값들을 일일이 찾아봐야 하기 때문에, **o(n)** 의 시간복잡도를 가지게 된다.  

이를 효과적으로 개선하기 위하여 사용하는 방식이 바로 **우선순위큐(Priority Queue)** 라는 알고리즘이다.  
**우선순위큐(Priority Queue)** 는 일반적으로 `힙(heap)` 이라는 자료구조를 통해서 구현한다.  
다음은 우선순위큐의 시간복잡도를 비교한 표이다.  

![image](https://user-images.githubusercontent.com/37824506/218364641-d9c1cb3b-9a20-479a-adc8-1cbbfa0f0719.png)

<br>

## 📖 힙(heap)이란?

`힙(heap)` 이란 다음과 같다.  

 - 데이터에서 최대값과 최소값을 빠르게 찾기 위해 사용되는 **완전 이진 트리** 형태이다.
 - 힙은 일종의 **반정렬 상태(느슨한 정렬 상태)** 이며 최대힙과 최소힙으로 나누어진다.
 - 최대힙은 자식노드보다 부모노드의 값이 크다.
 - 최소힙은 부모노드보다 자식노드의 값이 크다.
 - **중복을 허용한다.**

![image](https://user-images.githubusercontent.com/37824506/218364297-cc5d3f78-8622-43aa-b532-6fb9cde78af2.png)

최소힙은 루트값이 가장 작은 값을 가지게 되는 트리이다.  
최대힙은 루트값이 가장 큰 값을 가지게 되는 트리이다.  

최소힙을 기준으로 

 - 왼쪽 자식 노드 **index** = 부모노드 **index** / 2
 - 오른쪽 자식 노드 **index** = 부모노드 **index** / 2 + 1
 - 부모 노드 **index** = 부모노드 **index** / 2  

<br>

## 📖 [Java] 우선순위 큐 구현하기

우선순위 큐를 자바에서 구현을 하면 다음과 같이 배열을 통해 구현한다.  
편의상 0을 비워놓고 1부터 차례대로 집어넣는다.  

![image](https://user-images.githubusercontent.com/37824506/218365585-c24f2b9e-8c9f-4e07-8ee7-3065962efea3.png)

 - 왼쪽 자식 노드 **index** = 부모노드 **index** / 2
 - 오른쪽 자식 노드 **index** = 부모노드 **index** / 2 + 1
 - 부모 노드 **index** = 부모노드 **index** / 2  

이를 코드로 나타내면 다음과 같다.  

```java
import java.util.PriorityQueue;
import java.util.Collections;

public class Main {
    public static void main(String[] args) {
        //낮은 숫자가 우선 순위인 int 형 우선순위 큐 선언
        PriorityQueue<Integer> priorityQueueLowest = new PriorityQueue<>();

        //높은 숫자가 우선 순위인 int 형 우선순위 큐 선언
        PriorityQueue<Integer> priorityQueueHighest = new PriorityQueue<>(Collections.reverseOrder());



        // 삽입연산
        // add(value) 메서드의 경우 만약 삽입에 성공하면 true를 반환, 
        // 큐에 여유 공간이 없어 삽입에 실패하면 IllegalStateException을 발생
        priorityQueueLowest.add(1);
        priorityQueueLowest.add(10);
        priorityQueueLowest.offer(100);



        // 삭제연산
        // 첫번째 값을 반환하고 제거 비어있다면 null
        priorityQueueLowest.poll();

        // 첫번째 값 제거 비어있다면 예외 발생
        priorityQueueLowest.remove(); 

        // 첫번째 값을 반환만 하고 제거 하지는 않는다.
        // 큐가 비어있다면 null을 반환
        priorityQueueLowest.peek();

        // 첫번째 값을 반환만 하고 제거 하지는 않는다.
        // 큐가 비어있다면 예외 발생
        priorityQueueLowest.element();

        // 초기화
        priorityQueueLowest.clear();   
    }
```

<br>

## 🔗 관련 예시


tag:Priority Queue


<br>


***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁