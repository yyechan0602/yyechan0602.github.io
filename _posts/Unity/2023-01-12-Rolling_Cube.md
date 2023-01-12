---
title:  "큐브 돌리기"
excerpt: "큐브를 돌려서 회전시키는 방법에 대해서 알아보자"

categories:
  - Unity
tags:
  - [Unity]

toc: true
toc_sticky: true
 
date: 2023-01-12
last_modified_at: 2023-01-12
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

다음과 같이 단순하게 받은 값으로 꾸준히 Rotate를 하는 식으로 구현을 하였다. 

![rolling_cube1](https://user-images.githubusercontent.com/37824506/212037106-0db1111d-fc7e-4a9e-ab17-f04be56ee113.gif)

<br>

다음과 같이 잘 구현이 되었다.

<br>

## 3. 문제점 발견

<br>

그런데 이 코드에 단순히 중력을 적용시키자 다음과 같이 이상하게 큐브가 굴러갔다.

![rolling_cube2](https://user-images.githubusercontent.com/37824506/212038329-fa89090b-6d7e-46bc-b185-d15c50d34218.gif)

<br>



<br>



<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.