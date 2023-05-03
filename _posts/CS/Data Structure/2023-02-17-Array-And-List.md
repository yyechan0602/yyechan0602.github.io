---
title:  "[Data Structure][자바] 📂 배열과 리스트 (Priority Queue & Heap)"
excerpt: "제한된 공간과 시간안에서 어떻게 데이터를 처리할지에 대한 알고리즘을 알아보자"
categories:
  - Data Structure
tags:
  - [배열, 리스트, Priority Queue, Heap, Data Structure, 자료구조]

toc: true
toc_sticky: true
 
date: 2023-02-17
last_modified_at: 2023-02-17
---

<br>

## 📘 배열이란?

배열이란 연관된 여러개의 데이터들을 한번에 관리하기 위한 정적 자료구조이다.  
배열을 선언하여 하나의 변수에 여러가지 int, String 뿐만 아니라 Class도 하위 요소로써 가질 수 있다.  
다음과 같이 일정한 주소값과 안에 들어가는 **value** 값으로 이루어져 있다.  

![image](https://user-images.githubusercontent.com/37824506/219529248-8a13575b-14a6-45c8-aa4d-44bce1df7cad.png)

자바에서 배열 선언을 위해서는 다음과 같은 방식을 사용한다.  

```java
int[] arr = new int[100];
String[] strArr = { "Hello", "World", "1" };
```

<br>

## 📖 리스트란?

리스트란 배열과 비슷하지만 동적 자료구조이다.  
동적 자료구조란 미리 정해진 배열의 크기를 정해놓고, 데이터를 넣는 것이 아니라 List를 사용할 때마다 List의 크기를 동적으로 할당하여 늘려나가는 방식이다.  
배열과 비슷하게 다음과 같이 일정한 주소값과 안에 들어있는 **value** 값으로 이루어져 있다.  

![image](https://user-images.githubusercontent.com/37824506/219529288-cc22837e-0879-4c94-a297-b37cf27d9289.png)

자바에서 리스트 선언을 위해서는 다음과 같은 방식을 사용한다.  

```java
Arraylist<Integer> list = new ArrayList<Integer>();
```

<br>

## 📖 배열과 리스트의 차이점

배열과 리스트의 가장 큰 차이점으로는 **동적할당**과 **정적할당**의 차이가 있다.  
다음 그림과 같이 배열은 이미 선언해놓은 배열 크기이상으로 값을 추가할 수 없지만, 리스트는 동적할당이므로 다음과 같이 선언이 가능하다.  
하지만 일반적으로 리스트가 배열보다 시간과 공간적인 측면에서 비효율적이므로 동적할당이 필요없는 크기가 정해져있는 프로그램같은 경우는 배열을 쓰는 것이 오히려 공간적인 부분에서 효율적일 수 있다.  

![image](https://user-images.githubusercontent.com/37824506/219530517-6ae0c8ad-8563-4f97-9f46-d2f9362e9608.png)

<br>

## 📖 정렬과 탐색  


```java
 // 배열 정렬하기 (오름차순 / 내림차순)
Arrays.sort(arr);
Arrays.sort(arr, Arrays.reverseOrder());
 
 // 리스트 정렬하기 (오름차순 / 내림차순)
Collections.sort(list)
Collections.sort(list, Collections.reverseOrder())
```

만약 자신이 만든 클래스 타입의 배열이나 리스트를 정렬하고 싶으면 클래스 안에 다음과 같은 인터페이스를 구현해주면 된다.

```java
class ClassName implements Comparable{
  int value;

  public int compareTo(Object o){
    return this.value - o.value;
  }
}
```  


```java
int value = Arrays.binarySearch(arr, 33);
```

<br>

## 🔗 관련 예시


tag:Array  
tag:List


<br>


***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁