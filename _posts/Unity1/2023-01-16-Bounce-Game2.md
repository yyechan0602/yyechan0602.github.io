---
title:  "[Bounce Game] 🥎 미니게임 만들기 2"
excerpt: "간단한 미니게임을 만들고 실행해보자"

categories:
  - Unity1
tags:
  - [Unity1, Bounce, Game]

toc: true
toc_sticky: true
 
date: 2023-01-16
last_modified_at: 2023-01-17
---

## 1. 기본 화면 구성하기

이전과 같이 `Bounce Ball`이라는 형식으로 게임을 만든다.  
대신 이번에는 2D로 게임 프로젝트를 생성한다.  

이후 2D `sprite`를 생성후 자신이 원하는 `Asset`을 넣고 다음과 같이 기본적인 공과 땅을 구현해준다.

![스크린샷(14)](https://user-images.githubusercontent.com/37824506/212789989-333d9e9b-0cae-4a42-be14-ea35322d7e0a.png)

이때 하나의 땅의 크기를 (1, 1)로 지정하여 여러개의 블럭으로 땅을 배치하기로 하였다.  

![image](https://user-images.githubusercontent.com/37824506/212790382-45891282-c837-4e03-b8fd-3d1b5959b035.png)

이후 땅에는 `Box Collider 2D`를 추가해주고 공에는 `Rigidbody 2D`와 `Circle Collider 2D`를 추가해준다.  
또한 `Player`와 `Floor`태그를 만들어서 넣어준다.  

<br>

## 2. Jump와 이동 구현하기

<br>

점프와 플레이어 이동을 구현하기 위하여 새 `Bounce_Player`라는 Script를 만든후 다음과 같이 코드를 작성한다.  

    Rigidbody2D rigid;
    bool _isJump;
    public float JumpPower;
    public float limit_speed;
    void Start()
    {
        limit_speed = 5;
        JumpPower = 3;
        _isJump = true;
        rigid = GetComponent<Rigidbody2D>();
    }
    void Update()
    {
        PlayerMove();
        StartCoroutine(Jump());
    }
    void PlayerMove()
    {
        float h = Input.GetAxis("Horizontal");
        rigid.AddForce(Vector2.right * 10 * h * Time.deltaTime, ForceMode2D.Impulse);

        if (rigid.velocity.x > limit_speed)
        {
            rigid.velocity = new Vector2(limit_speed, rigid.velocity.y);
        }
        else if (rigid.velocity.x < -limit_speed)
        {
            rigid.velocity = new Vector2(-limit_speed, rigid.velocity.y);
        }

    }
    IEnumerator Jump()
    {
        if (_isJump == false)
        {
            rigid.AddForce(Vector2.up * JumpPower, ForceMode2D.Impulse);
            print("jump");
            _isJump = true;
            yield return null;
        }
    }
    private void OnCollisionEnter2D(Collision2D collision)
    {
        if (collision.collider.CompareTag("Floor")){
            _isJump = false;
            rigid.velocity = rigid.velocity / 2;
        }
    }

하지만 이 코드에는 한가지 문제가 있다. 바로 다음과 같이 옆에 배치된 바닥에 닿기만 해도 점프가 된다.

![bounce problem](https://user-images.githubusercontent.com/37824506/212789913-01965492-c3d7-4716-b2e6-260c32f3f973.gif)

이를 해결하기 위하여 다음과 같이 미세하게 `FloorTop`이라는 `Sprite`를 만들고 투명도를 0으로 바꾼후 `OnCollisionEnter2D`코드의 `CompareTag`를 `FloorTop`으로 바꾸어 주었다.

![스크린샷(13)](https://user-images.githubusercontent.com/37824506/212789859-508e9f84-5869-421b-8729-d52ae3ab6b37.png)

<br>

## 3. Camera 이동

맵을 이동하는데 카메라가 정지되어 있으면 맵 사이즈에 제약을 받아서 카메라 무브 관련되어 `Script`를 만들어 준다.  
새 `Bounce Camera` Script를 만든후 다음과 같이 작성해준다.  

<br>

    public GameObject player;
    Vector3 target;
    Vector3 velo;
    void Start()
    {
        velo = Vector2.zero;
        StartCoroutine(CameraMove());
    }
    IEnumerator CameraMove()
    {
        while (true)
        {
            target = player.GetComponent<Transform>().position + Vector3.back * 10;
            transform.position = Vector3.SmoothDamp(transform.position, target, ref velo, 1f);
            yield return null;
        }
    }

<br>

![bounce Camera](https://user-images.githubusercontent.com/37824506/212793863-4944be5c-0afd-4cbc-85d4-01631e87dca8.gif)


<br>

## 4. 여러가지 상호작용 오브젝트 만들기  

<br>

게임에서 사용할 여러가지 오브젝트를 만들어 주었다.  

![image](https://user-images.githubusercontent.com/37824506/212808629-a9db1f70-7811-477e-8e1e-a3a4f0905315.png)

이중 `WeakFloor`와 `Jump`에도 추가적으로 `Top`을 추가해 주었다.  
그리고 다음과 같이 여러 오브젝트간의 상호작용을 추가해 주었다.  

<br>   

    Rigidbody2D rigid;
    bool _isJump;
    public float JumpPower;
    public float Instance_JumpPower;
    public float limit_speed;
    public Vector2 Start_Point;

    void Start()
    {
        limit_speed = 5;
        JumpPower = 3;
        Instance_JumpPower = JumpPower;
        _isJump = true;
        rigid = GetComponent<Rigidbody2D>();

        Start_Point = new Vector2(0, 5);
    }

    IEnumerator Jump()
    {
        if (_isJump == false)
        {
            rigid.AddForce(Vector2.up * Instance_JumpPower, ForceMode2D.Impulse);
            _isJump = true;
            Instance_JumpPower = JumpPower;
            yield return null;
        }
        if (transform.position.y < -5)
        {
            Die();
        }
    }

    private void OnCollisionEnter2D(Collision2D collision)
    {
        if (collision.collider.CompareTag("FloorTop"))
        {
            _isJump = false;
            rigid.velocity = rigid.velocity / 2;
        }
        else if (collision.collider.CompareTag("WeakFloorTop"))
        {
            _isJump = false;
            rigid.velocity = rigid.velocity / 2;
        }
        else if (collision.collider.CompareTag("JumpTop"))
        {
            _isJump = false;
            rigid.velocity = rigid.velocity / 2;
            Instance_JumpPower = JumpPower * 1.5f;
        }
        else if (collision.collider.CompareTag("ThornTop") || collision.collider.CompareTag("Monster"))
        {
            Death();
        }
        else if (collision.collider.CompareTag("Coin"))
        {
            
        }
        else if (collision.collider.CompareTag("Portal"))
        {
            Clear();
        }
    }
    void Death()
    {
        rigid.velocity = rigid.velocity * 0;
        transform.position = Start_Point;
    }

    void Clear()
    {

    }

<br>

![3](https://user-images.githubusercontent.com/37824506/212812731-649e5a9c-8af8-484a-8e98-b5a917a50ec8.gif)

다음과 같이 잘 작동되는 모습이다.  
지금까지는 오브젝트에 닿으면 플레이어의 상태에 대해서 조절하였다.  
다음은 오브젝트가 사라지거나 이동하는 등도 구현할 것이다.

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁