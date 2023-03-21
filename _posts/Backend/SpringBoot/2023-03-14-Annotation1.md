---
title:  "[SpringBoot] 💡 @Annotation? 이란 무엇인가"
excerpt: "Intellj와 PostMan을 사용하여 PostMapping을 통한 데이터 송수신에 대해서 알아보자"
categories:
  - SpringBoot
tags:
  - [JSON, PostMapping, SpringBoot]

toc: true
toc_sticky: true
 
date: 2023-03-14
last_modified_at: 2023-03-17
---

## 📘  @Annotation 이란?

사전상으로는 단순히 `주석`이란 뜻이다.  
하지만 `Annotation`은 단순히 주석의 기능이 아니라, 자바 프로그래밍 언어에서 소스 코드에 추가하여 컴파일러나 런타임에서 사용될 수 있는 메타데이터의 형태를 가진 것이다.  
어노테이션은 컴파일러나 런타임에서 사용되는 정보를 제공하기 때문에, 코드의 가독성과 유지보수성을 높여주는 역할을 한다.  
`Spring`에서는 해당 `Annotation`을 보고 Spring의 `Bean`으로 추가한다.  

<br>

### 📌@Override 

어노테이션은 @ 기호를 사용하여 작성하며, 클래스, 메서드, 변수 등 다양한 요소에 적용할 수 있다.  
`@Override` `Annotation`은 메서드가 상속받는 과정에서 상위 클래스나 인터페이스에서 정의된 메서드를 재정의한 것임을 나타내며, 컴파일러가 이를 확인하여 오버라이딩이 제대로 되었는지 검사할 수 있습니다.

<br>

### 📌 @Controller

`@Controller`는 **MVC** 모델에서 **C** 에 해당하며, 주로 사용자의 요청을 처리한 후, 지정된 뷰에 모델 객체를 넘겨주는 역할을 한다.
클래스 앞에 `@Controller`를 선언하므로서, `Spring FrameWork`에 해당 클래스가 `Controller`임을 알려준다.  
이를 `DispatherServlet`에 반환한다.

<br>

### 📌 @RestController

`@RestController`는 `Controller`에 `ResponseBody`가 추가된 것이다.  
이는 일반적으로 `Json`의 형태로 객체 데이터를 반환한다.  
`Rest API`를 만들때 주로 사용되며, 객체를 `ResponseEntity`로 감싸서 반환한다.  

<br>

### 📌 @RequestMapping

`Http`의 모든 요청을 받는 어노테이션이다.  
하지만 다른 여러가지 요청을 받기 위해서는 `Annotation`에 별도 설정이 필요하다.  
일반적으로 `URL`을 통해 데이터를 보낼때, 단순히 `HTTP`와 같은 주소로 보여지는 정보만 보내지는 것이 아니라, 그 주소를 통해서 Body, Header, Param 등등의 정보들도 같이 보내지게 된다.  
하지만, 이는 개발자 도구 같은 툴로 데이터를 전부 볼 수 있으므로, 보안과는 아무런 관련이 없다.  

하지만 4.3 이상의 스프링부트에서는 더이상 `@RequestMapping` 을 사용하지 않는다.  
다음과 같이 각 **HTTP** 메서드에 맞는 어노테이션을 사용한다.  

 - @GetMapping
 - @PostMapping
 - @PutMapping
 - @DeleteMapping

아래는 `HTTP`에 담아서 보낼수 있는 여러가지 정보들이다.  

![image](https://user-images.githubusercontent.com/37824506/224936752-2474d838-0ee2-4c95-8bbe-97e43239ca2d.png)


<br>

### 📌 @RequestBody, @ResponseBody

클라이언트에서 서버에 보내는 메세지를 **request** 라고 하고, 서버에서 클라이언트에 보내는 메세지를 **response** 메세지라고 한다.  
이러한 통신을 할 때, 본문에 데이터를 담아서 보내야하는데 이 본문이 <span style="color:red">Body</span>이다.  
요청을 할 때는 **@RequestBody**, 응답을 할 때는** @ResponseBody**에 데이터를 담아서 보내야한다.

<br>

### 📌 @RequestHeader

위에서 말했듯이 `HTTP`에는 여러가지 정보들을 담아서 보낼 수 있다.  
이때, `header`의 정보도 같이 보내는데 이때 `header`의 원하는 데이터를 추출해 내는 `Annotation`이다.  

<br>

### 📌@JsonAutoDetect

`Jackson` 라이브러리에 들어있는 `Annotation`의 한 종류로써, 데이터를 전송하거나 받을떄 단순히 `text/html` 같은 문자열이 아닌 `JSON`이나 `XML`의 데이터 형태로 보내고 싶을 때, 데이터 구조를 직렬화 처리 해주는 라이브러리이다.  

<div class="notice--warning" markdown="1">
직렬화와 역직렬화란?

 - 직렬화: 객체를 전송가능한 형태로 말아주는 것
 - 역직렬화: 그 데이터를 다시 자바 객체로 변환해주는 것
</div>

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁