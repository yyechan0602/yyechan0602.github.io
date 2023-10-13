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

## 📖 클래스, 객체, 인스턴스의 개념

대부분의 시스템이 OOP(객체지향 프로그래밍)으로 구현 되는데 이는 유지보수성을 높이기 위해서이다.  
이때, 등장하는 3가지 개념이 다음과 같다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/e5e4aebd-a9e8-44a5-a583-eaa8b12191e9)


### 🍄 클래스(Class)란?

- 객체를 생성하기 위한 일종의 `설계도`이다.
- 속성(변수, 필드)과 동작(메서드)으로 이루어져 있다.
- Java를 실행시 클래스는 JVM 메모리의 클래스 영역에 로드된다.

<br>

### 🍄 객체(Object)란?

- 클래스에 선언된 모양 그대로 실체로 구현된 실체이다.
- oop의 관점에서 클래스의 타입으로 선언되었을 때, 객체라고 할 수 있다.

<br>

### 🍄 인스턴스(Instance)란?

- 설계도를 바탕으로 소프트웨어 세계로 구현된 구체적인 실체
- 인스턴스는 `객체`에 포함된다.
- 실체화된 인스턴스는 메모리에 할당된다.
- 인스턴스는 어떤 원본(추상적인 개념)으로부터 생성된 `복제품`을 의미한다.

DB에서는 Schema->instance

<br>

## 📖 클래스의 구조

```java
class Student {  // 클래스 선언
    String name;
    int age;

    public Student(String name, int parameterAge) { // 생성자
        this.name = name; 
        age = parameterAge; // 매개변수와 다르면 this를 안붙여도 된다.
    }

    public Student(String name){ 
        this(name, 15); // this()를 사용하여 같은 클래스의 다른 생성자 호출이 가능하다.
    }

    public int getAge(){ // 메소드
        return age;
    }
}

public class Main {
    public static void main(String[] args) {
        Student student = new Student("홍길동"); // new를 사용하여 객체 생성 후 초기화해준다.
    }
}
```

<br>

### 🍄 new의 역할?

- new는 객체를 위한 heap메모리를 할당함과 동시에 메모리 주소를 반환받는다.  
- 객체의 생성자를 호출하고 생성자는 객체 생성을 위한 클래스의 이름를 제공한다.  

<span style="color:red">**new 키워드는 객체를 생성한다.** </span>  

- reference type : 선언 -> 할당  
- primitive type : 할당  

위와 같이 객체는 선언 후 할당의 과정을 거친다.  
따라서, 모든 `reference type` 객체들은 전부 new 키워드를 사용하기 전에 선언만으로도 메모리상에 존재하게 된다.  
`Integer num;`을 선언하는 순간 Stack영역에 `null`이라는 주소값을 가르키는 `num`변수가 생성되게 된다.  
이때, new를 통해서 heap 영역에 실제 데이터를 저장하며 메모리를 할당하고, 이 주소값 위치를 `num`의 주소값에 저장하게 된다.  
따라서 `reference type`들은 `null`값을 할당하여도 문제가 없는 것이다.  

반면 `int num;`은 변수이므로 `할당`이라는 과정이 무조건 있어야지 메모리에 정상적으로 올라간다.  
따라서 `int num = null`은 존재할 수가 없다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/e8db026e-6efc-49b0-954b-0c20e8db5a9a)

<br>

## 📖 객체에 대한 고찰


<details>
<summary>Student student; 는 객체인가</summary>
<div markdown="1">  

<details>
<summary>만약 Student student가 객체가 아니라면 Student student=null; 는 객체인가</summary>
<div markdown="1">
 
<br>

<span style="color:red">**둘다 객체이다.** </span>  

첫번째 경우는 객체를 선언한 후 초기화를 하지 않은 경우이고, 두번째, 경우는 객체 선언후 초기화를 해 준 경우이다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/637f961b-3c28-49a5-bb13-fbacad3b84bf)

위와 같이 첫 번째는 객체이지만 초기화를 하지 않아서 정상적으로 작동하지 않는 모습이고, 두 번째는 null로 초기화가 되어있기 때문에 제대로 작동하는 모습이다.  

</div>
</details>

</div>
</details>

<!--

-->

<br>

<details>
<summary>int a = null; 은 실제로 가능한가?</summary>
<div markdown="1">

<details>
<summary> null은 객체인가? </summary>
<div markdown="1">

<br>

Java에서 공참조(힙에 실제로 참조되는 object가 없는 참조)의 경우는 당연히 객체가 붙어 있지 않다. 그러나, Java API 레퍼런스의 NullPointerException 항에는 다음과 같이 기술되어 있다.

"object가 필요한 경우 application이 null을 사용하려고 하면 throw된다. 가령 다음과 같은 경우이다."
null object의 instance method 호출
null object의 field(member variables)에 대한 액세스 또는 그 값의 변경
null의 길이를 배열처럼 취득할 경우
null의 slot을 배열처럼 액세스 또는 수정
null을 Throwable처럼 throw 할 경우

위에서 null object라는 말이 등장하는데 이는 공참조에 객체가 붙어 있지 않은 것이 아니라 null을 가리키는 객체라고 볼수 있다. 즉, 공참조라는 것은 JVM에서 봤을때 아무것도 참조하지 않는것이 아니라 null이라고 하는 object를 참조하고 있는것이다. 그러나 JSL 4.3.1에서는 다음과 같이 나와있다.

"참조값(reference)은 이러한 객체의 포인터나 어떤 객체도 참조하지 않는 특수한 null참조가 된다"

즉, 공참조는 어떤 객체도 참조하지 않는다고 단정하고 있다. 하지만 '==' 연산에 있어 두개의 객체가 모두 null이거나 동일한 객체 또는 배열 참조의 경우 true라고 되어있는것으로 봐서 서로 다른 두 객체가 동일한 null을 참조하고 있으므로 true가 된것이 아닌가 하는 생각을 할 수 있다.

즉, null이 Object의 instance 형태는 아니지만 개념적으로 봤을때 null도 object라고 봐야 하지 않을까?

[출처](https://cosmosnet.tistory.com/entry/%EA%B0%9C%EB%B0%9C%EC%9E%90%EA%B0%80-%EB%86%93%EC%B9%98%EA%B8%B0-%EC%89%AC%EC%9A%B4-%EC%9E%90%EB%B0%94%EC%9D%98-%EA%B8%B0%EB%B3%B8%EC%9B%90%EB%A6%AC)

</div>
</details>

</div>
</details>


<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁