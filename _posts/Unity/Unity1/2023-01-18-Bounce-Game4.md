---
title:  "[Bounce Game] ๐ฅ ๋ฏธ๋๊ฒ์ ๋ง๋ค๊ธฐ 4"
excerpt: "๊ฐ๋จํ ๋ฏธ๋๊ฒ์์ ๋ง๋ค๊ณ  ์คํํด๋ณด์"

categories:
  - Unity1
tags:
  - [Unity1, Bounce, Game]

toc: true
toc_sticky: true
 
date: 2023-01-18
last_modified_at: 2023-01-18
---

## 1. UI ๊ตฌํํ๊ธฐ

`Hierarchy`์์ `create -> UI -> Canvas`๋ฅผ ๋ง๋ ๋ค.
`UI`์ `Button`์ ์์ฑํด์ค๋ค `Option Button`์ด๋ผ๋ ์ด๋ฆ์ผ๋ก ๋ฐ๊ฟ์ค๋ค.
`Panel`์ ์์ฑํด์ค๋ค `Option`์ด๋ผ๋ ์ด๋ฆ์ผ๋ก ๋ฐ๊ฟ์ฃผ๊ณ , `Option`์๋์ `Button`์ 4๊ฐ ๋ง๋ ํ ์ด๋ฆ์ ๊ฐ๊ฐ `Play`, `Sound_On`, `Sound_Off`, `Menu`๋ก ๋ฐ๊ฟ์ค๋ค. ์ด๋ `Sound` ๋ฒํผ ๋๊ฐ๋ ์๋ก ๊ฒน์ณ ๋๋๋ค.
์ดํ ๋ฒํผ๋ณ ์์ ์ด ์ํ๋ `Asset`์ ๋ฃ์ด์ค๋ค, Panel์๋ ์ ๋นํ ์์์ ๋ฃ์ด์ฃผ๊ณ , ํฌ๊ธฐ ์กฐ์ ์ ํ๋ค.

๊ทธ๋ฌ์ ๋ค์๊ณผ ๊ฐ์ด ๊ตฌํ๋์๋ค.

![image](https://user-images.githubusercontent.com/37824506/213097946-24eeb8fa-01ac-4ec6-b2d1-010d57380faa.png)

์ดํ `Canvas`์ ์์์ผ๋ก `UI_Manager`๋ผ๋ ์ด๋ฆ์ผ๋ก `Empty` ์ค๋ธ์ ํธ๋ฅผ ๋ง๋ ํ `UI_Manager`๋ผ๋ ์คํฌ๋ฆฝํธ๋ฅผ ๋ง๋ค์ด์ ๋ฃ์ด์ค๋ค.

์คํฌ๋ฆฝํธ ์์ ๋ค์๊ณผ ๊ฐ์ ์ฝ๋๋ฅผ ๋ฃ์ด์ค๋ค.  

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

๊ฐ๊ฐ์ ๋ฒํผ์ ๋ค์๊ณผ ๊ฐ์ด ํจ์๋ฅผ ๋ฐฐ์ ํด์ฃผ๋ฉด ๋๋ค.

![playbutton](https://user-images.githubusercontent.com/37824506/213099113-a0f24ebe-77b8-4b7e-95ac-2835e93b6159.gif)

์ดํ `Sound_Off` ์ค๋ธ์ ํธ์ `inspector`์ ์๋ ์ด๋ฆ ์์ ๋ฒํผ์ ๋๋ฌ์ ๋นํ์ฑํ ์ํจ ํ์, `Option`๋นํ์ฑํ๋ฅผ ์ํค๊ณ  ๊ฒ์์ ์๋์ํฌ ์ ๋ค์๊ณผ ๊ฐ์ด ์ ์๋๋๋ค.

![option](https://user-images.githubusercontent.com/37824506/213099798-d82a1c79-17cb-4f9a-8c27-4b2ebae3ee09.gif)

<br>

## 2. MainMenu Scene ๋ง๋ค๊ธฐ

<br>

๋ค์์ผ๋ก ์ด์ ๊น์ง ๋ง๋ค์๋ `Scene`์ ๋ณต์ฌํ์ฌ `MainMenu`๋ผ๋ ์ด๋ฆ์ผ๋ก ๋ฐ๊ฟ์ค๋ค. ์ดํ ์์ ์๋ `GameManager`๋ฅผ ์ ์ธํ๊ณ  ๋ค ์ง์์ค๋ค.  

์ดํ ์๋ก์ด `Canvas`๋ฅผ ๋ง๋ ํ `MainMenu`๋ผ๋ ์ด๋ฆ์ผ๋ก `Panel`์ ๋ง๋ ๋ค. `MainMenu`์ด๋ฆ์ Panel์ ์์์ผ๋ก `Text`์ `Button`์ ๋ฃ์ด์ ๊พธ๋ฉฐ์ค๋ค. ๋๋ ๋ค์๊ณผ ๊ฐ์ด ๊ตฌ์ฑํ์๋ค.

![image](https://user-images.githubusercontent.com/37824506/213367391-e26a31b6-2002-4b13-9828-56f395ac7573.png)

๋ค์์ผ๋ก `Stage_List`๋ผ๋ ์ด๋ฆ์ผ๋ก `Panel์ ๋ง๋ ํ ๊ทธ ์์์ผ๋ก `Text`์ `Button`์ ๋ฃ์ด์ ๊พธ๋ฉฐ์ค๋ค. ์ดํ ๋์จ ๊ฒฐ๊ณผ๋ฌผ์ด๋ค.  

![image](https://user-images.githubusercontent.com/37824506/213367634-16248155-7c7e-4c99-9836-3e77b70b6ee8.png)

<br>

## 3. MainMenu ๊ธฐ๋ฅ ๊ตฌํํ๊ธฐ

<br>

์ง๊ธ๊น์ง `MainMenu`์ ์ฌ๋ฌ ์ค๋ธ์ ํธ๋ค์ ๋ง๋ค์ด ์ฃผ์๋ค. ์ด์  ๊ทธ ์ค๋ธ์ ํธ์ ๋ฒํผ๋ค์ ์ฌ๋ฌ๊ฐ์ง ๊ธฐ๋ฅ๋ค์ ๋ฃ์ด์ฃผ์ด์ผ ํ๋ค.  
์ด๋ฅผ ์ํ์ฌ `MainMenu_UI_Manager`์คํฌ๋ฆฝํธ๋ฅผ ๋ง๋ ํ ๋ค์ ์ฝ๋๋ฅผ ๋ฃ์ด์ค๋ค.

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
        Debug.Log("์ข๋ฃ");
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


๊ฐ๊ฐ์ ๋ฒํผ์ ์๋ `On Click()` Event ํจ์๋ค์ ๋ฃ์ด์ฃผ๋ฉด ๋๋ค.  
๋ค๋ฅธ `Scene`์ผ๋ก ์ด๋ํ๊ธฐ ์ํ์ฌ ๊ฐ๊ฐ์ `Scene`๋ค์ `Build`ํด์ฃผ์ด์ผ ํ๋ค.  
์ด๋ฅผ ์ํด ์ง๊ธ๊น์ง ๋ง๋ค์ด๋ `test`ํ์ผ์ ๋ณต์ฌํ์ฌ `Level 1`์ด๋ผ๋ `Scene`์ ๋ง๋ค์ด์ค๋ค. ์ดํ `Level 1`์ ์์ ์ด ์ํ๋ ๋๋ก ๊พธ๋ฏผ๋ค. ๋ค ๊พธ๋ฉด์ผ๋ฉด ๋ค์๊ณผ ๊ฐ์ด `Build Setting`์ ํด์ฃผ๋ฉด ๋๋ค.


![build](https://user-images.githubusercontent.com/37824506/213370307-9a1d88bd-a122-4c43-b529-d1b8ab0033a2.gif)

<br>

***
    ๊ฐ์ธ ๊ณต๋ถ ๊ธฐ๋ก์ฉ ๋ธ๋ก๊ทธ์๋๋ค.
    ํ๋ฆฌ๊ฑฐ๋ ์ค๋ฅ๊ฐ ์์ ๊ฒฝ์ฐ ์ ๋ณดํด์ฃผ์๋ฉด ๊ฐ์ฌํ๊ฒ ์ต๋๋ค.๐