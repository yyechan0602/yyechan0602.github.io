---
title:  "[Java] ☕ 클래스의 상속"
excerpt: "JAVA CS 지식 관련 정리"
categories:
  - Java
tags:
  - [JUnit, CS, Java]

toc: true
toc_sticky: true
 
date: 2023-10-14
last_modified_at: 2023-10-14
---

자바 상속의 특징
super 키워드
메소드 오버라이딩
다이나믹 메소드 디스패치 (Dynamic Method Dispatch)
추상 클래스
final 키워드
Object 클래스

## 📖 상속 (inheritance)

상속이란 자식 클래스가 부모 클래스의 기능을 그대로 물려받아서 사용할 수 있는 것을 의미한다.  
`상속`과 `인터페이스(Interface)는` 비슷해 보이나 다르다.  
`상속은` 부모클래스의 메서드를 전부 `Override` 할 필요는 없고, 다중 상속이 불가능하지만, `Interface`는 반드시 구현해야 하며, 다중 상속이 가능하다. 

- 단일상속이 원칙이며 다중상속이 불가능하다.
- 모든 클래스는 Object() 클래스를 자동으로 상속받게 되어있다.  


### 🍄 상속의 구조

```java
class A{
	private String name; // 자식 클래스에서 바로 접근이 불가능하다.
	
	public A(String name) {
        this.name = name;
		System.out.println("수퍼클래스 생성자");
	}

	public String getName() {
		return name;
	}
}

public class B extends A { //모든 클래스는 오브젝트를 상속받고 있다.
		int age;
		
		public B(String str, int age) {
			super(str); // 부모클래스의 생성자를 호출한다. 
			this.age = age;
			System.out.println("서브클래스 생성자");
		}
		
		public static void main(String[] args) {
				B b = new B("superman",1000);
				System.out.println(b.getName()); //상속 받았기 때문에 부모의 메서드를 사용할 수 있다.
				System.out.println(b.getA());
	}
}
```

이때, `super()` 변수는 부모의 클래스를 호출하는 역할을 한다.  

<br>

## 📖 메소드 오버라이딩

부모 클래스에서 상속받은 메소드를 다른 방식으로 사용하고 싶을 때 사용한다.  

```java
package org.example.functions;

public class Main {
    public static void main(String[] args) {

        Parent parent = new Parent();
        Sub sub = new Sub();

        parent.display();
        sub.display();
    }
}


class Parent{
    public void display(){
        System.out.println("이것은 부모이다");
    }
}

class Sub extends Parent{
    @Override
    public void display(){
        System.out.println("이것은 자식이다");
    }
}
```

<br>

## 📖 메서드 디스패치(Method Dispatch)

메서드 디스패치란 어떤 메서드를 호출할지 결정하여 실제로 실행시키는 과정으로 3가지가 존재한다.  


- 정적 메소드 디스패치
- 동적 메소드 디스패치
- 더블 디스패치


<br>

### 🍄 정적 메소드 디스패치

다음과 같이 `a.print()`를 했을 때, 클래스 A의 print가 불릴 것이라는 것을 확실히 알고 있다.  
컴파일러도 역시 이 메소드를 호출하고 실행시켜야 되는 것을 명확하게 알고 있는데, 이를 `정적 메소드 디스패치`라 부른다.

```java
class A{
    public void print(){
        System.out.println("A");
    }
}

public class Test{
      public static void main(String[] args){
             A a = new A();
             A.print();         //hi를 출력 
      }
}
```
<br>

### 🍄 동적 메소드 디스패치

동적 메소드 디스패치는 정적 디스패치와 다르게 컴파일러가 어떤 메소드를 호출해야 되는지 모르는 것을 말한다.  
메소드의 다형성을 보장하기 위하여 존재하는 방법이다.  
런타임 다형성은 멤버 변수에서는 보장되지 않기 때문에, 다음과 같이 `num`을 출력했을시에는 전부 1이 출력된다.  

<div class="notice--warning" markdown="1">
다형성(polymorphism이란?  

 - 객체들의 타입이 다르면 똑같은 메시지가 전달되더라도 서로 다른 동작을 하는 특징
</div>

```java
class A {
    int num = 1;
    void m1() {
        System.out.println("Inside A's m1 method");
    }
}

class B extends A {
    int num = 2;
    void m1() {
        System.out.println("Inside B's m1 method");
    }
}

class C extends A {
    int num = 3;
    void m1() {
        System.out.println("Inside C's m1 method");
    }
}

class Dispatch {
    public static void main(String args[]) {
        A a = new A();
        B b = new B();
        C c = new C();

        A ref;
        ref = a;
        ref.m1();
        System.out.println(ref.num);

        ref = b;
        ref.m1();
        System.out.println(ref.num);

        ref = c;
        ref.m1();
        System.out.println(ref.num);
    }
}
```

<br>

**결과**

```java
Inside A's m1 method
1
Inside B's m1 method
1
Inside C's m1 method
1
```

<br>

## 📖 추상 클래스 (Method Dispatch)

`추상 메소드`란 자식 클래스에서 반드시 오바라이딩해야만 사용할 수 있는 메소드를 의미한다.  
추상 메소드를 하나이상 포함하는 클래스를 가르켜 추상 클래스라 한다.  
오버라이딩을 통해 다형성을 만족시킬 수 있다.  

```java
abstract class Animal{
    abstract void Bark()
}

class Dog extends Animal{
    @Override
    void Bark(){
        System.out.println("baw wow")
    }
}
```

<br>

## 📖 final

final은 변수, 메서드, 클래스에 사용될 수 있다.  
초기값이 저장되면 이것이 최종적인 값이 되어 중간에 수정이 불가능하다.  
주소값을 나타내는 `final` 변수나 객체같은 경우에는 실제 값들의 수정은 가능하다.  
`상수`는 static(공용성) 이면서 final(수정 불가) 이므로 단순 final 하나만으로는 상수라 할 수 없다.  

```java

final static int a = 1; // 값을 변경 가능하다.
final Animal animal = new Animal(); // 새롭게 new를 통해서 초기화가 불가능하다.

final class Studnet{ // 다른 클래스에 상속할 수 없다.
    int a;
}

final class Parent{
    public final void print(){ // 상속은 되나 Overriding으로 재정의가 불가능하다.
        System.out.println("can't Overriding");
    }
}

```

<br>

## 📖 Object

자바에서 클래스 선언시 `extends`를 이용하여 다른 클래스를 상속받지 않으면 암시적으로 `java.lang.Object` 클래스를 상속하게 된다.  

따라서, 다음과 같이 기본적으로 모든 클래스는 `Object`를 가지고 있기 때문에, 다음과 같이 이미 지정한 메소드의 반환타입을 바꾸려 할시 다음과 같은 오류가 발생한다.  


![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/cc4be801-6c2a-47f9-bac4-8eb734f75057)

Object의 메소드는 다음과 같이 구성되어 있다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/e2072e26-d272-4909-b7e8-f7b10d076cdb)

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁