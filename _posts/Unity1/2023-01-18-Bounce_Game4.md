---
title:  "[Bounce Game] 🥎 미니게임 만들기 4"
excerpt: "간단한 미니게임을 만들고 실행해보자"

categories:
  - Unity1
tags:
  - [Unity1, Bounce, Game]

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

## 2. MainMenu Scene 만들기

<br>

다음으로 이전까지 만들었던 `Scene`을 복사하여 `MainMenu`라는 이름으로 바꿔준다. 이후 안에 있는 `GameManager`를 제외하고 다 지워준다.  

이후 새로운 `Canvas`를 만든후 `MainMenu`라는 이름으로 `Panel`을 만든다. `MainMenu`이름의 Panel의 자식으로 `Text`와 `Button`을 넣어서 꾸며준다. 나는 다음과 같이 구성하였다.

![image](https://user-images.githubusercontent.com/37824506/213367391-e26a31b6-2002-4b13-9828-56f395ac7573.png)

다음으로 `Stage_List`라는 이름으로 `Panel을 만든후 그 자식으로 `Text`와 `Button`을 넣어서 꾸며준다. 이후 나온 결과물이다.  

![image](https://user-images.githubusercontent.com/37824506/213367634-16248155-7c7e-4c99-9836-3e77b70b6ee8.png)

<br>

## 3. MainMenu 기능 구현하기

<br>

지금까지 `MainMenu`의 여러 오브젝트들을 만들어 주었다. 이제 그 오브젝트의 버튼들에 여러가지 기능들을 넣어주어야 한다.  
이를 위하여 `MainMenu_UI_Manager`스크립트를 만든후 다음 코드를 넣어준다.

```
public class Bounce_MainMenu_UI_Manager : MonoBehaviour
{
    private GameObject Game_Manager;
    public GameObject MainMenu;
    public GameObject Stage_list;
    public GameObject Lock;

    // Start is called before the first frame update
    void Start()
    {
        Game_Manager = GameObject.FindGameObjectWithTag("GameManager");
        if (Game_Manager.GetComponent<Bounce_GameManager>().Is_Go_Stage_List == true)
        {
            Go_Stage_List();
        }
        Is_Lock();
    }

    // Update is called once per fram

    // ========================== Main Menu =========================
    public void Go_Stage_List()
    {
        MainMenu.SetActive(false);
        Stage_list.SetActive(true);
        Game_Manager.GetComponent<Bounce_GameManager>().Is_Go_Stage_List = true;
    }
        public void Show_Rank()
    {
        
    }

    public void End()
    {
        Application.Quit();

    }

    private void OnApplicationQuit()
    {
        Debug.Log("종료");
    }

    // ========================== Stage List =========================
    public void Go_MainMenu()
    {
        MainMenu.SetActive(true);
        Stage_list.SetActive(false);
        Game_Manager.GetComponent<Bounce_GameManager>().Is_Go_Stage_List = false;
    }
    public void Go_Stage(int Stage)
    {
        Game_Manager.GetComponent<Bounce_GameManager>().Current_Stage = Stage;
        SceneManager.LoadScene("Level " + Stage);
    }
    public void Is_Lock()
    {
        for (int i = 0; i <= Game_Manager.GetComponent<Bounce_GameManager>().Clear_Stage; i++)
        {
            Lock.transform.GetChild(i).gameObject.SetActive(false);
        }
    }
}
```


각각의 버튼에 있는 `On Click()` Event 함수들을 넣어주면 된다.  
다른 `Scene`으로 이동하기 위하여 각각의 `Scene`들을 `Build`해주어야 한다.  
이를 위해 지금까지 만들어둔 `test`파일을 복사하여 `Level 1`이라는 `Scene`을 만들어준다. 이후 `Level 1`을 자신이 원하는 대로 꾸민다. 다 꾸면으면 다음과 같이 `Build Setting`을 해주면 된다.


![build](https://user-images.githubusercontent.com/37824506/213370307-9a1d88bd-a122-4c43-b529-d1b8ab0033a2.gif)

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁