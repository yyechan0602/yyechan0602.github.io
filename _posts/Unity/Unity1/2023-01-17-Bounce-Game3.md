---
title:  "[Bounce Game] ๐ฅ ๋ฏธ๋๊ฒ์ ๋ง๋ค๊ธฐ 3"
excerpt: "๊ฐ๋จํ ๋ฏธ๋๊ฒ์์ ๋ง๋ค๊ณ  ์คํํด๋ณด์"

categories:
  - Unity1
tags:
  - [Unity1, Bounce, Game]

toc: true
toc_sticky: true
 
date: 2023-01-17
last_modified_at: 2023-01-17
---

## 1. GameManager ๋ง๋ค๊ธฐ

<br>

ํ๋ ์ดํ๊ณ  ์๋ ์ฌ๋์ ID, ํด๋ฆฌ์ด ํ ์คํ์ด์ง ๊ฐ์, ํ๋ ์ด์ด ์ ์, DeathCount๋ฑ์ ๊ธฐ๋กํ๊ธฐ ์ํ `SingleTon`์ `GameManager`๋ฅผ ๋ง๋ค์ด์ค๋ค.  
์ด๋ฅผ ์ํ์ฌ `GameManager`์ด๋ฆ์ `Script`๋ฅผ ๋ง๋ค์ด ์ค ๋ค ๋ค์ ์ฝ๋๋ฅผ ์ถ๊ฐํด์ฃผ๋ฉด ๋๋ค.

    public static Bounce_GameManager instance = null;
    public string ID;
    public int Current_Stage;
    public int Clear_Stage;
    public int Current_Score;
    public int Score;
    public int Death_Count;

    private void Awake()
    {
        if (instance == null) //instance๊ฐ null. ์ฆ, ์์คํ์์ ์กด์ฌํ๊ณ  ์์ง ์์๋
        {
            instance = this; //๋ด์์ ์ instance๋ก ๋ฃ์ด์ค๋๋ค.
            DontDestroyOnLoad(gameObject); //OnLoad(์ฌ์ด ๋ก๋ ๋์์๋) ์์ ์ ํ๊ดดํ์ง ์๊ณ  ์ ์ง
        }
        else
        {
            if (instance != this) //instance๊ฐ ๋ด๊ฐ ์๋๋ผ๋ฉด ์ด๋ฏธ instance๊ฐ ํ๋ ์กด์ฌํ๊ณ  ์๋ค๋ ์๋ฏธ
                Destroy(this.gameObject); //๋ ์ด์ ์กด์ฌํ๋ฉด ์๋๋ ๊ฐ์ฒด์ด๋ ๋ฐฉ๊ธ AWake๋ ์์ ์ ์ญ์ 
        }
    }

<br>

์ด์  ๊ฒ์ ํ๋ ์ด ๋์ค `Scene`์ด ๋ฐ๋๋๋ผ๋ ์ด ์ค๋ธ์ ํธ๋ ์ ์ง๋๊ฒ ๋๋ค.  
์ด์  ์ฃฝ์์์ `DeathCount`๋ฅผ ์นด์ดํธ ํ๊ธฐ ์ํ์ฌ ์ํ์ฌ `Player` Script์ ๋์๊ฐ์ 
`public GameObject Game_Manager;`๋ฅผ ์ถ๊ฐํด์ค๋ค ๋ค์ ์ฝ๋๋ฅผ ๋ฃ์ด๋๋ค.

    void Death()
    {
        rigid.velocity = rigid.velocity * 0;
        transform.position = Start_Point;
        Game_Manager.GetComponent<Bounce_GameManager>().Death_Count += 1;
        Game_Manager.GetComponent<Bounce_GameManager>().Current_Score = 0;

        for (int i = 0; i < Coins.transform.childCount; i++){
            Coins.transform.GetChild(i).gameObject.SetActive(true);
        }
        for (int i = 0; i < Weak_Floors.transform.childCount; i++)
        {
            Weak_Floors.transform.GetChild(i).gameObject.SetActive(true);
        }
    }


<br>

## 2. ์ฝ์ธ ์ํธ์์ฉ ๊ตฌํํ๊ธฐ

์ฝ์ธ์ ๋จน์์์ ์ ์๊ฐ ์ค๋ฅด๊ณ  ์ฝ์ธ ์ค๋ธ์ ํธ๋ ์ ์ ๋นํ์ฑํ๊ฐ ๋์ฌ์ผ๋ง ํ๋ค. ๋ํ ์ฃฝ์์๋ ๋จน์ ์ ์๊ฐ ์ด๊ธฐํ๋๊ณ , ์ฝ์ธ์ด ๋ค์ ํ์ฑํ๊ฐ ๋์ด์ผ ํ๋ค.  

`Player`์คํฌ๋ฆฝํธ์ ๋ค์ด๊ฐํ `public GameObject Coins;` ์ฝ๋๋ฅผ ๋ฃ์ด์ค๋ค.

์ด๋ฅผ ์ํ์ฌ ๋ฐฉ๊ธ์ ์ ๋ง๋  `Death`ํจ์์ ๋ค์ ์ฝ๋๋ฅผ ๋ฃ๋๋ค.

        for (int i = 0; i < Coins.transform.childCount; i++){
            Coins.transform.GetChild(i).gameObject.SetActive(true);
        }

<br>


์ดํ `Coin` Scripts๋ฅผ ๋ง๋ค์ด์คํ ๋ค์ ์ฝ๋๋ฅผ ๋ฃ๋๋ค.

    public GameObject Game_Manager;
    private void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.gameObject.CompareTag("Player"))
        {
            gameObject.SetActive(false);
            Game_Manager.GetComponent<Bounce_GameManager>().Current_Score += 1;
        }
    }

Unity์ ๋์๊ฐ์ `Create Empty`๋ฅผ ๋ง๋ ํ ์ด๋ฆ์ `Coins`๋ก ๋ฐ๊พผํ ๋ชจ๋  `Coin`์ค๋ธ์ ํธ๋ฅผ ๋ฃ์ด์ค๋ค. ๊ฐ๊ฐ์ `Coin`๋ค์๊ฒ ์ ์คํฌ๋ฆฝํธ๋ฅผ ๋ฃ์ด์ค๋ค. ๋ `Player` ์ค๋ธ์ ํธ์ `Coins` ๋ณ์์ `Coins` ์ค๋ธ์ ํธ๋ฅผ ๋์ด๋ค๊ฐ ๋ฃ์ด์ค๋ค.

<br>

## 3. ๋ชฌ์คํฐ AI ๊ตฌํํ๊ธฐ

๋ชฌ์คํฐ๋ ๊ฐ๋งํ ๋ฉ์ถฐ ์๋๊ฒ ์๋๋ผ ์ค์ค๋ก ์๊ฐ์ ๊ฐ์ง๊ณ  ์์ง์ฌ์ผ ํ๋ค. ๋ฐ๋ผ์ ๋ค์๊ณผ ๊ฐ์ด 3๊ฐ์ง๋ฅผ ๊ตฌํํ๊ธฐ๋ก ํ์๋ค. 

- 2์ด๋ง๋ค ์์ผ๋ก ๊ฐ๊ธฐ, ์ ์ง, ๋ค๋ก๊ฐ๊ธฐ
- ์งํ๋ฐฉํฅ์ ๋ฐํ์ด ์์ ๊ฒฝ์ฐ ๋ฐฉํฅ ์ ํํ๊ธฐ
- ๋ฐฉํฅ์ ์ ํํ๊ฑฐ๋ ๋ค๋ก ๊ฐ ๋, ์บ๋ฆญํฐ๊ฐ ์ข์ฐ๋ฐ์  ๋๊ฒ ํ๊ธฐ

<br>

์ด๋ฅผ ์ํ์ฌ ๋ค์๊ณผ ๊ฐ์ด `Raycast`๋ฅผ ์ฌ์ฉํ์ฌ ์ด๋๋ฐฉํฅ์ ๋ฐํ์ด ์๋์ง ์ฒดํฌํ์๊ณ , `Coroutine`๋ฅผ ์ฌ์ฉํ์ฌ, 2์ด๋ง๋ค `Random.range`์ผ๋ก `-1, 0, 1`์ ๋ฐฉํฅ์ด ๋ฌด์์๋ก ๋์ค๋๋ก ํ์๋ค.

    Rigidbody2D rigid;
    public int next_Move;

    float currnetRotation;
    SpriteRenderer spriteRenderer;
    // Start is called before the first frame update
    void Start()
    {
        currnetRotation = -1;
        rigid = GetComponent<Rigidbody2D>();
        spriteRenderer = GetComponent<SpriteRenderer>();
        StartCoroutine(Think());
        StartCoroutine(Monster_Move());
        StartCoroutine(turn());
    }

    // Update is called once per frame
    void Update()
    {
    }

    IEnumerator Monster_Move()
    {
        while (true)
        {
            rigid.velocity = new Vector2(next_Move * 2, rigid.velocity.y);

            //Platform Check
            Vector2 frontVec = new Vector2(rigid.position.x + next_Move, rigid.position.y);
            Debug.DrawRay(frontVec, Vector3.down, new Color(0, 1, 0)); //์ด๋ก์
            RaycastHit2D rayHit = Physics2D.Raycast(frontVec, Vector3.down, 1, LayerMask.GetMask("platform"));
            if (rayHit.collider == null)
            {
                next_Move = -1 * next_Move;
            }
            yield return null;
        }
    }

    IEnumerator Think()
    {
        while (true)
        {
            next_Move = Random.Range(-1, 2);
            yield return new WaitForSeconds(2);
        }
    }

    IEnumerator turn()
    {
        while (true)
        {
            spriteRenderer.flipX = next_Move == 1;
            yield return null;
        }
    }

<br>

## 4. ์ฝํ ๋ฐํ ๊ตฌํํ๊ธฐ

์ฝํ ๋ฐํ ๊ฐ์ ๊ฒฝ์ฐ ๋ฐ์ผ๋ฉด ์ค๋ธ์ ํธ๊ฐ ์ฌ๋ผ์ง๊ณ , `Death`๊ฐ ๋ฐ๋ ์ ๋ค์ ์๊ฒจ์ผ ํ๋ค. ๋ฐ๋ผ์ `Coin`๊ณผ ๋น์ทํ๊ฒ `Player` ์คํฌ๋ฆฝํธ์ `public GameObject Weak_Floors;`๋ฅผ ๋ฃ์ด์ค๋ค.  

์ดํ `Death`ํจ์์ ๋ค์ ์ฝ๋๋ฅผ ๋ฃ์ด์ค๋ค.

    for (int i = 0; i < Weak_Floors.transform.childCount; i++){
        Weak_Floors.transform.GetChild(i).gameObject.SetActive(true);
    }

<br>

`Weak Floors Set`์ด๋ฆ์ผ๋ก `Empty Object`๋ฅผ ๋ง๋ค์ด์ค๋ค. ์ดํ ๋ชจ๋  `Weak Floor`๋ฅผ `Weak Floors Set`์ ๋ฃ์ด์ค๋ค. `Player` ์ค๋ธ์ ํธ์ `Weak_Floors`๋ณ์์ `Weak Floors Set`์ ๋ฃ์ด์ค๋ค.
    public GameObject Weak_Floors;

<br>

์๋ก์ด ์คํฌ๋ฆฝํธ๋ฅผ ๋ง๋ ํ ๋ค์๊ณผ ๊ฐ์ ์ฝ๋๋ฅผ ๋ฃ์ด์ค๋ค `Weak FloorTop`์ค๋ธ์ ํธ์ ๋ฃ์ด์ฃผ๋ฉด ๋๋ค.

    private void OnCollisionEnter2D(Collision2D collision)
    {
        if(collision.collider.CompareTag("Player")){
            gameObject.transform.parent.gameObject.SetActive(false);
        }
    }

<br>

## 5. ์์ง์ด๋ ๋ฐํ ๊ตฌํํ๊ธฐ

์ ์คํฌ๋ฆฝํธ๋ฅผ ๋ง๋  ํ `Moving Floor`์ ๋ฃ์ด์ฃผ๋ฉด ๋๋ค.  
๋ชฌ์คํฐ์์ ์ฌ์ฉํ `Raycast`๋ฅผ ๋ณํํ์ฌ ์ฌ์ฉํ์๋ค.

    Rigidbody2D rigid;
    public float next_Move;
    void Start()
    {
        rigid = GetComponent<Rigidbody2D>();
        next_Move = 1;
        StartCoroutine(Move());
    }

    IEnumerator Move()
    {
        while (true)
        {
            rigid.velocity = new Vector2(next_Move * 2, rigid.velocity.y);

            //Platform Check
            Vector2 frontVec = new Vector2(rigid.position.x + next_Move / 1.8f, rigid.position.y);
            Debug.DrawRay(frontVec, Vector3.right * next_Move, new Color(0, 1, 0)); //์ด๋ก์
            RaycastHit2D rayHit = Physics2D.Raycast(frontVec, Vector3.down, 1, LayerMask.GetMask("platform"));
            if (rayHit.collider != null)
            {
                next_Move = -1 * next_Move;
            }
            yield return null;
        }
    }

<br>

## 6. ๊ตฌ๋ ํ๋ฉด

์ดํ ์ ์์ ์ผ๋ก ์ ๊ตฌ๋๋๋ ๋ชจ์ต์ด๋ค.

![gameScreen](https://user-images.githubusercontent.com/37824506/213096717-86c57679-ad1a-46e5-ab8f-e966373f47a3.gif)


<br>

***
    ๊ฐ์ธ ๊ณต๋ถ ๊ธฐ๋ก์ฉ ๋ธ๋ก๊ทธ์๋๋ค.
    ํ๋ฆฌ๊ฑฐ๋ ์ค๋ฅ๊ฐ ์์ ๊ฒฝ์ฐ ์ ๋ณดํด์ฃผ์๋ฉด ๊ฐ์ฌํ๊ฒ ์ต๋๋ค.๐