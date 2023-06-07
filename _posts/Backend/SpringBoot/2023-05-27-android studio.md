---
title:  "[SpringBoot] 💡 JPA란?"
excerpt: "JPA란 무엇이고, 데이터베이스 어떤 상관관계가 있는지 알아보자"
categories:
  - SpringBoot
tags:
  - [JPA, SpringBoot]

toc: true
toc_sticky: true
 
date: 2023-05-26
last_modified_at: 2023-05-26
---

## 📘  JPA(Java Persistence API)

`JPA(Java Persistence API)` 는 자바에서 `ORM` 기술 표준으로 사용되는 인터페이스의 모음이다.  

<div class="notice--warning" markdown="1">
직렬화와 역직렬화란?
---
title:  "[SpringBoot] 💡 JPA란?"
excerpt: "JPA란 무엇이고, 데이터베이스 어떤 상관관계가 있는지 알아보자"
categories:
  - SpringBoot
tags:
  - [JPA, SpringBoot]

toc: true
toc_sticky: true
 
date: 2023-03-26
last_modified_at: 2023-03-26
---

## 📘  JPA(Java Persistence API)

`JPA(Java Persistence API)` 는 자바에서 `ORM` 기술 표준으로 사용되는 인터페이스의 모음이다.  

<div class="notice--warning" markdown="1">
**ORM**이란?

`Object Relational Mapping` 이란 뜻으로, 
</div>

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁---
title:  "[SpringBoot] 💡 JPA란?"
excerpt: "JPA란 무엇이고, 데이터베이스 어떤 상관관계가 있는지 알아보자"
categories:
  - SpringBoot
tags:
  - [JPA, SpringBoot]

toc: true
toc_sticky: true
 
date: 2023-03-26
last_modified_at: 2023-03-26
---

## 📘  JPA(Java Persistence API)

`JPA(Java Persistence API)` 는 자바에서 `ORM` 기술 표준으로 사용되는 인터페이스의 모음이다.  

<div class="notice--warning" markdown="1">
**ORM**이란?

`Object Relational Mapping` 이란 뜻으로, 
</div>

```
class MainActivity : AppCompatActivity() {
    val names = mutableListOf<String>()
    val phones = mutableListOf<String>()
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        val binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)
        title = "전화번호부"

        val path: File = getDatabasePath("testdb")
        if (path.exists().not()) {
            val db = openOrCreateDatabase("testdb", Context.MODE_PRIVATE, null)
            db.execSQL(
                "create table USER_TB (_id integer primary key autoincrement, name text not null, phone text)"
            )
            db.close()
        }

        binding.resultList.layoutManager = LinearLayoutManager(this)
        val adapter = ResultAdapter(names, phones)
        binding.resultList.adapter = adapter
        binding.resultList.addItemDecoration(
            DividerItemDecoration(
                this,
                LinearLayoutManager.VERTICAL
            )
        )

        binding.searchAllBtn.setOnClickListener {
            val db = openOrCreateDatabase("testdb", Context.MODE_PRIVATE, null)
            val cursor = db.rawQuery("select name, phone from USER_TB", null)
            names.clear()
            phones.clear()
            while (cursor.moveToNext()) {
                names.add(cursor.getString(0))
                phones.add(cursor.getString(1))
            }
            db.close()
            adapter.notifyDataSetChanged()
        }

        binding.insertBtn.setOnClickListener {
            val db = openOrCreateDatabase("testdb", Context.MODE_PRIVATE, null)

            db.execSQL(
                "insert into USER_TB(name, phone) values(?, ?)",
                arrayOf(binding.inputName.text.toString(), binding.inputPhone.text.toString())
            )

            db.close()
        }

        binding.deleteBtn.setOnClickListener {
            val db = openOrCreateDatabase("testdb", Context.MODE_PRIVATE, null)
            db.execSQL("delete from USER_TB")

            db.close()

        }

    }
}

class ResultHolder(val binding: ResultItemBinding) : RecyclerView.ViewHolder(binding.root)

class ResultAdapter(val names: MutableList<String>, val phones: MutableList<String>) :
    RecyclerView.Adapter<ResultHolder>() {
    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ResultHolder =
        ResultHolder(
            ResultItemBinding.inflate(
                LayoutInflater.from(parent.context),
                parent, false
            )
        )

    override fun getItemCount(): Int = names.size + 1

    override fun onBindViewHolder(holder: ResultHolder, position: Int) {
        if (position == 0) {
            holder.binding.name.text = "[[ NAME ]]"
            holder.binding.phone.text = "[[ PHONE ]]"
        } else {
            holder.binding.name.text = names[position - 1]
            holder.binding.phone.text = phones[position - 1]
        }
    }
}

```

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁
 - 직렬화: 객체를 전송가능한 형태로 말아주는 것
 - 역직렬화: 그 데이터를 다시 자바 객체로 변환해주는 것
</div>

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁