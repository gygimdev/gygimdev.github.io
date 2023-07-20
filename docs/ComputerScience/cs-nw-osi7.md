---
layout: default
title: OSI 7 계층 & TCP/IP 4 계층
parent: 네트워크
grand_parent: 컴퓨터공학(Computer Science)
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

# OSI 7 계층과 TCP/IP 4 계층

## 캡슐화 & 역캡슐화
### 캡슐화
정보를 header 에 포함시켜서 하위 계층으로 전송하는 것

### 역캡슐화
캡슐화된 정보를 역순으로 꺼내면서 원래의 데이터를 얻는 과정

## 3 way handshake
TCP/IP 프로토콜로 통신하기 전 정확한 정보 전송을 위해 대상 컴퓨터와 세션을 연결하는 과정입니다.
1. SYN 패킷을 보낸다.
2. ACK + SYN 패킷을 받는다.
3. ACK 패킷을 다시 보낸다
4. 연결완료

## 4 way handshake
TCP 연결을 종료하는 과정은 4 way handshake 를 통해서 이루어집니다.
1. FIN 패킷을 보냄
2. ACK 패킷을 받음
3. FIN 패킷을 받음
4. ACK 패킷을 보냄

## OSI 7 계층
네트워크 통신을 표준화한 모델입니다.
하지만 실무적으로 이용하기 복잡해서 TCP/IP 4 계층이 사용되고 있습니다.

### 07. 응용 계층
사용자-소프트웨어간 소통을 담당하는 계층  
HTTP, SSH, SMTP 프로토콜을 활용한 사용자 UI 입력/출력

### 06. 표현 계층
데이터의 표현 방식을 결정하는 역할
데이터 인코딩 디코딩을 수행, 포장, 암호화, 압축

### 05. 세션 계층
프로세스간 호스트 연결 유지  
TCP/IP 세션 체결(API, Socket 등)


### 04. 전송 계층
전송 방식 결정(TCP/UDP)  
패킷 분할 및 재조립

### 03. 네트워크 계층
데이터를 목적지까지 빠르게 전달하는 역할(라우팅을 담당)  
IP 할당, 데이터의 최적 경로를 선택

### 02. 데이터 계층
통신의 흐름을 관리하는 역할  
프레인 전송(오류감지, 흐름제어)

### 01. 물리 계층
전기 신호를 데이터로 변형
binary 데이터를 케이블을 통해 전송

## TCP/IP 4 계층

### TCP
TCP는 연결/신뢰성 프로토콜입니다. 연결지향적이기 때문에 3way handshaking 을 하여
두 호스트의 전송 계층 사이에서 논리적 연결을 설정합니다.
신뢰성을 보장하기 때문에 header 가 더 크고 속도가 느립니다.

### UDP
UDP는 비연결성 프로토콜입니다. 그래서 3way handshaking 과정이 없습니다.
하지만 header의 크기가 작아서 빠른 수신이 가능합니다.

### 01. 응용계층
사용자-소프트웨어간 소통을 담당하는 계층  
HTTP, SSH, SMTP 등

### 02. 전송계층
통신 노드간 신뢰성 있는 데이터 전송을 보장하는 계층
TCP/UDP 

#### TCP
TCP 로 보내는 패킷을 segment  
3단계: setup, transfer, termination 단계를 거칩니다.
흐름제어: 데이터의 전송속도와 수신 속도를 맟추는 작업
오류제어: 회손된 segment 감지 및 재전송

#### UDP
UDP 로 보내는 패킷을 datagram

### 03. 인터넷 계층
패킷을 최종 목적지까지 라우팅 하는 계층
IP, ARP 프로토콜 등이 사용됩니다.

### 04. 네트워크 엑세스/인터페이스 계층
데이터를 전기신호로 변환, MAC 주소를 사용해 알맞은 기기로 데이터를 전달
Ethernet, Wi-Fi 프로토콜 등이사용됩니다.

