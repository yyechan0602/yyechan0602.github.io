---
title:  "[Algorithm] 📈 최소 신장 트리 (MST, Minimum Spanning Tree)"
excerpt: "제한된 공간과 시간안에서 어떻게 데이터를 처리할지에 대한 알고리즘을 알아보자"
categories:
  - Type Of Algorithm
tags:
  - [최소 신장 트리, MST, Minimum Spanning Tree, Algorithm, Algorithm1]

toc: true
toc_sticky: true
 
date: 2023-06-26
last_modified_at: 2023-06-26
---

## 📖 최소 신장 트리(MST)

### 🍄 신장 트리(Spanning Tree)  

 - `연결 그래프`에서 그래프 탐색을 통해서 생기는 트리 엣지로 이루어진 `사이클을 갖지 않는 최소 부분 그래프`를 의미한다.
 - 그래프의 모든 정점이 서로 연결되어 있으면서, 순환구조가 반복되지 않는다.
 - 최소 부분이란 - 모든 정점을 포함하고, `간선의 개수 : 정점의 개수 -1`  

### 🍄 최소 신장 트리(MST, Minimum Spanning Tree)

- 최소 신장 트리란 `Spanning Tree`중에서 사용된 가중치의 값이 최소인 트리이다.
 
![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/90704864-fffc-468e-b63b-f3131f99c88c)

위와 같이 각 간선들의 길이의 합의 최소가 되는 연결 트리가 MST이다.  
이를 구하기 위해서는 2가지 알고리즘이 있다.  
 - Prim MST 알고리즘 (단계적 확장)
 - Kruskal MSt 알고리즘 (Greedy)

<br>

### 🍄 Prim MST
 - T 와 

<br>

### 🍄 Kruskal MST

그리디 알고리즘의 일종으로 보통 최소 힙을 이용하여 구한다.  
모든 그래프 정점을 최소힙에 넣음으로써 시작한다.

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/efb5a825-d7c1-4b4d-93d7-8d50002a22d5)

![image](https://github.com/yyechan0602/yyechan0602.github.io/assets/37824506/d3e17b61-0975-4f31-b267-c509e4340f9b)

### 🕸 4번의 사이클 판단 - Union & Find 활용

#### Union-Find
 - 서로소 집합을 표현할 때 사용하는 알고리즘  

#### 3가지 연산 
 - make-set(x)
   - 초기화, arr[i] = i
 - union(x, y)
   - 합치기
   - x, y가 속한 집합을 합치는 과정, 일반적으로 parent = x, child = y
   - O(N)
 - find(x)
   - 찾기, x가 속한 집합의 `최상위 노드 반환`
   - O(N-1), 트리의 높이와 시간 복잡도가 동일하다.
   - 경로 압축한 경우 상수 시간  


<details>
<summary> union-find 코드 구현 </summary>
<div markdown="1">

```java
#### make(){
  for(int i=0; i < N; i++){
    root[i] = i;
  }
}
```

#### union(x, y)
```java
void union(int from, int to){
  int fromRoot = find(from);
  int toRoot = find(to);

  if(fromRoot == toRoot) return false;
  else root[toRoot] = fromRoot;
  return true;
}
```

#### find(x)
```java
int find(int x){
  if(root[x] == x) {
    return x;
  } else{
    return find(root[x]); // 재귀를 이용하는 방식
    return root[x] = find(root[x]);
  }
}
```

</div>
</details>

## 🔗 관련 예시


tag:MST


<br>


***
    개인 공부 기록용 블로그입니다.
    틀리거나 오류가 있을 경우 제보해주시면 감사하겠습니다.😁