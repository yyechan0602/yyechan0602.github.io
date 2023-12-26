---
title:  "[Summary] BufferReader 사용하기"
excerpt: "실력향상을 위한 Java 주요 함수 정리"

categories:
  - Summary
tags:
  - [BufferReader, Java, Coding_Test]

toc: true
toc_sticky: true
 
date: 2023-01-26
last_modified_at: 2023-01-28
---

## 1. Scanner

Java에서 입출력에서 기본적으로 사용하는 함수는 `Scanner`이다.  

다음과 같이 기본적으로 여러개의 형변환을 지원하고, 자동으로 공백과 개행(' ', '\t', '\r', '\n' 등등..)을 기준으로 읽는다.

```
Scanner sc = new Scanner(System.in);

int n = sc.nextInt(); // int
long l = sc.nextLong(); // int
String s = sc.next(); // String
String s = sc.nextLine(); // String
````

하지만 코딩에서 자동으로 여러가지 기능을 지원해주는 함수나 프로그램은 필연적으로 더 느릴 수 밖에 없다.  

`Scanner`를 사용할경우 형변환과 여러기능이 있어서 간단하지만, 내부적으로 여러가지 정규 표현식이 있어서 시간이 오래 걸린다.  

따라서 `BaekJoon`관련 문제를 풀다보면 `Scanner`를 사용하면 도저히 시간초과로 인하여 풀 수 없는 문제가 나타나게 된다.  
이를 해결하기 위하여 코딩테스트를 할 때 필수로 익하여 하는 것이 바로 `BufferReader`와 `BufferWriter`이다.

<br>

## 2. BufferReader/BufferWriter  


`BufferReader`와 `BufferWriter`는 `Buffer`를 사용하여 입출력을 하는 함수이다.  

`BufferReader`는 기본적으로 값을 `String`형태로 가져오고, 어떠한 처리도 해주지 않는다.  
따라서 이를 사용자가 원한는대로 형변환을 직접 해주고, 공백과 개행(' ', '\t', '\r', '\n' 등등..)으로 직접 나눠줘야 한다.  



```
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
```

<br>

또한 기본적으로 `BufferReader`는 `IOException`이라는 예외처리를 발생시킨다.  
이를 해결해주기 위하여 `throws IOException`이나 `try`와 `catch`를 이용하여 예외를 처리해주어야한다.  


<br>

이제 직접 사용해보자.  

다음과 같이 훨씬 복잡해 보이는 코드이지만 실제로 작동해보면 더 빠르게 작동하는 것을 알 수 있다.

```
  public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    BufferedWriter bw = new BufferedWriter(new OutputStreamWriter((System.out)));
    StringTokenizer st  = new StringTokenizer(br.readLine());

    String a = st.nextToken();

    bw.write(a);
    bw.newLine();
    bw.flush();
    bw.close();
    }
```
<br>

위의 코드와 같이 `StringToken`를 사용하여 문자를 넣은 후, `nextToken()`함수를 이용하여 하나씩 가져와 사용이 가능하다.

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁