---
layout: default
title: 스프링 MVC(Model View and Controller)
parent: 스프링 프레임워크(Spring Framework)
---

# 스프링 MVC
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

## 용어정리

### 01. 서블릿컨테이너(ServletContainer)
서블릿컨테이너는 서블릿의 생명주기를 관리하고, 클라이언트의 HTTP 요청을 받아서 해당 요청을 처리하는 서블릿을 실행시킨다. 

### 02. 디스패처서블릿(DispatcherServlet)
디스패처서블릿은 클라이언트로부터의 HTTP 요청을 받아 해당 요청을 처리할 핸들러를 찾아서 실행시키고 그 결과를 HTTP 응답으로 반환한다.

### 03. 핸들러매핑(HandlerMapping)
핸들러매핑은 스프링 프레임워크에서 클라이언트 요청에 대해 어떤 컨트롤러가 요청을 처리할지 결정하는 역할을 한다. 

### 04. 핸들러어댑터(HandlerAdapter)
핸들러어댑터는 핸들러맵핑을 통해 결정된 컨트롤러를 실행하는 역할을 한다.

### 05. 핸들러어댑터리스트(HandlerAdapterList)
핸들러어댑터는 다양한 컨트롤러 타입을 지원하기 위해 여러개가 존재한다. 이러한 어댑터의 목록을 관리하는 역할을 하는 곳이다.

### 06. 핸들러(Handler)
스프링 MVC에서 클라이언트의 요청을 처리하는 메서드를 말한다. 핸들러는 컨트롤러(Controller) 라고 부르며, 클라이언트의 요청을 받아 적절한 작업을 수행한 후에 응답을 반환하는 역할을 한다.

### 07. 뷰리졸버(ViewResolver)
뷰리졸버는 핸들러가 요청을 처리한 후 view 의 이름을 반환하게 되면, 해당 뷰이름을 실제 뷰 객체와 매핑시켜주는 역할을 한다.

### 08. 뷰(View)
핸들러가 처리한 결과 데이터를 적절한 형태로 랜더링하여 사용자에게 제공하는 역할을 한다.

---

## MVC 구조
![spring-mvc-structure.png](..%2F..%2Fstatic%2Fspring-mvc-structure.png)
### 01. 핸들러 조회
`디스패처서블릿(DispatcherServlet)`은 HTTP 요청이 오면, 해당 요청을 처리할 적절한 `핸들러(Handler)`를 `핸들러매핑(HandlerMapping)` 통해 찾는다.  
`핸들러매핑(HandlerMapping)`은 스프링MVC 프레임워크가 시작될때 자동으로 등록되고, 대표적인 핸들러로는 `RequestMappingHandlerMapping`이 있다.  

이렇게 핸들러매핑은 `@RequestMapping` 어노테이션을 사용해 URL 패턴과 `핸들러(Handler)`를 매핑하여 조회한다.  

또다른 핸들러매핑으로는 `BeanNameUrlHandlerMapping` 이 있으며, 이 매핑은 스프링 빈의 이름과 URL을 매핑하여 요청을 처리할 컨트롤러를 찾는다.
이렇게 `핸들러매핑(HandlerMapping)`은 `디스패처서블릿(dispatcherServlet)` 에 등록되어 HTTP요청이 들어오면 요청 URL 과 매핑된 컨트롤러를 찾아서 실행한다.

### 02. 핸들러어댑터 조회

`디스패처서블릿(DispatcherServlet)`은 `핸들러매핑(HandlerMapping)`을 통해 반환된 `핸들러(Handler)`와 함께 해당 핸들러를 처리할 수 있는 `핸들러어댑터(HandlerAdapter)` 를 찾는다.  
핸들러어댑터를 찾는 과정에서는 핸들러어댑터를 구현하는 모든 클래스들에 대해 하나씩 검사를 하고, 구현체중 `핸들러(Handler)`의 메서드와 일치하는 메서드를 가지고 있는 `핸들러어댑터(HandlerAdapter)`를 찾으면 그 핸들러 어댑터를 사용한다.

{: .note }
`핸들러어댑터(HandlerAdapter)`를 사용하여 핸들러를 호출하는 이유는 `핸들러(Handler)` 의 구현 방법이 다양할 수 있기 때문이다. 예를 들면 핸들러가 POJO(Plain Old Java Object) 로 구현되어 있거나, @Controller 어노테이션을 사용한 경우, 혹은 @RestController 애노테이션을 사용한 경우 등이 있을 수 있다. 이러한 다양한 컨트롤러 구현 방법에 대응하기 위해서 스프링MVC 는 `핸들러어댑터(HandlerAdapter)`를 사용하여 핸들러 객체의 메서드를 호출한다.


### 03. 핸들러 실행 
`핸들러어댑터(HandlerAdapter)` 를 통해 핸들러(컨트롤러) 실행되고 `모델앤뷰(ModelAndView)` 객체를 반환한다.
`모델앤뷰(ModelAndView)` 객체는 `뷰이름(viewName)` 과 `데이터(model)`를 속성으로 가지고 있다. 이 속성은 이후에 `ViewResolver` 를 통해 실제 뷰 객체를 찾을 때 사용되고 모델 속성은 서버에서 클라이언트로 보내는 데이터(model and viewName)를 담고 있다.

### 04. 뷰 객체 조회
`디스패처서블릿(DispatcherServlet)`은 반환된 `모델앤뷰(ModelAndView)` 객체를 사용해 `뷰리졸버(ViewResolver)`에서 실제 뷰 객체를 찾는다.

### 05. 응답생성
`디스패처서블릿(DispatcherServlet)`은 `뷰리졸버(ViewResolver)` 를 통해 찾은 실제 뷰 객체와 `핸들러(Handler)`의 실행 결과인 Model(데이터)를 이용하여 최종적인 응답결과를 생성하는 작업을 수행한다.

---

