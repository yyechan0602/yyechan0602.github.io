---
title:  "Bounce Game 4"
excerpt: "간단한 미니게임을 만들고 실행해보자"

categories:
  - Unity
tags:
  - [Unity, Bounce, Game]

toc: true
toc_sticky: true
 
date: 2023-01-18
last_modified_at: 2023-01-18
---

## 1. UI 구현하기

`Hierarchy`에서 `create -> UI -> Canvas`를 만든다.
`UI`의 `Button`을 생성해준뒤 `Option Button`이라는 이름으로 바꿔준다.
`Panel`을 생성해준뒤 `Option`이라는 이름으로 바꿔주고, `Option`아래에 `Button`을 4개 만든후 이름을 각각 `Play`, `Sound_On`, `Sound_Off`, `Menu`로 바꿔준다. 이때 `Sound` 버튼 두개는 서로 겹쳐 놓는다.
이후 버튼별 자신이 원하는 `Asset`을 넣어준뒤, Panel에는 적당한 색상을 넣어주고, 크기 조절을 한다.

그러자 다음과 같이 구현되었다.

![image](https://user-images.githubusercontent.com/37824506/213097946-24eeb8fa-01ac-4ec6-b2d1-010d57380faa.png)

이후 `Canvas`의 자식으로 `UI_Manager`라는 이름으로 `Empty` 오브젝트를 만든후 `UI_Manager`라는 스크립트를 만들어서 넣어준다.

스크립트 안에 다음과 같은 코드를 넣어준다.  

    public GameObject option_Button;
    public GameObject option;
    public GameObject sound_On;
    public GameObject sound_Off;

    public void Pause()
    {
        option_Button.SetActive(false);
        option.SetActive(true);
    }
    public void Begin()
    {
        option_Button.SetActive(true);
        option.SetActive(false);
    }

    public void Sound_On()
    {
        sound_On.SetActive(false);
        sound_Off.SetActive(true);
    }
    public void Sound_Off()
    {
        sound_On.SetActive(true);
        sound_Off.SetActive(false); 
    }

    public void MainMenu()
    {

    }

각각에 버튼에 다음과 같이 함수를 배정해주면 된다.

![playbutton](https://user-images.githubusercontent.com/37824506/213099113-a0f24ebe-77b8-4b7e-95ac-2835e93b6159.gif)

이후 `Sound_Off` 오브젝트의 `inspector`에 있는 이름 옆의 버튼을 눌러서 비활성화 시킨 후에, `Option`비활성화를 시키고 게임을 작동시킬 시 다음과 같이 잘 작동된다.

![option](https://user-images.githubusercontent.com/37824506/213099798-d82a1c79-17cb-4f9a-8c27-4b2ebae3ee09.gif)

<br>

## 2. MainMenu 구현하기



<br>


***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.