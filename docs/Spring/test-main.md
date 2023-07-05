---
layout: default
title: 스프링테스트(JUnit)
parent: 스프링(Spring)
has_children: true
nav_order: 5
---

## 테스트

## TDD
에자일 개발 방식 중 하나, 테스트를 먼저 설계하고 코드를 작성하는 방식.
코드를 설계할때 단계적 목표에 대해서 설정하고 진행하고자 하는 것에 대한 결정 방향의 갭을 줄이고자 함
최초 목표에 맞춘 테스트를 구축하여 그에 맞게 코드를 설계하기 때문에 보다 적은 의견 충돌을 기대할 수 있다.

## 테스트 코드의 목적
코드의 안정성을 높일 수 있다.
기능을 추가하거나 변경되는 과정에서 발생할 수 있는 Side-Effect 를 줄일 수 있다.
해당 코드가 작성된 목적을 명확하게 표현할 수 있다.
코드에 불필요한 내용이 들어가는 것을 줄일 수 있다.

## JUnit
자바 진영의 대표적인 테스트 프레임워크

## 단위 테스트(Unit Test)
코드의 특정 모듈이 의도된 대로 동작하는지 테스트 하는 절차를 의미
모든 함수와 메소드에 대한 각각의 테스트 케이스를 작성하는 것

## JUnit 모듈

### JUnit Jupiter
TestEngine API 구현체로 JUnit5 를 구현하고 있음. 테스트의 실제 구현체는 별도 모듈을 


### JUnit Platform


## Junit 생명 주기
- @Test: 테스트용 메서드를 표현하는 어노테이션
- @BeforeEach: 각 테스트 메서드가 실행되기 전에 실행되어야하는 메서드를 표현
- @AfterEach: 각 테스트 메서드가 시작된 후 실행되어야하는 메서드를 표현
- @BeforeAll: 전체 테스트 시작 전에 실행되어야 하는 메서드를 표현, 제일먼저 시작(static 처리 필요)
- @AfterAll: 전체 테스트 종료 후에 실행되어야 하는 메서드를 표현, 제일 나중에 시작(static 처리 필요)

## JUnit 어노테이션 종류

### @SpringBootTest
- 통합 테스트 용도로 사용됨
- @SpringBootApplication 을 찾아 하위의 모든 Bean 을 스캔하여 로드함
- 그 후 Test 용 Application Context를 만들어 Bean 을 추가하고, MockBean 을 찾아 교체

### @ExtendWith
- JUnit4 에서 @RunWith 로 사용되던 어노테이션이 ExtendWith 로 변경됨
- @ExtendWith는 메인으로 실행될 Class 를 지정할 수 있음
- @SpringBootTest는 기본적으로 @ExtendWith 가 추가되어 있다.

### @WebMvcTest(Class명.class)
- ()괄호 안에 작성된 클래스만 실제로 로드하여 테스트를 진행
- 매개변수를 지정해주지 않으면 @Controller, @RestController, @RestControllerAdvice 등
  컨트롤러와 연관된 Bean 이 모두 로드된다.
- 스프링의 모든 Bean 을 로드하는 @SpringBootTest 대신 컨트롤러 관련 코드만 테스트할 경우 사용

### @Autowired about Mockbean
- Controller 의 API 를 테스트하는 용도인 MockMvc 객체를 주입 받음
- perform() 메서드를 활용하여 컨트롤러의 동작을 확인할 수 있음
- .andExpect(), andReturn() 등의 메서드를 같이 활용함

### @MockBean
- 테스트할 클래스에서 주입 받고 있는 객체에 대해 가짜 객체를 생성해주는 어노테이션
- 해당 객체는 실제 행위를 하지 않음
- given() 메서드를 활용하여 가짜 객체의 동작에 대해 정의하여 사용할 수 있음

### @AutoConfigureMockMvc
- spring.test.mockmvc 의 설정을 로드하면서 MockMvc의 의존성을 자동으로 주입
- MockMvc 클래스는 REST API 테스트를 할 수 있는 클래스

### @Import
- 필요한 Class들을 Configuration 으로 만들어 사용할 수 있음
- Configuration Component 클래스도 의존성 설정할 수 있음
- Import된 클래스는 주입으로 사용 가능

## 통합테스트
통합테스트는 여러 기능을 조합하여 전체 비즈니스 로직이 제대로 동작하는지 확인하는 것을 의미
통합 테스트의 경우, @SpringBootTest 어노테이션을 사용하여 진행
- @SpringBootTest는 @SpringBootApplication 을 찾아가서 모든 Bean 을 로드하게 됨
- 이 방법을 대규모 프로젝트에서 사용할 경우, 테스트를 실행할 때마다 모든 빈을 스캔하고 로드하는 작업이 반복되어 매번 무거운 작업을 수행해야 함
- 이런 무거운 방법을 피하기 위해서 '단위테스트' 를 진행한다

## 단위 테스트
단위 테스트는 프로젝트에 필요한 모든 기능에 대한 테스트를 각각 진행하는 것을 의미
일반적으로 스프링 부트에서는 'org.springframework.boot:spring-boot-starter-test' 디펜던시만으로 의존성을 모두 가질 수 있음

F.I.R.S.T 원칙
- Fast: 테스트 코드의 실행은 빠르게 진행되어야 한다.
- Independent: 독립적인 테스트가 가능해야 한다.
- Repeatable: 테스트는 매번 같은 결과를 만들어야 한다.
- Self-Validating: 테스트는 그 자체로 실행하여 결과를 확인할 수 있어야 한다.
- Timely: 단위 테스트는 비즈니스 코드가 완성되기 전에 구성하고 테스트가 가능해야 한다.(코드가 완성되기 전부터 테스트가 따라와야 한다는 TDD의 원칙을 담고 있음)
