---
title:  "[Bounce Game] π₯ λ―Έλκ²μ λ§λ€κΈ° 5"
excerpt: "κ°λ¨ν λ―Έλκ²μμ λ§λ€κ³  μ€νν΄λ³΄μ"

categories:
  - Unity1
tags:
  - [Unity1, Bounce, Game]

toc: true
toc_sticky: true
 
date: 2023-01-19
last_modified_at: 2023-01-19
---

## 1. SingleTon κ΄λ ¨ λ¬Έμ 

<br>

μ§κΈκΉμ§ μ½λλ₯Ό μ§  ν μ€νμ μν€λ©΄ λ€λ₯Έ `Scene`μμ λ§λ  `SingleTon`μ μΈμνμ§ λͺ»νλ λ¬Έμ κ° λ°μνλ€.  
μ΄λ₯Ό ν΄κ²°νκΈ° μνμ¬ `GameManager`λ₯Ό μ¬μ©νλ `Object`λ€μ λ€μκ³Ό κ°μ μμ μ ν΄μ£Όμλ€.
`GameManager`λ₯Ό μ§μ  λ£μ΄μ£Όλ κ²μ΄ μλλΌ `Script`μμΌλ‘ μμμ μ°Ύλ μμΌλ‘ μμ μ νμ¬μ λ€λ₯Έ `Scene`μμ μ¨ `GameManager`λΌλ `Tag`κ° λκ°μ μ μ°Ύμ μ μλλ‘ νμλ€. μ΄ν λͺ¨λ  `GameManager`μ€λΈμ νΈμ `Tag`λ‘ `GameManager`λ₯Ό λ£λλ€.

    public GameObject Game_Manager;

    void Start()
    {
        Game_Manager = GameObject.FindGameObjectWithTag("GameManager");
    }

μ΄ν κ²μ λμ€μ `MainMenu`λ‘ κ°κΈ° μνμ¬ `Player` μ€ν¬λ¦½νΈμ `UI_Manager`μ `SceneManager.LoadScene("MainMenu");` μ½λλ₯Ό λ£μ΄μ£Όλ©΄ λλ€.

<br>

## 2. DB μ°λνκΈ°


<br>

***
    κ°μΈ κ³΅λΆ κΈ°λ‘μ© λΈλ‘κ·Έμλλ€.
    νλ¦¬κ±°λ μ€λ₯κ° μμ κ²½μ° μ λ³΄ν΄μ£Όμλ©΄ κ°μ¬νκ² μ΅λλ€.π