---
title:  "๐ Unity์ DB ์ฐ๋ํ๊ธฐ"
excerpt: "LogIn์ฐฝ์ ๋ง๋ค๊ณ  DB์ ์ฐ๋ํ์ฌ ๋ก๊ทธ์ธ๊ธฐ๋ฅ์ ๊ตฌํํ์"

categories:
  - Unity1
tags:
  - [Unity1, Login, SignUp]

toc: true
toc_sticky: true
 
date: 2023-01-16
last_modified_at: 2023-01-16
---

<br>

## 1. SQLite ๋ค์ด๋ก๋

<br>

๋ค์ ์ฌ์ดํธ์์ 3๋ฒ์งธ ์ค์ ์๋ ๊ฒ์ ๋ค์ด๋ฐ์ผ๋ฉด ๋๋ค.

https://sqlitebrowser.org/dl/

![image](https://user-images.githubusercontent.com/37824506/212581520-1cfc0647-a373-49ad-a608-2a773856cb79.png)

<br>

## 2. Unity ์์ฑ

Unity์์ ์ `Project`๋ฅผ ์์ฑํ๋ค.

์๋ DDL์ ๋ค์ด ๋ฐ์ ํ `Asset` ํด๋ ์์ `Plugins` ํด๋๋ฅผ ๋ง๋ค์ด์ ๋ฃ๋๋ค.

[was-practice.zip](https://github.com/yyechan0602/yyechan0602.github.io/files/10422008/was-practice.zip)

์์ ์ ์ ๋ํฐ ํ๋ก์ ํธ `Assets` ํด๋ ์์ `StreamingAssets` ํด๋๋ฅผ ๋ง๋  ํ `DB Browser for SQLite.exe`๋ฅผ ์คํ์์ผ์ `MyDB`๋ก ์ ํ์ผ์ ๋ง๋ค์ด์ค๋ค.  

<br>

## 3. ๊ธฐ๋ณธ์ฐฝ ๊ตฌ์ฑ

Hierarchy์ `Canvas`๋ฐ์ผ๋ก `Panel`์ ๋ง๋ ํ `Input Field` 2๊ฐ์ `Button`์ ์ถ๊ฐํด์ค๋ค.  
์ดํ ์ด๋ฆ์ ๋ฐ๊ฟ์ฃผ๊ณ , ID์ Password ๊ฐ์ฒด์ ์์ `Placeholder`์์ text๋ฅผ ๊ฐ๊ฐ `Id`์ `Password`๋ก ๋ฐ๊ฟ์ค๋ค.  
๋ `create Empty`๋ก `script` ์ค๋ธ์ ํธ๋ฅผ ๋ง๋ค์ด์ค๋ค.

<br>

![image](https://user-images.githubusercontent.com/37824506/212581006-2606af06-e669-4cc9-95d5-946e11fdacd2.png)

์ดํ `Scripts`๋ผ๋ ํด๋๋ฅผ ๋ง๋ค์ด์ค ํ ์์ `LogIn` Script๋ฅผ ์์ฑํด์ค๋ค.  

<br>

## 4. DB ์ฝ๋ ์์ฑ

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
        print("DB ์์ฑ ์๋ฃ");
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
                print("DB์ฐ๊ฒฐ ์ฑ๊ณต");
            }
            else
            {
                print("์ฐ๊ฒฐ์คํจ[ERROR]");
            }
        }
        catch (Exception e)
        {
            print(e);
        }
    }

<br>

***
    ๊ฐ์ธ ๊ณต๋ถ ๊ธฐ๋ก์ฉ ๋ธ๋ก๊ทธ์๋๋ค.
    ํ๋ฆฌ๊ฑฐ๋ ์ค๋ฅ๊ฐ ์์ ๊ฒฝ์ฐ ์ ๋ณดํด์ฃผ์๋ฉด ๊ฐ์ฌํ๊ฒ ์ต๋๋ค.๐