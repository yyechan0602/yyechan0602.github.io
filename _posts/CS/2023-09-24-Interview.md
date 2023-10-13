---
title:  "[CS Interview] 📈 Interview"
excerpt: "CS 면접 대비용 여러 질문 모음집"
categories:
  - CS Interview
tags:
  - [CS, Glossary]

toc: true
toc_sticky: true
 
date: 2023-09-24
last_modified_at: 2023-09-24
---

## 📖 Java 질문 모음집

<br>

### 1 JVM

<br>

🍄 Java는 플랫폼에 종속적이지 않고 이식성이 뛰어나다.  
그렇다면 JVM은 플랫폼에 종속적이지 않고 이식성이 뛰어난가?  
- 아니다. JVM이 플랫폼에 종속적이기 때문에, `.class`파일이 플랫폼을 신경쓰지 않고 전부 동일할 수 있다.

<br>

🍄 Java가 C나 C++같은 언어보다 느린 이유?  

<br>

🍄 Jit Compiler는 바이트 코드 전체를 컴파일 하여 Native Code로 변환하는데 이때, Native Code는 무엇을 의미하는가?  

<br>

🍄 자바에는 포인터가 없는가?  

<br>

### 2 람다식

<br>

🍄 람다식과 익명 함수는 내부적으로 서로 같은 것인가?  

<br>

### 3 상속

<br>

🍄 int num1 = null;은 불가능하다.  
반면, Integer num2 = null; 은 가능하며 심지어 if(null==num2)와 같은 식으로 비교까지 가능하다.  
왜 이런 것이 가능한 것인지 이와 관련하여 new의 역할이 무엇인지 할당과 선언을 사용하여 설명해라  

- 자바의 데이터 타입은 다음 두가지로 이루어진다.
  - reference type : 선언 -> 할당  
  - primitive type : 할당  
- 이때, reference type은 선언만으로 메모리상에 존재가 가능하지만, primitive type은 할당을 해야지 메모리상에 정상적으로 존재하게 된다.
- 따라서 reference type은 null이라는 객체를 가르키는 null타임이 가능하지만, primitive 타입은 값 그 자체를 할당하는 방식이기 때문에 null이라는 객체를 가르키는 것 자체가 불가능하다.

<br>

🍄 자바에서 모든 클래스는 Object 클래스를 상속받게 되는데, 자바에서는 다중 상속을 막는다.  
그렇다면 Animal을 상속받은 dog 클래스는 Object 클래스를 상속받지 못한 것인가?  

- 상속받은 Animal 클래스 자체가 Object클래스를 상속받은 개념이기 때문에 dog 클래스도 상속받았다고 볼 수 있다.

<br>

🍄 다음 함수는 정상적으로 작동하는가?
```java
class A {
    int num = 1;
    public void toString(){
      System.out.println("hello");
    }
}
```
- 정상적으로 작동하지 않는다.  
- 다음과 같이 Object의 `toString` 함수와 충돌한다.  
![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/cc4be801-6c2a-47f9-bac4-8eb734f75057) 

<br>

🍄 다음 코드는 실행되는가? 만약 실행된다면 결과는 어떻게 나오는가?

```
class ConstructorTest{
    private void ConstructorTest(){
        System.out.println("Constuctor");
    }
}

public class Main {
    public static void main(String[] args) {
        ConstructorTest ct = new ConstructorTest();
    }
}
```

- 싱행은 되나 아무것도 출력되지 않는다.  
- 생성자가 없기 때문에 `Object` 에서 상속받은 기본 생성자로 생성된다.

<br>


***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁