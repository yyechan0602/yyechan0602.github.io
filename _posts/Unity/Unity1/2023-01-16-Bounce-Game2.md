---
title:  "[Bounce Game] ๐ฅ ๋ฏธ๋๊ฒ์ ๋ง๋ค๊ธฐ 2"
excerpt: "๊ฐ๋จํ ๋ฏธ๋๊ฒ์์ ๋ง๋ค๊ณ  ์คํํด๋ณด์"

categories:
  - Unity1
tags:
  - [Unity1, Bounce, Game]

toc: true
toc_sticky: true
 
date: 2023-01-16
last_modified_at: 2023-01-17
---

## 1. ๊ธฐ๋ณธ ํ๋ฉด ๊ตฌ์ฑํ๊ธฐ

์ด์ ๊ณผ ๊ฐ์ด `Bounce Ball`์ด๋ผ๋ ํ์์ผ๋ก ๊ฒ์์ ๋ง๋ ๋ค.  
๋์  ์ด๋ฒ์๋ 2D๋ก ๊ฒ์ ํ๋ก์ ํธ๋ฅผ ์์ฑํ๋ค.  

์ดํ 2D `sprite`๋ฅผ ์์ฑํ ์์ ์ด ์ํ๋ `Asset`์ ๋ฃ๊ณ  ๋ค์๊ณผ ๊ฐ์ด ๊ธฐ๋ณธ์ ์ธ ๊ณต๊ณผ ๋์ ๊ตฌํํด์ค๋ค.

![์คํฌ๋ฆฐ์ท(14)](https://user-images.githubusercontent.com/37824506/212789989-333d9e9b-0cae-4a42-be14-ea35322d7e0a.png)

์ด๋ ํ๋์ ๋์ ํฌ๊ธฐ๋ฅผ (1, 1)๋ก ์ง์ ํ์ฌ ์ฌ๋ฌ๊ฐ์ ๋ธ๋ญ์ผ๋ก ๋์ ๋ฐฐ์นํ๊ธฐ๋ก ํ์๋ค.  

![image](https://user-images.githubusercontent.com/37824506/212790382-45891282-c837-4e03-b8fd-3d1b5959b035.png)

์ดํ ๋์๋ `Box Collider 2D`๋ฅผ ์ถ๊ฐํด์ฃผ๊ณ  ๊ณต์๋ `Rigidbody 2D`์ `Circle Collider 2D`๋ฅผ ์ถ๊ฐํด์ค๋ค.  
๋ํ `Player`์ `Floor`ํ๊ทธ๋ฅผ ๋ง๋ค์ด์ ๋ฃ์ด์ค๋ค.  

<br>

## 2. Jump์ ์ด๋ ๊ตฌํํ๊ธฐ

<br>

์ ํ์ ํ๋ ์ด์ด ์ด๋์ ๊ตฌํํ๊ธฐ ์ํ์ฌ ์ `Bounce_Player`๋ผ๋ Script๋ฅผ ๋ง๋ ํ ๋ค์๊ณผ ๊ฐ์ด ์ฝ๋๋ฅผ ์์ฑํ๋ค.  

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

ํ์ง๋ง ์ด ์ฝ๋์๋ ํ๊ฐ์ง ๋ฌธ์ ๊ฐ ์๋ค. ๋ฐ๋ก ๋ค์๊ณผ ๊ฐ์ด ์์ ๋ฐฐ์น๋ ๋ฐ๋ฅ์ ๋ฟ๊ธฐ๋ง ํด๋ ์ ํ๊ฐ ๋๋ค.

![bounce problem](https://user-images.githubusercontent.com/37824506/212789913-01965492-c3d7-4716-b2e6-260c32f3f973.gif)

์ด๋ฅผ ํด๊ฒฐํ๊ธฐ ์ํ์ฌ ๋ค์๊ณผ ๊ฐ์ด ๋ฏธ์ธํ๊ฒ `FloorTop`์ด๋ผ๋ `Sprite`๋ฅผ ๋ง๋ค๊ณ  ํฌ๋ช๋๋ฅผ 0์ผ๋ก ๋ฐ๊พผํ `OnCollisionEnter2D`์ฝ๋์ `CompareTag`๋ฅผ `FloorTop`์ผ๋ก ๋ฐ๊พธ์ด ์ฃผ์๋ค.

![์คํฌ๋ฆฐ์ท(13)](https://user-images.githubusercontent.com/37824506/212789859-508e9f84-5869-421b-8729-d52ae3ab6b37.png)

<br>

## 3. Camera ์ด๋

๋งต์ ์ด๋ํ๋๋ฐ ์นด๋ฉ๋ผ๊ฐ ์ ์ง๋์ด ์์ผ๋ฉด ๋งต ์ฌ์ด์ฆ์ ์ ์ฝ์ ๋ฐ์์ ์นด๋ฉ๋ผ ๋ฌด๋ธ ๊ด๋ จ๋์ด `Script`๋ฅผ ๋ง๋ค์ด ์ค๋ค.  
์ `Bounce Camera` Script๋ฅผ ๋ง๋ ํ ๋ค์๊ณผ ๊ฐ์ด ์์ฑํด์ค๋ค.  

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

## 4. ์ฌ๋ฌ๊ฐ์ง ์ํธ์์ฉ ์ค๋ธ์ ํธ ๋ง๋ค๊ธฐ  

<br>

๊ฒ์์์ ์ฌ์ฉํ  ์ฌ๋ฌ๊ฐ์ง ์ค๋ธ์ ํธ๋ฅผ ๋ง๋ค์ด ์ฃผ์๋ค.  

![image](https://user-images.githubusercontent.com/37824506/212808629-a9db1f70-7811-477e-8e1e-a3a4f0905315.png)

์ด์ค `WeakFloor`์ `Jump`์๋ ์ถ๊ฐ์ ์ผ๋ก `Top`์ ์ถ๊ฐํด ์ฃผ์๋ค.  
๊ทธ๋ฆฌ๊ณ  ๋ค์๊ณผ ๊ฐ์ด ์ฌ๋ฌ ์ค๋ธ์ ํธ๊ฐ์ ์ํธ์์ฉ์ ์ถ๊ฐํด ์ฃผ์๋ค.  

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

๋ค์๊ณผ ๊ฐ์ด ์ ์๋๋๋ ๋ชจ์ต์ด๋ค.  
์ง๊ธ๊น์ง๋ ์ค๋ธ์ ํธ์ ๋ฟ์ผ๋ฉด ํ๋ ์ด์ด์ ์ํ์ ๋ํด์ ์กฐ์ ํ์๋ค.  
๋ค์์ ์ค๋ธ์ ํธ๊ฐ ์ฌ๋ผ์ง๊ฑฐ๋ ์ด๋ํ๋ ๋ฑ๋ ๊ตฌํํ  ๊ฒ์ด๋ค.

<br>

***
    ๊ฐ์ธ ๊ณต๋ถ ๊ธฐ๋ก์ฉ ๋ธ๋ก๊ทธ์๋๋ค.
    ํ๋ฆฌ๊ฑฐ๋ ์ค๋ฅ๊ฐ ์์ ๊ฒฝ์ฐ ์ ๋ณดํด์ฃผ์๋ฉด ๊ฐ์ฌํ๊ฒ ์ต๋๋ค.๐