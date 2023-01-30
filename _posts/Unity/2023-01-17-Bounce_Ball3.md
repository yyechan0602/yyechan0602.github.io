---
title:  "Bounce Game 3"
excerpt: "간단한 미니게임을 만들고 실행해보자"

categories:
  - Unity1
tags:
  - [Unity1, Bounce, Game]

toc: true
toc_sticky: true
 
date: 2023-01-17
last_modified_at: 2023-01-17
---

## 1. GameManager 만들기

<br>

플레이하고 있는 사람의 ID, 클리어 한 스테이지 개수, 플레이어 점수, DeathCount등을 기록하기 위한 `SingleTon`의 `GameManager`를 만들어준다.  
이를 위하여 `GameManager`이름의 `Script`를 만들어 준 뒤 다음 코드를 추가해주면 된다.

    public static Bounce_GameManager instance = null;
    public string ID;
    public int Current_Stage;
    public int Clear_Stage;
    public int Current_Score;
    public int Score;
    public int Death_Count;

    private void Awake()
    {
        if (instance == null) //instance가 null. 즉, 시스템상에 존재하고 있지 않을때
        {
            instance = this; //내자신을 instance로 넣어줍니다.
            DontDestroyOnLoad(gameObject); //OnLoad(씬이 로드 되었을때) 자신을 파괴하지 않고 유지
        }
        else
        {
            if (instance != this) //instance가 내가 아니라면 이미 instance가 하나 존재하고 있다는 의미
                Destroy(this.gameObject); //둘 이상 존재하면 안되는 객체이니 방금 AWake된 자신을 삭제
        }
    }

<br>

이제 게임 플레이 도중 `Scene`이 바뀌더라도 이 오브젝트는 유지되게 된다.  
이제 죽었을시 `DeathCount`를 카운트 하기 위하여 위하여 `Player` Script에 돌아가서 
`public GameObject Game_Manager;`를 추가해준뒤 다음 코드를 넣어둔다.

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

## 2. 코인 상호작용 구현하기

코인을 먹었을시 점수가 오르고 코인 오브젝트는 잠시 비활성화가 되여야만 한다. 또한 죽었을때 먹은 점수가 초기화되고, 코인이 다시 활성화가 되어야 한다.  

`Player`스크립트에 들어간후 `public GameObject Coins;` 코드를 넣어준다.

이를 위하여 방금전에 만든 `Death`함수에 다음 코드를 넣는다.

        for (int i = 0; i < Coins.transform.childCount; i++){
            Coins.transform.GetChild(i).gameObject.SetActive(true);
        }

<br>


이후 `Coin` Scripts를 만들어준후 다음 코드를 넣는다.

    public GameObject Game_Manager;
    private void OnTriggerEnter2D(Collider2D collision)
    {
        if (collision.gameObject.CompareTag("Player"))
        {
            gameObject.SetActive(false);
            Game_Manager.GetComponent<Bounce_GameManager>().Current_Score += 1;
        }
    }

Unity에 돌아가서 `Create Empty`를 만든후 이름을 `Coins`로 바꾼후 모든 `Coin`오브젝트를 넣어준다. 각각에 `Coin`들에게 위 스크립트를 넣어준다. 또 `Player` 오브젝트의 `Coins` 변수에 `Coins` 오브젝트를 끌어다가 넣어준다.

<br>

## 3. 몬스터 AI 구현하기

몬스터는 가만히 멈춰 있는게 아니라 스스로 생각을 가지고 움직여야 한다. 따라서 다음과 같이 3가지를 구현하기로 하였다. 

- 2초마다 앞으로 가기, 정지, 뒤로가기
- 진행방향에 발판이 없을 경우 방향 전환하기
- 방향을 전환하거나 뒤로 갈 때, 캐릭터가 좌우반전 되게 하기

<br>

이를 위하여 다음과 같이 `Raycast`를 사용하여 이동방향에 발판이 있는지 체크하였고, `Coroutine`를 사용하여, 2초마다 `Random.range`으로 `-1, 0, 1`의 방향이 무작위로 나오도록 하였다.

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
            Debug.DrawRay(frontVec, Vector3.down, new Color(0, 1, 0)); //초록색
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

## 4. 약한 발판 구현하기

약한 발판 같은 경우 밟으면 오브젝트가 사라지고, `Death`가 발동 시 다시 생겨야 한다. 따라서 `Coin`과 비슷하게 `Player` 스크립트에 `public GameObject Weak_Floors;`를 넣어준다.  

이후 `Death`함수에 다음 코드를 넣어준다.

    for (int i = 0; i < Weak_Floors.transform.childCount; i++){
        Weak_Floors.transform.GetChild(i).gameObject.SetActive(true);
    }

<br>

`Weak Floors Set`이름으로 `Empty Object`를 만들어준다. 이후 모든 `Weak Floor`를 `Weak Floors Set`에 넣어준다. `Player` 오브젝트의 `Weak_Floors`변수에 `Weak Floors Set`을 넣어준다.
    public GameObject Weak_Floors;

<br>

새로운 스크립트를 만든후 다음과 같은 코드를 넣어준뒤 `Weak FloorTop`오브젝트에 넣어주면 된다.

    private void OnCollisionEnter2D(Collision2D collision)
    {
        if(collision.collider.CompareTag("Player")){
            gameObject.transform.parent.gameObject.SetActive(false);
        }
    }

<br>

## 5. 움직이는 발판 구현하기

새 스크립트를 만든 후 `Moving Floor`에 넣어주면 된다.  
몬스터에서 사용한 `Raycast`를 변형하여 사용하였다.

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
            Debug.DrawRay(frontVec, Vector3.right * next_Move, new Color(0, 1, 0)); //초록색
            RaycastHit2D rayHit = Physics2D.Raycast(frontVec, Vector3.down, 1, LayerMask.GetMask("platform"));
            if (rayHit.collider != null)
            {
                next_Move = -1 * next_Move;
            }
            yield return null;
        }
    }

<br>

## 6. 구동 화면

이후 정상적으로 잘 구동되는 모습이다.

![gameScreen](https://user-images.githubusercontent.com/37824506/213096717-86c57679-ad1a-46e5-ab8f-e966373f47a3.gif)


<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁