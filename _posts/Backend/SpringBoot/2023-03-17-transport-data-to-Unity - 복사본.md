---
title:  "[SpringBoot] 💡 JSON을 이용한 데이터 송수신?"
excerpt: "Intellj와 PostMan을 사용하여 PostMapping을 통한 데이터 송수신에 대해서 알아보자"
categories:
  - SpringBoot
tags:
  - [JSON, PostMapping, SpringBoot]

toc: true
toc_sticky: true
 
date: 2023-03-14
last_modified_at: 2023-03-14
---

## 📘 사전준비

`postMan`이라는 API를 디자인하고 빌드하고 테스트하기 위한 API 플랫폼을 깔아준다.  

다음으로 `IntelliJ` 를 설치해준다.  
이후 `Spring initializr`를 이용하여 새 프로젝트를 생성해준다.  

![image](https://user-images.githubusercontent.com/37824506/224937618-df6dff3b-d664-403b-9e85-ecff2cbe09de.png)

이때 다음과 같이 `Spring Boot DevTools`, `Lombok`과 `Spring Web`을 체크해준다.  

![image](https://user-images.githubusercontent.com/37824506/224937722-7de21c4d-f248-4135-a333-c1d4194dcfcd.png)

이후, [유니티 설치 방법](https://yyechan0602.github.io/unity1/Unity-Install/) 에 있는 방법을 따라서, 유니티를 설치한다.

<br>

## 📘 PostMapping을 사용하기

다음과 같이 `main/java/com.example.(파일이름)` 아래에 `Controller`라는 패키지를 만들고, 그 폴더 안에 `PostController`라는 이름으로 자바 스크립트를 하나 생성해준다. 

![image](https://user-images.githubusercontent.com/37824506/225908638-6ff0fd81-832a-40a1-8b47-3daf91c8d20b.png)

이후 안에 다음과 같이 코드를 작성해준다.  


```java
package com.example.imsgame.Controller;

import com.fasterxml.jackson.annotation.JsonAutoDetect;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestHeader;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class asd {

    @PostMapping("/postMethod")
    public ResponseEntity<String> processData(@RequestBody UnityData unityData, @RequestHeader("Content-Type") String contentType) {
        if ("application/json".equals(contentType)) {
            String result = "수신된 데이터: " + unityData.toString();
            return ResponseEntity.ok(result);
        } else {
            return ResponseEntity.badRequest().body("Invalid Content-Type");
        }
    }

    @JsonAutoDetect
    public static class UnityData {
        private String id;
        private String password;

        public UnityData(String id, String password) {
            this.id = id;
            this.password = password;
        }

        public String getId() {
            return id;
        }

        public String getPassword() {
            return password;
        }

        public void setId(String id) {
            this.id = id;
        }

        public void setPassword(String password) {
            this.password = password;
        }

        //toString 오버라이드
        @Override
        public String toString() {
            return "유니티 데이터{" +
                    "이름 ='" + id + "'" +
                    ", password =" + password +
                    '}';
        }
    }
}
```

위 코드에서 **@** 라는 특이한 기호가 보인다.  
이는 `Annotation`이고 이는 [Annotation 이란 무엇인가](https://yyechan0602.github.io/springboot/Annotation1/) 에서 확인할 수 있다.  

이때 `ResponseEntity<String> processData()` 함수에서 `/postMethod`라는 주소로 온 데이터에 들어있는 `body`를 파싱해서 처리한다.  
이때 이 받은 데이터를 처리하기 위한 `UnityData`라는 `DTO`를 하나 만들어주고, 안에 `String` 형식으로 `id`와 `password`를 생성해준다.  
여기서 `getter, setter`를 선언해 줘야 하는데, `IntelliJ`에서 이를 지원하는 간단한 명령어가 있다.  
코드를 추가하고 싶은 곳에 커서를 둔 뒤, `alt + insert` 키를 눌러준 후, `getter, setter`를 추가해준다.  

이제 `(파일이름)Application`을 실행시키면 다음 화면과 같이 정상적으로 코드가 작동이 된다.  

![image](https://user-images.githubusercontent.com/37824506/226229393-9ebafc85-746b-443b-a050-011682244e45.png)  

이후 `postMan`에서 형식을 `post`로 변경해준뒤, `http://localhost:8080/postMethod`를 입력해주고, `body` 부분에 `raw` 데이터 형식으로 다음과 같이 입력해준뒤 `Send`를 누르면 이렇게 답변이 오게 된다.

![image](https://user-images.githubusercontent.com/37824506/226229637-5988b691-a3ef-4306-a3fc-0b998e65c0b9.png)

<br>

## 📘 로그인 체크하기  

`postMapping`으로 받아온 데이터가 `UnityData`와 아이디와 비밀번호가 같은지 확인하기 위하여, `UnityData` class 안에 다음 코드를 넣어준다.  

```java
    public boolean isExist() {
        if (id.equals(id2) && password.equals(password2)) {
            return true;
        } else {
            return false;
        }
    }
```

이후 임의로 정한 아이디, 비밀번호를 넣어주고, 받은것과 체크해서 같은지 확인하기 위해 본문을 바꿔준다.  

```java
    final static String id2 = "123";
    final static String password2 = "456";

    @PostMapping("/postMethod")
    public ResponseEntity<String> processData(@RequestBody UnityData unityData, @RequestHeader("Content-Type") String contentType) {
        if ("application/json".equals(contentType)) {
            String result = "수신된 데이터: " + unityData.toString();
            String result2;
            if (unityData.isExist()) {
                System.out.println("맞네");
                result2 = "ok";
            } else {
                System.out.println("틀리네");
                result2 = "no";
            }

            return ResponseEntity.ok(result);
        } else {
            return ResponseEntity.badRequest().body("Invalid Content-Type");
        }
    }
```

<br>

## 📘 Unity 연동하기  

이후 유니티에 들어가서 다음과 같이 `UI`를 만들어준다.

![image](https://user-images.githubusercontent.com/37824506/226274738-43c7744d-e9a9-42de-a98d-cdfbb24ffc07.png)

<br>

이후 아래와 같은 `Script`파일을 만들어준뒤, 설정해주면 `Unity`쪽은 완성된다.  
이 유니티 연동 부분에서 가장 중요한 부분은 유니티에서 보내는 데이터의 변수명과 서버쪽에서 받는 데이터의 변수명이 똑같아야한다.  
이 오류를 찾아내는데 꽤나 시간이 걸렸다.

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using System;
using UnityEngine.Networking;
using System.Text;

public class UI_Manage : MonoBehaviour
{
    public Text id;
    public Text password;
    // Start is called before the first frame update
    void Start()
    {
    }

    // Update is called once per frame
    void Update()
    {
    }

    IEnumerator SendJsonData(){
        MyData data = new MyData();

        data.id = id.text.ToString();
        data.password = password.text.ToString();

        String url = "http://localhost:8080/postMethod"; // 상황에 맞는 api 호출 -> 매핑된 url을 호출한다.
        String json = JsonUtility.ToJson(data);

        UnityWebRequest request = UnityWebRequest.Post(url, json);

        request.SetRequestHeader("Content-Type", "application/json");

        //==============중요============
        byte[] jsonToSend = new UTF8Encoding().GetBytes(json);
        request.uploadHandler = new UploadHandlerRaw(jsonToSend);

        yield return request.SendWebRequest();

        if(request.isNetworkError || request.isHttpError){
            Debug.LogError(request.error);
        }else{
            Debug.Log(request.downloadHandler.text);
        }
    }

    public void OnClick2(){
        Debug.Log(id.text + " " + password.text);
        StartCoroutine(SendJsonData());
    }
}

[System.Serializable]
public class MyData{
    public string id;
    public string password;
}
```

<br>

이후 다음과 같이 틀렸을 떄는 서버쪽에서 틀리다고 하고,

![image](https://user-images.githubusercontent.com/37824506/226275992-04dedea1-249f-4354-a9a5-884b139423ae.png)

옳바르게 했을시, 맞다고 요청이 나오게 된다.

![image](https://user-images.githubusercontent.com/37824506/226276047-49cf36fe-df4d-4fc4-bc4e-9eb9cea1fbae.png)

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁