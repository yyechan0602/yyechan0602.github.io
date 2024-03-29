---
title:  "[Bounce Game] 🥎 미니게임 만들기 구상"
excerpt: "간단한 미니게임을 만들고 실행해보자"

categories:
  - Unity1
tags:
  - [Unity1, Bounce, Bouncy, Bounce Ball, Game]

toc: true
toc_sticky: true
 
date: 2023-01-15
last_modified_at: 2023-01-15
---

<br>

## 1. 간단한 2D 게임 정하기

세상에는 수많은 여러가지 2D 게임들이 있다.  
똥피하기, Bounce Ball, 벽점프 게임, 건물 부수기, 미로 탈출하기 게임 등등이 있는데 그중에 Bounce Ball이라는 게임을 구현해 보겠다.  

<br>

## 2. Bounce Ball이라는 게임에 필요한 기능  

- UI
  - 메인메뉴와 스테이지 선택하는 기능
  - 맵을 깨면 다음 스테이지가 언락되는 기능
  - 일시정지 및 메인메뉴로 돌아가는 기능
  - DB연동을 통한 로그인과 깬 스테이지에 대한 저장
  - 아이디 별 Death Count와 ranking 기록

<br>

- 게임 컨텐츠
  - 자동으로 일정 높이만큼 점프하는 기능
  - 키보드 방향키에 즉각적으로 반응되지 않는 관성이 적용된 물리법칙
  - 계속 유지되는 발판 및 일정시간마다 사라지거나 이동하는 발판
  - 더블점프같은 능력을 사용할 수 있는 능력 코인
  - 바닥으로 떨어지거나 장애물에 닿으면 처음으로 돌아가는 기능

## 3. UI  

- 메인메뉴와 스테이지 선택하는 기능
  - MainMenu와 스테이지 정보를 담고 있는 Scene 을 만들어서 버튼에 따라 메인메뉴와 스테이지의 장면을 보여준다.  

<br>

- 맵을 깨면 다음 스테이지가 언락되는 기능
  - 각 스테이지마다 `_unlock`이라는 `bool`변수를 배치하여 그 전 스테이지를 클리어시 다음 스테이지의 `_unlock`값이 `true`가 되게 설정한다.
  - 스테이지를 선택시 `_unlock`이 `true`인 스테이지만 선택이 가능하도록 구현한다.
  - singletone 변수에 `Stage_clear` 변수를 넣어서 스테이지를 깰 때마다 1씩 더해준다.

<br>

- 일시정지 및 메인메뉴로 돌아가는 기능
  - 게임을 실행하면 오른쪽 위에 `singletone` 타입의 톱니바퀴 UI를 만들어서 버튼을 누르면 일시정지가 되고 메인메뉴로 가거나 종료를 할 수 있는 버튼을 추가한다.

<br>


- DB연동을 통한 로그인과 깬 스테이지에 대한 저장
  - DB 연동을 통하여 회원가입 후 ID, PassWord가 같을시 로그인
  - 로그인 후 저장된 DB에 따른 스테이지 클리어 기록 및 `DeathCound` 동기화

<br>

- 아이디 별 Death Count와 ranking 기록
  - rank 메뉴에 들어가면 모든 사용자의 DB에서 DeathCount와 스테이지 클리어 개수를 조회하여 볼 수 있는 기능 구현

<br>

## 4. 게임 컨텐츠

- 자동으로 일정 높이만큼 점프하는 기능
  - `Update`문에 `Jump`라는 1.5칸 블럭의 높이만큼 자동으로 점프하는 함수를 넣는다.
  - `Jump` 함수에 `_isJump`라는 bool변수가 false일때만 실행되도록 구현한다.

<br>


- 키보드 방향키에 즉각적으로 반응되지 않는 관성이 적용된 물리법칙
  - `Velocity`라는 -1 ~ 1 사이의 float 함수를 만들어서 키보드에 따라 `Velocity` 값이 변하게 한다.
  - 이후 `Ball`에 `new Vector(Velocity * Speed, 0)`을 더해서 버튼을 누른 시간만큼 빨라지거나 느려지는 물리법칙을 구현한다.
  - `Ball`이 땅에 닿을때마다 `Velocity`의 값에 1/2를 곱해서 마찰력을 구현한다.
  - 여러가지 능력에 따라 일시적으로 `Speed`의 값을 조정한다.

<br>

- 계속 유지되는 발판 및 일정시간마다 사라지거나 이동하는 발판
  - 일정 `Time.deltaTime`마다 오브젝트를 비활성화 하거나 이동시킨다.

<br>

- 더블 점프같은 능력을 사용할 수 있는 능력 코인
  - 맵에서 생성되는 코인을 먹은 후 `space`를 누르면 능력 사용 가능
  - 더블 점프같은 경우 공중에서 `_isJump`를 false로 초기화

<br>

- 바닥으로 떨어지거나 장애물에 닿으면 처음으로 돌아가는 기능
  - `Ball`의 script에 일정 y이하로 떨어지거나 Tag가 `Trap`에 닿을 시 `Death Count`가 증가하고, 시작위치로 순간이동


<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁