---
title:  "๐ฒ ํ๋ธ ๋๋ฆฌ๊ธฐ"
excerpt: "ํ๋ธ๋ฅผ ๋๋ ค์ ํ์ ์ํค๋ ๋ฐฉ๋ฒ์ ๋ํด์ ์์๋ณด์"

categories:
  - Unity1
tags:
  - [Unity1, Rolling, Cube]

toc: true
toc_sticky: true
 
date: 2023-01-12
last_modified_at: 2023-01-13
---

## 1. ํ๋ธ ๊ตด๋ฆฌ๊ธฐ

ํ์ฌ ์คํฐ๋๋ฅผ ํ๊ณ  ์๋ ๊ณณ์์ ๋ค์๊ณผ ๊ฐ์ ๊ตด๋ฌ๊ฐ๋ ํ๋ธ์ ๋ํด ํ๋ฒ ๋ง๋ค์ด ์ค๋ผ๊ณ  ๊ณผ์ ๋ฅผ ๋ด์ฃผ์จ๋ค.  


![project](https://user-images.githubusercontent.com/37824506/212035571-95ffde87-f8d3-4aa9-878a-a6bb1f50343d.gif)

<br>

์ฒ์์ ์ด ๊ณผ์ ๋ฅผ ๋ด์ฃผ์๊ณ  ๋์ ์ด๊ฑธ ์ด๋ป๊ฒ ๊ตฌํํด์ผ ํ๋์ง ๊ณ ๋ฏผํ๋ค๊ฐ wasd ๋ฐฉํฅํค์ ๋ฐ๋ผ Rotation์ ๋ฐ๊พธ๋ ์์ผ๋ก ํ๊ธฐ๋ก ๊ตฌ์์ ํ์๋ค.
<br>

## 2. ์ด๊ธฐ๊ตฌ์

<br>

![images](https://user-images.githubusercontent.com/37824506/212033775-b67a73fc-b942-453f-a64f-29c42cfba4f6.PNG)

์์ ๊ฐ์ด ๋จ์ํ๊ฒ ๋ฐ์ ๊ฐ์ผ๋ก ๊พธ์คํ Rotate๋ฅผ ํ๋ ์์ผ๋ก ๊ตฌํ์ ํ์๋ค. 

![rolling_cube1](https://user-images.githubusercontent.com/37824506/212037106-0db1111d-fc7e-4a9e-ab17-f04be56ee113.gif)

<br>

๊ทธ๋ฌ์ ๋ค์๊ณผ ๊ฐ์ด ์ ๊ตฌํ์ด ๋์๋ค.

<br>

## 3. ๋ฌธ์ ์  ๋ฐ๊ฒฌ

<br>

๊ทธ๋ฐ๋ฐ ์ด ์ฝ๋์ ๋จ์ํ ์ค๋ ฅ์ ์ ์ฉ์ํค์ ๋ค์๊ณผ ๊ฐ์ด ์ด์ํ๊ฒ ํ๋ธ๊ฐ ๊ตด๋ฌ๊ฐ๋ค.
์ด๊ฒ์ ํด๊ฒฐํ๊ธฐ์ํด ๋ง์ฐฐ๋ ฅ, ์ค๋ ฅ์ ๋ํด์ ์ฌ๋ฌ๊ฐ์ง ์ค์ ์ ํด์คฌ๋๋ฐ๋ ๋ถ๊ตฌํ๊ณ  ์ด๋ ํ ํด๊ฒฐ์ฑ์ด ๋์ค์ง ์์๋ค.

![rolling_cube2](https://user-images.githubusercontent.com/37824506/212038329-fa89090b-6d7e-46bc-b185-d15c50d34218.gif)

<br>

## 4. ์ต์ข ์ฝ๋ 

๊ฒฐ๊ตญ ๊ตฌ๊ธ๋ง์ ํ๋ฉฐ ๋ฐฉ๋ฒ์ ์ฐพ๋ค๊ฐ `rolling cube`๋ผ๊ณ  ๊ฒ์์ ํ์ ์ฐธ๊ณ ํ  ๋งํ ์์์ด ๋์๋ค. 

<https://www.youtube.com/watch?v=06rs3U2bpy8>  

์ด ๋์์์ ์ฐธ๊ณ ํ์ฌ ์ฝ๋๋ฅผ ์งฐ๋ค.
  
<br>

### Update๋ฌธ  

```
void Update()
    {
        if (_isRolling != true)
        {
            if (Input.GetKey(KeyCode.W)) { Rolling_Manage(Vector3.forward); }
            else if (Input.GetKey(KeyCode.S)) { Rolling_Manage(Vector3.back); }
            else if (Input.GetKey(KeyCode.D)) { Rolling_Manage(Vector3.right); }
            else if (Input.GetKey(KeyCode.A)) { Rolling_Manage(Vector3.left); }
        }
    }
```

์ด๋์ค์ ์ด๋ํ๋๊ฒ์ ๋ง๊ธฐ ์ํ์ฌ `_isrolling`์ด false์ผ ๋๋ง ์๋ํ๊ฒ ํ์๋ค.  
ํค๋ณด๋์ ์๋ ฅ์ ๋ฐ๋ฅธ ์ด๋์ ๊ตฌํํ๊ธฐ ์ํ์ฌ wasd์ ๋ฐ๋ฅธ `Rolling_Manage` ํจ์๋ฅผ ์๋์ํค๊ฒ `Update`๋ฌธ์ ๊ตฌํํ์๋ค.  

<br>


### Rolling_Manager
```
void Rolling_Manage(Vector3 dir)
    {
        var axis = transform.position + (Vector3.down + dir) * 0.5f;
        var angle = Vector3.Cross(Vector3.up, dir);
        StartCoroutine(Rolling(axis, angle));
    }
```

์ฌ๊ธฐ์ ๋ง์ฝ d๊ฐ์ด ๋ค์ด์์ ์์ `axis`๋ `transform.position`์ด๋ผ๋ ํ์ฌ ์์น์ `Vector3.down` (0, -1, 0)์ `dir` (1, 0, 0)์ด๋ผ๋ ๋ฒกํฐ๊ฐ์ ํฉ์น๊ณ  2๋ก ๋๋ ๊ฐ์ธ (0.5, -0.5, 0)๋งํผ ์์ง์ด๋ฉด ๋ฌผ์ฒด์ ์ฌ์ด์ฆ๊ฐ 1์ด๋ผ ํ์๋, ๊ทธ ๋ฌผ์ฒด์ ๋ชจ์๋ฆฌ์ ์ขํ๊ฐ ๋์จ๋ค.

<br>

![image](https://user-images.githubusercontent.com/37824506/212218893-4d39e3b7-a9fb-49d1-8639-3c408ee683bb.PNG)

<br>

๋ `angle`์ `Vector3.Cross`๋ผ๋ ์ธ์ ํจ์๋ฅผ ์ด์ฉํ์ฌ `Vector3.up` (0, 1, 0)๊ณผ `dir` (1, 0, 0)์ ์ธ์ ์ํค๋ฉด +๊ฐ์ด ๋์จ๋ค. ์ด๋ ๊ฒ ๋ ๊ฐ์ ์ธ์ ์ํจ ๊ฐ์ ๋ถํธ๋ฅผ ํตํด์ ํ๋ธ๊ฐ ์ด๋ ๋ฐฉํฅ์ผ๋ก ๊ตด๋ฌ๊ฐ์ง๋ฅผ ์ ํด์ฃผ์๋ค.
ํ๋ก๊ทธ๋จ์ด ์๋ํ๋ ๋์ค์ ๋ฐ๋ก ์๋๋๊ฒ ํ๊ธฐ ์ํ์ฌ `coroutine`์ ์ฌ์ฉํ์๋ค.

<br>

## rolling


```
IEnumerator Rolling(Vector3 axis, Vector3 angle)
    {
        _isRolling = true;
        for (int i = 0; i < (90 / speed); i++) {
            transform.RotateAround(axis, angle, speed);
            yield return null;
        }
        _isRolling = false;
    }
```

<br>

์ดํ `Rolling`์ด๋ผ๋ ํจ์์์๋ `_isRolling`์ true๋ก ๋ณ๊ฒฝํ๊ณ , `RotateAround`๋ผ๋ `axis`๊ฐ์ ๊ธฐ์ค์ผ๋ก `angle`๋ฐฉํฅ์ผ๋ก ๋๋ ค์ฃผ๋ ํจ์๋ฅผ ์ด์ฉํ์ฌ ํ๋ธ๋ฅผ 90๋ ๋๋ ค์ฃผ์๋ค.

<br>

## ๊ฒฐ๊ณผ๋ฌผ

![rooling_cube](https://user-images.githubusercontent.com/37824506/212220228-04a5a5c5-1981-4a96-8011-ba79d75bc1c1.gif)

์ดํ ์์ฑ๋ ๊ฒฐ๊ณผ๋ฌผ์ด๋ค.

<br>



<br>

***
    ๊ฐ์ธ ๊ณต๋ถ ๊ธฐ๋ก์ฉ ๋ธ๋ก๊ทธ์๋๋ค.
    ํ๋ฆฌ๊ฑฐ๋ ์ค๋ฅ๊ฐ ์์ ๊ฒฝ์ฐ ์ ๋ณดํด์ฃผ์๋ฉด ๊ฐ์ฌํ๊ฒ ์ต๋๋ค.๐