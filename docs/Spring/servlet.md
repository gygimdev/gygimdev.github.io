---
layout: default
title: 서블릿(Servlet)
parent: 스프링 프레임워크(Spring Framework)
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
스프링 MVC가 도입되기 이전에는 대부분의 웹 애플리케이션 개발에서 서블릿을 사용하여 동적인 서버 요청을 처리했습니다.
서블릿은 애플리케이션이 시작될때 서블릿컨테이너에 인스턴스화 되며, 클라이언트 요청마다 새로운 스레드가 생성되어 해당 서블릿 인스턴스가 요청을 처리합니다.
서블릿을 사용하면 HTTP 요청의 파라미터, 세션 관리, 쿠키 처리 등과 같은 웹 애플리케이션의 기능을 직접 처리할 수 있습니다.
그러나 서블릿은 저수준의 API를 제공하기 때문에, 개발자가 직접 HTTP 요청과 응답을 다루기 위해 많은 코드 작업이 필요했습니다.
{: .fs-3 }

### 싱글톤패턴
서블릿은 여러 클라이언트의 요청을 동시에 처리할 수 있어야 하므로, 상태 정보를 공유할 필요가 있습니다. 싱글톤 패턴을 사용하면 서블릿 인스턴스 내의 상태 정보가 여러 요청에 공유되어 일관성을 유지할 수 있습니다
{: .fs-3 }

### 구현방법

```java
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
스프링에서의 서블릿 컨테이너는 서블릿의 실행과 생명 주기를 관리하는 역할을 합니다.
서블릿 컨테이너는 애플리케이션 로딩시점에 서블릿 객체를 미리만들어두고 사용하기 때문에 요청마다 객체를 생성하지 않습니다.
서블릿 컨테이너는 클라이언트의 요청을 받아들이고, 요청에 따라 적절한 서블릿을 실행하여 요청을 처리합니다.
{: .fs-3 }

{: .note }
동시요청을 처리하기위해 서블릿 컨테이너는 스레드 풀(Thread Pool)을 관리하며,
요청이 들어올 때마다 스레드 풀에서 사용 가능한 스레드를 가져와 해당 요청을 처리합니다.
스레드 풀은 미리 일정량의 스레드를 생성하여 유지하고, 요청이 들어오면 해당 스레드를 할당하여 요청을 처리한 후 다시 풀에 반환합니다.
이를 통해 스레드의 생성과 소멸에 따른 오버헤드를 줄이고, 효율적인 리소스 관리를 할 수 있습니다.
{: .fs-3 }

### 브라우저 서블릿 요청 흐름도
![servletFlow.png](..%2F..%2Fstatic%2FservletFlow.png)


{: .note }
스프링 MVC에서는 개발자가 직접 서블릿을 만들어 사용하는 것이 아니라, 스프링 프레임워크가 제공하는 DispatcherServlet을 사용합니다. 개발자는 DispatcherServlet을 설정하고, 요청에 대한 매핑을 정의하는 등의 작업을 통해 웹 애플리케이션의 동작을 제어할 수 있습니다. DispatcherServlet은 요청을 받으면 컨트롤러에게 전달하고, 컨트롤러는 비즈니스 로직을 처리한 후에 응답을 생성합니다.
{: .fs-3 }
