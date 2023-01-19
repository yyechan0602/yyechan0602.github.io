---
title:  "Bounce Game 5"
excerpt: "간단한 미니게임을 만들고 실행해보자"

categories:
  - Unity
tags:
  - [Unity, Bounce, Game]

toc: true
toc_sticky: true
 
date: 2023-01-19
last_modified_at: 2023-01-19
---

## 1. SingleTon 관련 문제

<br>

지금까지 코드를 짠 후 실행을 시키면 다른 `Scene`에서 만든 `SingleTon`을 인식하지 못하는 문제가 발생한다.  
이를 해결하기 위하여 `GameManager`를 사용하는 `Object`들에 다음과 같은 수정을 해주었다.
`GameManager`를 직접 넣어주는 것이 아니라 `Script`상으로 알아서 찾는 식으로 수정을 하여서 다른 `Scene`에서 온 `GameManager`라도 `Tag`가 똑같을 시 찾을 수 있도록 하였다. 이후 모든 `GameManager`오브젝트에 `Tag`로 `GameManager`를 넣는다.

    public GameObject Game_Manager;

    void Start()
    {
        Game_Manager = GameObject.FindGameObjectWithTag("GameManager");
    }

이후 게임 도중에 `MainMenu`로 가기 위하여 `Player` 스크립트와 `UI_Manager`에 `SceneManager.LoadScene("MainMenu");` 코드를 넣어주면 된다.

<br>

## 2. DB 연동하기



<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.