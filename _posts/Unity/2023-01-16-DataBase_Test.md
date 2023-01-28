---
title:  "Unity와 DB 연동하기"
excerpt: "LogIn창을 만들고 DB와 연동하여 로그인기능을 구현하자"

categories:
  - Unity
tags:
  - [Unity, Login, SignUp]

toc: true
toc_sticky: true
 
date: 2023-01-16
last_modified_at: 2023-01-16
---

<br>

## 1. SQLite 다운로드

<br>

다음 사이트에서 3번째 줄에 있는 것을 다운받으면 된다.

https://sqlitebrowser.org/dl/

![image](https://user-images.githubusercontent.com/37824506/212581520-1cfc0647-a373-49ad-a608-2a773856cb79.png)

<br>

## 2. Unity 생성

Unity에서 새 `Project`를 생성한다.

아래 DDL을 다운 받은 후 `Asset` 폴더 안의 `Plugins` 폴더를 만들어서 넣는다.

[was-practice.zip](https://github.com/yyechan0602/yyechan0602.github.io/files/10422008/was-practice.zip)

자신의 유니티 프로젝트 `Assets` 폴더 안에 `StreamingAssets` 폴더를 만든 후 `DB Browser for SQLite.exe`를 실행시켜서 `MyDB`로 새 파일을 만들어준다.  

<br>

## 3. 기본창 구성

Hierarchy에 `Canvas`밑으로 `Panel`을 만든후 `Input Field` 2개와 `Button`을 추가해준다.  
이후 이름을 바꿔주고, ID와 Password 객체의 안의 `Placeholder`안의 text를 각각 `Id`와 `Password`로 바꿔준다.  
또 `create Empty`로 `script` 오브젝트를 만들어준다.

<br>

![image](https://user-images.githubusercontent.com/37824506/212581006-2606af06-e669-4cc9-95d5-946e11fdacd2.png)

이후 `Scripts`라는 폴더를 만들어준 후 안에 `LogIn` Script를 생성해준다.  

<br>

## 4. DB 코드 작성

<br>

    IEnumerator DBCreate()
    {
        string filepath = string.Empty;
        filepath = Application.dataPath + "/MyDB.db";
        if (!File.Exists(filepath))
        {
            File.Copy(Application.streamingAssetsPath + "/MyDB.db", filepath);
        }
        yield return new WaitForSeconds(0.1f);
        print("DB 생성 완료");
    }

    public string GetDBFilePath()
    {
        string str = string.Empty;
        if (Application.platform == RuntimePlatform.Android)
        {
            str = "URI=file:" + Application.persistentDataPath + "/MyDB.db";
        }
        else
        {
            str = "URI=file:" + Application.streamingAssetsPath + "/MyDB.db";
        }
        return str;
    }

    public void DBConnectionCheck()
    {
        try
        {
            dbConnection = new SqliteConnection(GetDBFilePath());
            dbConnection.Open();

            if (dbConnection.State == ConnectionState.Open)
            {
                print("DB연결 성공");
            }
            else
            {
                print("연결실패[ERROR]");
            }
        }
        catch (Exception e)
        {
            print(e);
        }
    }

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁