---
layout: default
title: 쓰레드(Thread)
parent: 컴퓨터공학(Computer Science)
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

---


# 쓰레드(Thread)
> 쓰레드란 하나의 프로세스 안에서 실행되는 작업 단위

프로세스가 실행될때 실제 작업을 쓰레드가 수행합니다.
모든 프로세스에는 한개 이상의 쓰레드가 있으며,
두개 이상의 쓰레드를 가지는 프로세스를 멀티쓰레드 프로세스(multi-threaded process) 라고 합니다.

## 특징
- 독립적인 Stack 메모리 영역을 가지고 있다.
- 쓰레드가 속해있는 프로세스의 메모리 영역(Code, Data, Heap) 영역을 공유한다.

