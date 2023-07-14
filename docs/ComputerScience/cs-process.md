---
layout: default
title: 프로세스(Process)
parent: 컴퓨터공학(Computer Science)
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

# 프로세스(Process)
> 프로세스란 실행중인 프로그램을 말합니다.  
> 프로그램이 <u>메모리에 적재</u>되어 <u>CPU를 할당</u> 받아 실행되는 상태

## 프로그램을 실행시키는 방법
> 프로그램을 실행시키려면 메모리에 프로그램을 적재해야합니다.

CPU는 내부기억장치(메모리) 에서 프로그램을 읽어오기 때문에
프로그램을 실행시키려면 메모리에 프로그램을 적재해야합니다.

### CPU 는 메모리에서 어떻게 코드를 읽어올까?
> PC Register(Program Counter)를 사용해서 읽어옵니다.

CPU 는 PC Register 에 저장된 코드, 명령어를 보고 프로세스 연산을 실행합니다.
PC Register는 CPU 내부에 위치하고 있으며, 실행되어야할 프로세스의 코드, 명령어,
즉 메모리의 코드 영역(Code) 의 주소값을 가르키고 있습니다.
CPU 는 해당 주소값을 보고 프로세스를 실행시킵니다.

## 프로세스의 메모리 영역
> 메모리에 적재된 프로세스는 4가지 영역으로 나누어 집니다.  
> Code, Data, Stack, Heap

### 코드 영역(Code)
실제 프로그램 코드가 저장되는 영역

### 데이터 영역(Data)
전역변수가 저장되는 영역

### 스택 영역(Stack)
함수 호출시 생성되는 지역변수, 매개변수가 저장되는 곳

### 힙 영역(Heap)
동적 메모리 할당이 필요할 경우

## 프로세스의 상태
### 실행(running)
프로세스가 CPU를 점유하고 명령을 수행중인 상태

### 준비(ready)
CPU만 할당받으면 명령을 수행할 수 있는 준비된 상태

### 봉쇄(wait, sleep, blocked)
CPU를 할당받아도 명령을 실행할 수 없는 상태(I/O 작업을 기다리고 있는 경우)

