# HTTP 메세지 컨버터는 스프링 MVC 어디쯤에서 사용되는 것일까?


# Argument Resolver
이렇게 파라미터를 유연하게 처리할 수 있는 이유가 바로 ArgumentResolver 덕분이다.  
애노테이션 기반 컨트롤러를 처리하는 `RequestMappingHandlerAdaptor` 는  
바로 이 `ArgumentResolver` 를 호출해서 컨트롤러(핸들러) 가 필요로 하는  
다양한 파라미터의 값(객체)를 생성한다.

# 동작방식
`ArgumentResolver` 의 `supportsParameter()` 를 호출해서  
해당 파라미터를 지원하는지 체크하고, 지원하면 `resolveArgument()` 를 호출해서  
실제 객체를 생성한다. 그리고 이렇게 생성된 객체가 컨트롤러 호출시 넘어가는 것이다.

# HTTP 메세지 컨버터는 어디쯤 있을까?
`argument resolver`, `return value resolver` 가 HTTP 메세지 컨버터를 사용한다.
### 요청의 경우
`@RequestBody` 를 처리하는 `ArgumentResolver` 가 있고,
`HttpEntity` 를 처리하는 `ArgumentResolver` 가 있다.  
이 `ArgumentResolver` 들이 HTTP 메시지 컨버터를 사용해서 필요한 객체를 생성하는 것이다.
### 응답의 경우
`@ResponseBody` 와 `HttpEntity` 를 처리하는 `ReturnValueHandler` 가 있다.
그리고 여기에서 HTTP 메시지 컨버터를 호출해서 응답 결과를 만든다.
