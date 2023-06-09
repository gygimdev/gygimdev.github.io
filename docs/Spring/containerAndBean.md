---
layout: default
title: 스프링 빈과 컨테이너
parent: 스프링(Spring)
nav_order: 3
---

# 스프링 빈(Bean) 그리고 컨테이너(container)
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

## 스프링 빈(Spring Bean)
스프링프레임워크에서는 웹 애플리케이션을 구동하기 위해 자바 객체를 사용하는데요.
이 객체들을 스프링 빈(Bean) 이라고 합니다.
스프링 빈을 사용하기 위해서는 스프링컨테이너에 등록해주어야 하는데요.
이때 스코프 설정을 통해 스프링빈이 어떻게 생성되고 관리, 공유될지를 설정해줄 수 있습니다.
{: .fs-3 }

---

## 스프링 컨테이너(Spring Container)
스프링컨테이너는 IoC 컨테이너라고도 불리며, 이곳에서 스프링 빈을 등록하여 빈의 생명주기를 관리합니다.
{: .fs-3 }

---

## 스프링 빈의 생명주기(Bean Lifecycle)
스프링 빈의 생명주기는 네 가지 단계가 있습니다.
{: .fs-3 }

### 단계 1: 인스턴스화
인스턴스화 단계에서는 빈 객체들이 생성되는 시점입니다.
{: .fs-3 }

### 단계 2: 의존성주입
의존성 주입단계에서는 생성된 객체들의 의존성이 주입되는 시점입니다.
{: .fs-3 }

### 단계 3: 초기화
초기화 단계에서는 객체들이 실제로 사용되기 전, 남은 설정들을 콜백메서드를 통해 설정되는 단계입니다.
보통 데이터베이스 연결이나, 네트워킹 연결등 무거운 작업이 실행됩니다.
{: .fs-3 }

#### 콜백메서드:
초기화 단계에서는 콜백 메서드를 통해 초기화 전, 후로 특정 작업을 할수있는 방법을 제공합니다.
{: .fs-3 }

1. 인터페이스 방법(InitializingBean, DisposableBean)
   {: .fs-3 }
2. 메서드 방법(initMethod, destoryMethod)
   {: .fs-3 }
3. 어노테이션 방법(PostConstruct, PreDestory)
   {: .fs-3 }

### 단계 4: 소멸
스프링빈이 종료되는 단계입니다.
{: .fs-3 }

---

## 빈 스코프(Bean Scope)
스프링 컨테이너 내에서 스프링빈이 생성될때 어떻게 생성이 되고, 관리되며,
공유될지를 @Scope 스코프 어노테이션을 통해 설정할 수 있습니다.
{: .fs-3 }

### 싱글톤(singleton)
스프링 빈의 기본 스코프 설정은 싱글톤입니다.
싱글톤으로 생성된 스프링빈은 컨테이너 안에서 한번만 생성이되며 모든 자원에서 동일하게 공유됩니다.
{: .fs-3 }

### 프로토타입(prototype)
스프링 컨테이너 내에서 생성요청이 올때마다 새로운 인스턴스가 만들어집니다.
스프링컨테이너에서 생성, 의존성 주입, 초기화단계 까지만 관리해주고 그 이후로는 관리하지 않습니다.
{: .fs-3 }

### 리퀘스트(request)
HTTP 요청 마다 생성되며, 같은 요청 안에서 동일한 인스턴스가 공유됩니다.
{: .fs-3 }

### 세션(session)
세션과 생명주기를 같이합니다.
{: .fs-3 }

### 애플리케이션(application)
서블릿컨텍스트와 함께 생명주기를 같이합니다.
{: .fs-3 }

---

### 스프링에서 빈(Bean)을 싱글톤으로 사용하는 이유:
스프링 컨테이너에 등록된 빈은 기본적으로 싱글톤으로 관리됩니다.
이렇게 관리하는 이유는 대규모 트래픽을 처리해야하기 때문인데요.
{: .fs-3 }

예를 들어 한개의 요청당 10개의 빈이 만들어진다고 가정했을때
1초에 10개의 요청이 온다면 100개의 새로운 객체가 만들어지게 됩니다.
{: .fs-3 }

요청마다 빈이 생성된다면 서버에 부하가 걸리기 때문에 빈을 싱글톤으로 관리하는 것이 권장됩니다.
싱글톤으로 빈을 관리하면 대규모 트래픽 처리시 여러 쓰래드가 빈을 공유하여 작업을 처리할 수 있습니다.
{: .fs-3 }

