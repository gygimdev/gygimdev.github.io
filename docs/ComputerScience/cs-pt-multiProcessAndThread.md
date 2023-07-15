---
layout: default
title: 멀티프로세스와 멀티쓰레드의 차이
parent: 프로세스와 쓰레드
grand_parent: 컴퓨터공학(Computer Science)
nav_order: 6
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

# 멀티 프로세스와 멀티 쓰레드의 차이

## 멀티프로세스(Multi-Process)

### 장점
- 안정성: 프로세스는 각자의 메모리 영역을 가지고 있으므으로 각 프로세스에게 영향을 주지 않습니다.

### 단점
- 많은 메모리 공간을 차지합니다.
- 느림: 컨택스트 스위칭시 비용이 많이 듭니다.

## 멀티쓰레드(Multi-Thread)

### 장점
- 빠름: 컨텍스트 스위칭 비용이 저렴합니다.
- 메모리 공간을 프로세스와 고유함으로 적게 차지합니다.
### 단점
- 안정성: 프로세스내 메모리 공간을 공유하기 때문에 동기화 문제가 생길 수 있습니다.