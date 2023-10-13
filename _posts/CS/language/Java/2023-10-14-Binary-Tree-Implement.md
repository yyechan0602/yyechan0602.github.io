---
title:  "[Java] ☕ Binary Tree 구현"
excerpt: "JAVA CS 지식 관련 정리"
categories:
  - Java
tags:
  - [JUnit, CS, Java]

toc: true
toc_sticky: true
 
date: 2023-10-14
last_modified_at: 2023-10-14
---


## 📖 Binary Tree 구현

- int 값을 가지고 있는 이진 트리를 나타내는 Node 라는 클래스를 정의하세요.
- int value, Node left, right를 가지고 있어야 합니다.
- BinrayTree라는 클래스를 정의하고 주어진 노드를 기준으로 출력하는 bfs(Node node)와 dfs(Node node) 메소드를 구현하세요.
- DFS는 왼쪽, 루트, 오른쪽 순으로 순회하세요  

<br>

```java
package org.example.functions;

import java.util.LinkedList;
import java.util.Queue;
import java.util.Stack;

public class BinaryTree {
    node root;

    public BinaryTree() {

        node node17 = new node(17, null, null);
        node node13 = new node(13, null, null);
        node node12 = new node(12, null, null);
        node node8 = new node(8, null, node17);
        node node7 = new node(7, null, null);
        node node6 = new node(6, node12, node13);
        node node5 = new node(5, null, null);
        node node4 = new node(4, node8, null);
        node node3 = new node(3, node6, node7);
        node node2 = new node(2, node4, node5);
        node node1 = new node(1, node2, node3);

        this.root = node1;
    }

    public void BFS() {
        System.out.println("===BFS 시작===");
        Queue<node> q = new LinkedList<>();
        q.add(root);

        while(!q.isEmpty()){
            node curNode = q.poll();

            if(curNode==null) continue;

            q.add(curNode.left);
            q.add(curNode.right);
            System.out.println(curNode.value);
        }
        System.out.println("===BFS 끝===");
    }

    public void DFS(){
        System.out.println("===DFS 시작===");
        Recursive(root);
        System.out.println("===DFS 끝===");
    }

    public void Recursive(node node){
        if(node == null) return;

        Recursive(node.left);
        System.out.println(node.value);
        Recursive(node.right);
    }
}

class node {
    int value;
    node left;
    node right;

    public node(int value, node left, node right) {
        this.value = value;
        this.left = left;
        this.right = right;
    }

    public node() {
        this.left = null;
        this.right = null;
    }
}
```

<br>

### 🍄 테스트

```
public class Testing {

    @Test
    public void test(){
        BinaryTree bt = new BinaryTree();

        bt.BFS();
        bt.DFS();
    }
}
```

다음과 같이 잘 작동하는 모습이다.  

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/7942f768-5aac-472d-b877-188860c56e39)

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/46f6a441-be5d-4ce8-982e-e1df6a66cc41)


***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁