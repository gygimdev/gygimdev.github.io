---
layout: default
title: 스프링 컨테이너와 빈
parent: 스프링 프레임워크(Spring Framework)
---

# 스프링 컨테이너와 빈
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

{: .highlight } 
스프링 컨테이너는 빈의 생성과 관리를 담당하며, 빈은 컨테이너에 등록되어 컨테이너가 제공하는 기능을 활용하면서 애플리케이션에서 필요한 객체로 사용됩니다.

## 스프링 컨테이너(Conatiner)

스프링컨테이너는 스프링프레임워크의 핵심 컴포넌트로서, 제어의 역전(IoC) 와 의존성 주입(DI) 라는 디자인패턴 기반으로 동작합니다.
또한 BeanFactory를 상속한 ApplicationContext의 구현체를 사용하여 빈의 라이프사이클을 관리하고, 빈의 생성, 설정, 조회, 의존성 주입 등의 기능을 제공합니다.
컨테이너는 XML, JavaConfig, 어노테이션 등 다양한 설정 방식을 지원하여 빈의 설정 정보를 읽어들이고, 빈의 인스턴스를 생성하고 관리합니다.
{: .fs-3 }

### 빈 팩토리(BeanFactory)
- 빈 팩토리(BeanFactory)는 스프링의 가장 기본적인 인터페이스로, 빈의 생성과 조회, 라이프사이클 관리 등의 핵심 기능을 제공합니다.
{: .fs-3 }

### 애플리케이션 컨텍스트(ApplicationContext)
- 애플리케이션 컨택스트(ApplicationContext) 는 빈 팩토리(BeanFactory)의 확장된 버전으로, 빈 팩토리의 모든 기능을 포함하면서 다양한 부가 기능을 추가로 제공합니다.
- 부가 기능으로는 빈의 생성과 조회, 라이프사이클 관리뿐만 아니라, 메시지 소스 처리, 이벤트 발행, AOP(Aspect-Oriented Programming), 트랜잭션 관리 등 다양한 기능을 제공합니다.
{: .fs-3 }

---

## 스프링 빈(Bean)
스프링 빈은 스프링 컨테이너가 생성하고 관리하는 객체를 말합니다.
빈은 스프링 컨테이너에 등록되어야만 컨테이너가 관리할 수 있으며, 컨테이너에 등록될 때, 빈의 스코프(scope)와 라이프사이클 관련 설정 등의 정보를 포함하고 있습니다. 
또한 빈은 컨테이너에서 관리되므로, 컨테이너의 장점인 라이프사이클 관리, 의존성 주입, AOP(Aspect-Oriented Programming) 등의 기능을 활용할 수 있습니다.
{: .fs-3 }

---

### 스프링프레임워크
스프링프레임워크는자동 구성(Auto Configuration) 기능을 제공하지 않기 때문에 AppConfig 를 작성해야합니다.
작성방법으로는 Xml 설정, JavaConfig 설정, Annotation 기반 설정이 있습니다.
이렇게 다양한 방법으로 설정된 빈의 메타정보를 읽어오기 위해 컨테이너는DefinitionReader를 통해 설정 정보를 읽고 BeanDefinition 을 생성합니다.
이를 기반으로 빈의 생성과 관리를 수행합니다.
{: .fs-3 }

### 스프링부트
자동 구성 기능을 제공하기 때문에별도의 설정 클래스를 작성할 필요가 없습니다.
@SpringBootApplication 어노테이션이 지정된 메인 클래스를 사용하면 어노테이션을 활용하여 설정과 컴포넌트 스캔, 자동 구성을 한 번에 처리합니다.
{: .fs-3 }
