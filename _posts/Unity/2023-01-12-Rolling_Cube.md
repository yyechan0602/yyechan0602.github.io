---
title:  "큐브 돌리기"
excerpt: "큐브를 돌려서 회전시키는 방법에 대해서 알아보자"

categories:
  - Unity
tags:
  - [Unity, Rolling, Cube]

toc: true
toc_sticky: true
 
date: 2023-01-12
last_modified_at: 2023-01-13
---

## 1. 큐브 굴리기

현재 스터디를 하고 있는 곳에서 다음과 같은 굴러가는 큐브에 대해 한번 만들어 오라고 과제를 내주셨다.  


![project](https://user-images.githubusercontent.com/37824506/212035571-95ffde87-f8d3-4aa9-878a-a6bb1f50343d.gif)

<br>

처음에 이 과제를 내주시고 나서 이걸 어떻게 구현해야 하는지 고민하다가 wasd 방향키에 따라 Rotation을 바꾸는 식으로 하기로 구상을 하였다.
<br>

## 2. 초기구상

<br>

![images](https://user-images.githubusercontent.com/37824506/212033775-b67a73fc-b942-453f-a64f-29c42cfba4f6.PNG)

위와 같이 단순하게 받은 값으로 꾸준히 Rotate를 하는 식으로 구현을 하였다. 

![rolling_cube1](https://user-images.githubusercontent.com/37824506/212037106-0db1111d-fc7e-4a9e-ab17-f04be56ee113.gif)

<br>

그러자 다음과 같이 잘 구현이 되었다.

<br>

## 3. 문제점 발견

<br>

그런데 이 코드에 단순히 중력을 적용시키자 다음과 같이 이상하게 큐브가 굴러갔다.
이것을 해결하기위해 마찰력, 중력에 대해서 여러가지 설정을 해줬는데도 불구하고 어떠한 해결책이 나오지 않았다.

![rolling_cube2](https://user-images.githubusercontent.com/37824506/212038329-fa89090b-6d7e-46bc-b185-d15c50d34218.gif)

<br>

## 4. 최종 코드 

결국 구글링을 하며 방법을 찾다가 `rolling cube`라고 검색을 하자 참고할 만한 영상이 나왔다. 

<https://www.youtube.com/watch?v=06rs3U2bpy8>  

이 동영상을 참고하여 코드를 짰다.
  
<br>

### Update문  

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

이동중에 이동하는것을 막기 위하여 `_isrolling`이 false일 때만 작동하게 하였다.  
키보드의 입력에 따른 이동을 구현하기 위하여 wasd에 따른 `Rolling_Manage` 함수를 작동시키게 `Update`문을 구현하였다.  

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

여기서 만약 d값이 들어왔을 시에 `axis`는 `transform.position`이라는 현재 위치에 `Vector3.down` (0, -1, 0)와 `dir` (1, 0, 0)이라는 벡터값을 합치고 2로 나눈 값인 (0.5, -0.5, 0)만큼 움직이면 물체의 사이즈가 1이라 했을때, 그 물체의 모서리의 좌표가 나온다.

<br>

![image](https://user-images.githubusercontent.com/37824506/212218893-4d39e3b7-a9fb-49d1-8639-3c408ee683bb.PNG)

<br>

또 `angle`은 `Vector3.Cross`라는 외적함수를 이용하여 `Vector3.up` (0, 1, 0)과 `dir` (1, 0, 0)을 외적시키면 +값이 나온다. 이렇게 두 값을 외적시킨 값의 부호를 통해서 큐브가 어느 방향으로 굴러갈지를 정해주었다.
프로그램이 작동하는 도중에 따로 작동되게 하기 위하여 `coroutine`을 사용하였다.

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

이후 `Rolling`이라는 함수에서는 `_isRolling`을 true로 변경하고, `RotateAround`라는 `axis`값을 기준으로 `angle`방향으로 돌려주는 함수를 이용하여 큐브를 90도 돌려주었다.

<br>

## 결과물

![rooling_cube](https://user-images.githubusercontent.com/37824506/212220228-04a5a5c5-1981-4a96-8011-ba79d75bc1c1.gif)

이후 완성된 결과물이다.

<br>



<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.