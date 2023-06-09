---
layout: default
title: 서블릿(Servlet)
parent: 스프링(Spring)
permalink: /docs/spring/servlet
nav_order: 4
---

# 스프링 서블릿(Servlet)
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

## 서블릿(Servlet)

서블릿은 HTTP 요청과 응답을 효율적이게 처리할수 있게 해주는 자바 객체입니다. 
예를 들어 HTTP 요청과 응답을 읽어 객체로 만드는 작업은 손이 많은 가는 작업인데요.
이런 손이 많이 가는 작업은 내부 톰캣과 같은 컨테이너에게 위임하고
개발자들은 중요한 비즈니스 로직에 집중할 수 있게 해줍니다.
{: .fs-3 }

스프링 MVC등장 이후로는 서블릿을 직접 구현하지 않고
dispatcherServlet 을 통해 요청을 처리하고 컨트롤러를 구현합니다. 
{: .fs-3 }

### 서블릿은 싱글톤패턴으로 생성됩니다.
서블릿은 여러 클라이언트의 요청을 동시에 처리할 수 있어야합니다.
싱글톤으로 서블릿을 생성함으로써 일관성있는 요청처리와
불필요한 인스터스화를 막아 자원절감을 할 수 있습니다.
{: .fs-3 }

### 구현방법

```java
// 공통
public class MyServlet extends HttpServlet {
    
    @Override
    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 요청 메서드에 상관없이 호출되는 service() 메서드입니다.
        // 요청 메서드에 따라 적절한 동작을 수행하도록 구현합니다.
        
        String method = request.getMethod(); // 요청의 HTTP 메서드를 가져옵니다.
        
        if (method.equalsIgnoreCase("GET")) {
            doGet(request, response); // GET 요청에 대한 처리 로직을 호출합니다.
        } else if (method.equalsIgnoreCase("POST")) {
            doPost(request, response); // POST 요청에 대한 처리 로직을 호출합니다.
        } else {
            // 기타 다른 요청 메서드에 대한 처리 로직을 구현할 수 있습니다.
        }
    }
}
```

```java
// 메서드별
public class MyServlet extends HttpServlet {
    
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // GET 요청 처리 로직을 구현합니다.
        // 요청 파라미터 읽기, 데이터 처리, 응답 생성 등을 수행합니다.
        // 예시로 "Hello, World!"를 응답으로 전송합니다.
        response.getWriter().write("Hello, World!");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // POST 요청 처리 로직을 구현합니다.
        // 요청 파라미터 읽기, 데이터 처리, 응답 생성 등을 수행합니다.
    }

    // 다른 HTTP 메서드에 대해서도 필요한 경우 해당 메서드를 오버라이딩하여 처리 로직을 추가할 수 있습니다.
}

```

## 서블릿 컨테이너
서블릿 컨테이너는 크게 3가지 일을 합니다.
{: .fs-3 }

첫 번째로, 애플리케이션 실행시 싱글톤으로 서블릿을 인스턴스화 시킵니다.
{: .fs-3 }

두 번째로, 요청이 들어오면 적절한 서블릿을 찾아 매핑해줍니다.
{: .fs-3 }

세 번째로, 동시요청을 처리하기 위해 쓰레드 풀을 관리합니다.
쓰레드 풀은 일정량의 쓰레드를 생성하고 유지하며, 요청이 들어오면 해당 쓰레드를 할당하여 처리합니다.
요청 처리가 완료되면 쓰레드를 쓰래드풀에 반환하여 효율적으로 리소스 관리를 할 수 있습니다.
{: .fs-3 }

![servlet.png](..%2F..%2Fstatic%2Fspring%2Fservlet.png)


