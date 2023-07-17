---
layout: default
title: 이진트리와 이진탐색트리
parent: 그래프(graph)
grand_parent: 알고리즘(Algorithm)
nav_order: 2
---

{: .no_toc }
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

# 이진트리와 이진탐색트리

## 이진트리(BT: Binary Tree)
> 이진트리는 각 노드의 자식수가 2개 이하로 구성되어 있는 트리입니다.


### 이진트리의 종류

#### 01. 정 이진 트리(Full Binary tree)
자식노드가 0 또는 2개인 이진 트리

#### 02. 완전 이진 트리(Complete Binary Tree)
왼쪽부터 채워져 있는 이진 트리

#### 03. 변질 이진 트리(Degenerate Binary Tree)
자식노드가 하나 밖에 없는 이진 트리

#### 04. 포화 이진 트리(Perfect Binary Tree)
모든 노드가 차 있는 이진 트리 
#### 05. 균형 이진 트리(Balanced Binary Tree)
왼쪽 하위 노드와 오른쪽  하위 노드의 높이가 1인 트리
* map, set 을 구현하는 레드브랙트리는 균형 이진 트리 중 하나입니다.

---

## 이진탐색트리(BST, Binary Search Tree)
> 이진 트리의 종류, 오른쪽 하위트리는 부모 노드의 값보다 큰 값,
왼쪽 하위트리는 부모 노드의 값보다 작은 값이 들어 있는 트리입니다.

탐색에 용이합니다. 예) 업앤다운 숫자 찾기

### 삽입 순서가 중요
> 1, 2, 3 으로 입력이 된다면 선형적 자료구조가 생성이됩니다.
이럴 경우 탐색이 용이하다는 장점을 살리지 못합니다.

삽입 순서에 따라서 노드를 회전시키는 등 방법을 통해서 균형잡히게 만들 수 있습니다.  
예) AVL트리, 레드블랙 트리



