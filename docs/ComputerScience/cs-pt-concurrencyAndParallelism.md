---
layout: default
title: 동시성과 병렬성
parent: 프로세스와 쓰레드
grand_parent: 컴퓨터공학(Computer Science)
nav_order: 3
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

# 동시성과 병렬성(Concurrency and Parallelism)

## 동시성(Concurrency)
> 여러 작업이 동시에 실행되는것처럼 보이는 개념

CPU 코어가 1개 일때, 여러 Process 를 짧은 시간동안 번갈아 가면서 연산을 하게 되는 시분할 시스템(time sharing system)으로 실행되는 것입니다.

## 병렬성(Parallelism)
> 실제로 여러 작업이 동시에 처리되는 개념

CPU 코어가 여러개일 때, 각각의 코어가 Process 를 연산함으로써, Process가 동시에 실행되는 것입니다.

