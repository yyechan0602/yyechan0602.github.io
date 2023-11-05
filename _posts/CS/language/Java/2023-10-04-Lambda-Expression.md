---
title:  "[Java] ☕ 람다식 (Lamda)"
excerpt: "JAVA CS 지식 관련 정리"
categories:
  - Java
tags:
  - [CS, Java]

toc: true
toc_sticky: true
 
date: 2023-10-04
last_modified_at: 2023-10-04
---

## 📖 람다식

`람다 함수 또는 람다식`은 일종의 `익명 함수(Anonymous Functions)`라는 개념이다.  
`익명 클래스(Annoymous Class)'의 함수버전이라고 생각하도 되며, 한번 사용 후 버려지는 함수이다.  

```java
public static void main(String[] args) {
    Comparator<Integer> comp = new Comparator<Integer>() {
        @Override
        public int compare(Integer o1, Integer o2) {
            return o1.compareTo(o2); // o1 은 Integer 이고, Integer 은 Comparable 을 구현하고,
        }	 // Comparable 에 compareTo 메서드가 있다.
    };
    System.out.println(comp.compare(2, 1));
}
```

```java
public static void main(String[] args) {
    Comparator<Integer> comp = (o1, o2) -> (o1.compareTo(o2));

    System.out.println(comp.compare(2, 1));
}
```

## 📖 익명 구현 클래스 vs 람다식




<br>

## 📖 switch 연산자  

기존 `case:`를 대체하여 `->`를 사용한다.

```java
public class MyClass {
	
	public static void main(String[] args) {
		MyClass myclass = new MyClass();
		myclass.switchExample(Day.TUE); // TUE Day
		myclass.switchExample(Day.SUN); // SUN Day
	}
	
	void switchExample(Day day) {
		switch (day) {
			case MON, TUE -> System.out.println(Day.MON + " Day");
			case SUN -> System.out.println(Day.SUN + " Day");
      default -> {
        yield -1;
      }
		}
	}
	
	enum Day {
		MON, TUE, WED, THUR, FRI, SAT, SUN
	}
}
```

<br>

## 📖 3항 연산자

3항 연산자로 변수나 함수에 값을 if문 없이 바로 넣을 수 있다.

```java
String str1 = "b가 더 크거나 같다";
if(a>b){
  str="a가 더크다"
} 

String str2 = a > b ? "a가 더크다" : "b가 더 크거나 같다";
```

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁