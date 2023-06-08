---
layout: default
title: 스프링 MVC(Model View and Controller)
parent: 스프링(Spring)
nav_order: 5
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

## 모델-뷰-컨트롤러(MVC: Model-View-Controller)
우리는 하나의 조직을 효율적으로 운영하기 위해서 각 부서를 만들고 역할과 책임을 부여해 관리합니다.
웹 애플리케이션을 만들때도 코드의 역할과 책임을 나누어 관리할 수 있다면 우리는 견고한 웹 애플리케이션을 만들 수 있을 것입니다.
{: .fs-3 }

이미 다양한 소프트웨어 아키텍쳐 패턴이 존재하지만 스프링에서는 모델-뷰-컨트롤러(Model, View, Controller) 기반의 패턴인 스프링MVC 를 제공합니다.
{: .fs-3 }

![mvc.png](..%2F..%2Fstatic%2Fspring%2Fmvc.png)
스프링MVC 는 웹 애플리케이션 구조를 세 가지 주요 컴포넌트로 분리하여 개발하는 아키텍쳐 패턴인데요.
각 컴포넌트는 다음과 같은 역할을 수행합니다.
{: .fs-3 }

### 1.모델(Model)
비즈니스 로직을 처리하고 데이터를 저장, 관리하는 역할을 합니다.
주로 비즈니스 로직처리, 데이터의 가공, 유효성 검증, 데이터베이스 연동 등의 역할을 수행합니다.
{: .fs-3 }

### 2.뷰(View)
사용자에게 결과를 표시하는 역할을 합니다.
주로 HTML, JSP, Thymeleaf 등의 템플릿 엔진을 사용하여 데이터를 동적으로 표시합니다.
{: .fs-3 }

### 3.컨트롤러(Controller)
사용자의 요청을 처리하고 모델(Model)과 뷰(View)를 연결하는 역할을 합니다.
클라이언트로부터의 요청을 받아 해당 요청을 처리하기 위해 필요한 비즈니스 로직을 실행하고, 결과 데이터를 모델(Model)에 저장하고, 적절한 뷰(View)를 선택하여 클라이언트에 응답합니다.
{: .fs-3 }

---

## 스프링 MVC 구조와 흐름
모델-뷰-컨트롤러 패턴에 대해서 간단하게 알아보았으니 스프링MVC 를 자세히 살펴봅시다. 스프링MVC 는 dispatcherServlet 중심으로 동작합니다.
{: .fs-3 }

![springMvc.png](..%2F..%2Fstatic%2Fspring%2FspringMvc.png)

### 디스패처서블릿(DispatcherServlet)
사용자의 요청이 들어오면 dispatcherServlet 이 제일먼저 요청을 받아드립니다. 
요청을 받은 디스패처서블릿은 요청처리를 컨트롤러에게 위임해야하는데요.
스프링에서는 컨트롤러를 구현할 수 있는 방법이 다양하기 때문에
적절한 핸들러메서드를 찾고 실행시키려면
"핸들러매핑", "핸들러어댑터"의 도움이 필요합니다.
{: .fs-3 }

### 핸들러매핑(HandlerMapping)
핸들러매핑은 요청 URL 과 사전에 등록된 매핑규칙을 사용해 핸들러를 찾아내는데요.
예를 들면 @RquestMapping 어노테이션을 사용하였다면
`RequestMappingHanlderMapping` 규칙을 통해
요청 URL 과 매핑되는 어노테이션이 달린 핸들러를 찾아낼 수 있습니다.
{: .fs-3 }
```java

// "/users/1"로 요청이 들어온다면 getUser 를 찾아낸다.
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public String getUser(@PathVariable int id, Model model) {
        // 핸들러 메서드의 로직이 들어갑니다.
    }
}

```
이 밖에도 핸들러매핑은 요청을 처리할 컨트롤러를 찾기 위해 다양한 매핑 전략을 사용합니다.
{: .fs-3 }


### 핸들러어댑터(HandlerAdaptor)
핸들러어댑터는 핸들러매핑을 통해 찾은 핸들러매서드를 실행시키는 역할을 합니다. 
핸들러어댑터를 사용해 핸들러메서드를 실행시키는 이유는 앞서 설명한 바와 같이
핸들러메서드의 구현 방법이 다양할 수 있기 때문입니다.
{: .fs-3 }

@Controller 어노테이션을 사용한 경우,
혹은 @RestController 애노테이션을 사용한 경우 등 다양한 구현방법이 있을 수 있는데요.
이러한 다양한 컨트롤러 구현 방법에 대응하기 위해 스프링은 핸들러어댑터를 사용합니다.
{: .fs-3 }

```java
public class RequestMappingHandlerAdapter implements HandlerAdapter {

    @Override
    public boolean supports(Object handler) {
        return handler instanceof HandlerMethod;
    }

    @Override
    public ModelAndView handle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        HandlerMethod handlerMethod = (HandlerMethod) handler;
        Method method = handlerMethod.getMethod();

        // 요청과 매개변수를 적절히 처리하여 핸들러 메서드를 실행
        Object result = method.invoke(handlerMethod.getBean(), extractMethodArguments(request, response, handlerMethod));

        // 결과를 ModelAndView 객체로 변환
        ModelAndView modelAndView = convertToModelAndView(result);

        return modelAndView;
    }
}
```
위 예시는 @RequestMapping 어노테이션이 적용된 핸들러메서드를 실행시키고 요청을 처리하는 역할을 합니다.
supports 메서드에서 인자로 받은 handler 가 HandlerMethod(요청을 처리하는 메서드를 포함한 컨트롤러 객체메타정보) 의 타입인지 확인하고
결과가 참이라면 handle 메서드에서 핸들러메서드를 실행시킵니다.
{: .fs-3 }

### 핸들러메서드(Controller)
핸들러메서드 혹은 컨트롤러의 요청이 완료되면 ModelAndView 객체를 디스패처서블릿으로 반환합니다.
ModelAndView 객체에는 요청처리 결과데이터와 반환할 view 의 이름을 가지고 있습니다.
{: .fs-3 }

### 뷰리졸버(ViewResolver)
요청 처리 결과를 클라이언트로 반환하려면 실제 뷰(View) 객체를 찾아야하는데요.
앞서 핸들러메서드를 통해 반환받은 ModelAndView 객체에 뷰 이름이 있기 때문에
디스패처 서블릿은 뷰리졸버를 통해 실제 뷰 객체를 찾아낼 수 있습니다.
{: .fs-3 }

---
