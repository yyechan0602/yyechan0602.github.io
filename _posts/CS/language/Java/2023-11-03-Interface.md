---
title:  "[Java] ☕ 인터페이스 (Interface)"
excerpt: "JAVA CS 지식 관련 정리"
categories:
  - Java
tags:
  - [JUnit, CS, Java]

toc: true
toc_sticky: true
 
date: 2023-11-03
last_modified_at: 2023-11-03
---


## 📖 Interface

인터페이스란 자바 프로그래밍 언어에서 클래스들이 구현해야 하는 동작을 지정하는데 사용하는 추상 자료형으로 일종의 설계도와 유사하다.  
무조건 구현을 통하여 실사용이 가능하며, 인터페이스 자체에는 기능 명시 이외에 어떠한 기능도 없다.  
다음과 같이 클래스 앞에 `interface`를 붙여서 인터페이스를 만들 수 있다.  

```java
public interface RemoteControl{
  int num = 1;

  public void turnOn();
  public void turnOff();
}
```

<br>

## 📖 인터페이스 구현

인터페이스 구현에는 구현클래스와 익명 구현 객체를 통한 두가지 방법이 존재한다.  

### 🍄 구현 클래스

인터페이스는 다른 class에서 `implements`를 통하여 구현할 수 있으며, `Override`를 사용하여 명시가 가능하다.

```java
public class Television implements RemoteControl{
  public void turnOn(){
    // 티비키는 명령들
  }

    public void turnOff(){
    // 티비끄는 명령들
  }

  public void channel(){ // 구현 클래스 메소드
    // 채널 print();
  }
}
```

<br>

### 🍄 익명 구현 객체

일회성의 객체를 위하여 한번만 사용할 때, 다음과 같이 선언한다.  

```java
Arrays.sort(arr, new Comparator<String()>{
  @Override
  public int compare(String s1, String s2){
    if(s1.length == s2.length()){
      return s1.compareTo(s2);
    } else{
      return s1.length() - s2.length();
    }
  }
})
```

<br>

## 📖 인터페이스 레퍼런스를 통한 구현체 사용 방법

```java
public static void main(String args[]){
  RemoteControl tv1 = new Television();
  Television tv2 = new Television();

  tv1.channel(); // 불가능
  tv2.channel(); // 가능
}
```

<br>

## 📖 Interface의 요소

- 상수
  - public static final로 생성되며 생략이 가능하며, 일반 변수는 생성이 불가능하다.  
- 메서드
- default 메소드
  - 초기값을 설정해주는 메서드로 재정의가 가능하다.
- static 메소드
  - static 메소드는 특정 객체에 속하지 않기 때문에, 인터페이스를 구현하는 클래스의 API의 한 부분이 아니다. 
- private 메소드
  - 인터페이스 내에서만 사용이 가능하며, 재정의가 불가능하다.

```java
public interface RemoteControl {

	double IP = 127.0.0.1; //나중에 상수가됨
  int error = -99999;
	
  void turnOn();
  void turnOff();

	//디폴트 메서드
	default void getIP() {
		myMethod(); //private 메서드 사용
	}

	//static메서드
	static void getLocalIP() {
		System.out.print("지금의 아이피 주소는 : ");
		myMethod(); //private static 메서드 사용
	}

	//private 메서드
	private void myMethod() {
		System.out.print("설정되지 않았습니다.");
  }
}
	//private static 메서드
	private static int mystaticMethod() {
		return IP
	}

}
```

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁