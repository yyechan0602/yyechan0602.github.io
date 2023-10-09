---
title:  "[Java] ☕ 자료구조 구현"
excerpt: "JAVA CS 지식 관련 정리"
categories:
  - Java
tags:
  - [JUnit, CS, Java]

toc: true
toc_sticky: true
 
date: 2023-10-08
last_modified_at: 2023-10-09
---

## 📖 LinkedList 구현  

- LinkedList가 무엇인지 학습하세요.
- 정수를 저장하는 ListNode 클래스를 구현하세요.
- ListNode add(ListNode head, ListNode nodeToAdd, int position) 메소드를 구현하세요.
- ListNode remove(ListNode head, int positonToRemove) 메소드를 구현하세요.
- boolean contains(ListNode head, ListNode nodeTocheck) 메소드를 구현하세요.

```java
package org.example;

public class LinkedList<E> { // 제너릭 클래스 Element의 약자
    Node<E> head;
    Node<E> tail;
    int count;

    public LinkedList() {
        this.head = new Node<>(null, null);
        this.tail = null;
        count = 0;
    }

    public void add(int index, E value) {
        if (index > count) {
            throw new ArrayIndexOutOfBoundsException();
        }

        count++;

        if (index == 0) {
            head = new Node<>(head, value); // head부분 앞에 새로운 노드를 만들고 해드의 주소값을 옮긴다

            if (tail == null) {
                tail = head;
            }
            return;
        }

        Node<E> node = head;
        for (int i = 0; i < index - 1; i++) {
            node = node.next;
        }

        node.next = new Node<>(node.next, value);

        if (node == tail) {
            tail = node.next;
        }
    }

    public E get(int index) {
        if(index>count) throw new IndexOutOfBoundsException();

        Node<E> node = head;
        for (int i = 0; i < index; i++) {
            node = node.next;
        }

        return node.value;
    }

    public void remove(int index) {
        if(index>count) throw new IndexOutOfBoundsException();
        count--;

        if (index == 0) {
            head = head.next; // head의 주소값을 다음 node로 옮긴다

            if (head.next == null) {
                tail = null;
            }
            return;
        }

        Node<E> node = head;
        for (int i = 0; i < index-1; i++) {
            node = node.next;
        }

        if (node.next == tail) {
            tail = node.next.next;
        }

        node.next = node.next.next;
    }

    public boolean contains() {
        return true;
    }
}

class Node<E> {
    Node<E> next;
    E value;

    public Node(Node<E> next, E value) {
        this.next = next;
        this.value = value;
    }

    public Node() {
        this.next = null;
        this.value = null;
    }
}
```


<br>

## 📖 Stack을 구현  

- int 배열을 사용하여 정수를 저장하는 Stack을 구현
- void push(int data) 메소드를 구현
- int pop() 메소드를 구현

```java
package org.example;

public class Stack<E> {
    LinkedList<E> linkedList;

    public Stack() {
        this.linkedList = new LinkedList<>();
    }

    public void push(E value) {
        linkedList.add(0, value);
    }

    public E pop() {
        E result = linkedList.get(linkedList.getSize() - 1);
        linkedList.remove(linkedList.getSize() - 1);

        return result;
    }
}
```

<br>

## 📖 앞서 만든 ListNode를 사용해서 Stack을 구현

- ListNode head를 가지고 있는 ListNodeStack 클래스를 구현
- void push(int data) 메소드를 구현
- int pop() 메소드를 구현 



<br>

## 📖 Queue 구현  

- 배열을 사용해서 한번.
- ListNode를 사용해서 한번.

<br>

***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁