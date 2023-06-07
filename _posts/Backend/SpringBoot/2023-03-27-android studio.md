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

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁
 - 직렬화: 객체를 전송가능한 형태로 말아주는 것
 - 역직렬화: 그 데이터를 다시 자바 객체로 변환해주는 것
</div>

```
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main4)
        title = "포토샵"

        grapicView = MyGraphicView(this)
        pictureLayout.addView(grapicView)

        btt1.setOnClickListener{
            sX = sX + 0.2f
            sY = sY + 0.2f
            grapicView.invalidate()
        }
        btt2.setOnClickListener{
            sX = sX - 0.2f
            sY = sY - 0.2f
            grapicView.invalidate()
        }
        btt3.setOnClickListener{
            angle = angle + 20
            grapicView.invalidate()
        }
        btt4.setOnClickListener{
            color = color + 0.2f
            grapicView.invalidate()
        }
        btt5.setOnClickListener{
            color = color - 0.2f
            grapicView.invalidate()
        }
        btt6.setOnClickListener{
            bl = true
            grapicView.invalidate()
        }



        return3.setOnClickListener {
            finish()
        }
    }
    class MyGraphicView(context: Context) : View(context) {
        override fun onDraw(canvas : Canvas) {
            super.onDraw(canvas)

            var picture = BitmapFactory.decodeResource(resources,R.drawable.lena256)

            var picX = (this.width - picture.width) / 2f
            var picY = (this.height - picture.height) / 2f
            var cenX = this.width / 2f
            var cenY = this.height / 2f

            val paint = Paint()
            var bMask : BlurMaskFilter
            val array = floatArrayOf(color,0f,0f,0f,0f,
            0f,color,0f,0f,0f,
            0f,0f, color,0f,0f,
            0f,0f,0f,1f,0f)
            val cm = ColorMatrix(array)
            paint.colorFilter = ColorMatrixColorFilter(cm)

            bMask = BlurMaskFilter(30f,BlurMaskFilter.Blur.NORMAL)

            if(bl == true)
                paint.maskFilter = bMask


            canvas.scale(sX,sY,cenX,cenY)
            canvas.rotate(angle,cenX,cenY)


            canvas.drawBitmap(picture,picX,picY,paint)

            picture.recycle()
        }
    }
```

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁