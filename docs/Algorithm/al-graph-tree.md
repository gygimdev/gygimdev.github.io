---
layout: default
title: 트리(Tree)
parent: 그래프(graph)
grand_parent: 알고리즘(Algorithm)
nav_order: 1
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

---
# 트리(Tree Data Structure)
나무를 뒤집은 모양을 가지고 있는 자료구조입니다.

              [1](루트, 부모노드)        | level 1
              / \
    (내부노드)[2]  [3](리프, 자식노드)     | level 2
           /              
        [4]                          | level 3
       /   \
     [5]   [6]                       | level 4

[2]는 [4] 의 부모 노드이다.  
[6]은 [5] 의 자식 노드이다.  
루트노드: 1  
서브트리: 4, 5, 6
리프노드: 3, 5, 6


## 특징
- 자식노드와 부모노드
- 계층구조
- 무방향
- 싸이클 X


