# 핸들러 맵핑과 핸들러 어댑터

HTTP 요청이 들어오면 `dispatcher servlet` 에서 핸들러를 핸들러 매핑에서 조회하고  
반환된 핸들러를 처리할 핸들러 어댑터를 찾는다.

핸들러 맵핑에서 핸들러를 찾는 우선 순위는 1. @RequestMapping 어노테이션, 2. 스프링 비 이름으로 찾는다.

핸들러를 처리할 핸들러 어댑터를 찾는 우선 순위는 1. @RequestMapping 어노테이션, 2. HttpRequestHandler 처리, 3. SimpleControllerHandlerAdapter(컨트롤러 인터페이스 처리)

핸들러를 처리할 핸들러 어댑터를 찾으면 핸들러 어댑터.handle 이 호출된다.

# 뷰 리졸버(View resolver)
스프링 부트가 올라올때 여러가지를 자동으로 등록하는데, 그중에 하나가 `internalResourceViewResolver`이다.
이걸 등록할때 `application.properties` 에 등록한 `spring.mvc.view.prefix` 와 `spring.mvc.view.suffix` 설정 정보를 사용해서 등록한다.

핸들러 어댑터가 `ModelAndView` 를 반환
그리고 디스패쳐가 다시  `viewResolver` 를 호출 `view` 를 반환한다.

스프링 부트가 `viewResolver` 를 호출할때 마다 등록되어 있는 `viewResolver` 들을 조회하고 실행한다. 첫번째로 `1. BeanNamViewResolver` 빈 이름으로 뷰를 찾아서 반환한다. 두번째로 `2. InternalResourceViewResolver` JSP를 처리할 수 있는 뷰를 반환한다.

```java
    ...
        return new ModelAndView("new-form");
```

이런식으로 return 하게 되면 `new-form` 이라는 뷰 이름으로 `viewResolver` 를 순서대로 호출한다. `1. BeanNameViewResolver` 는 `new-form` 으로 등록된 뷰를 찾아야하는데 없어서 다음! `InternalResourceViewResolver` 가 호출 된다.

# MVC 시작
```java
@Controller
public class SpringMemberFormControllerV1 {

    @RequestMapping("/springmvc/v1/members/new-form")
    public ModelAndView process() {
        return new ModelAndView("new-form");
    }
}
```
### `@Controller` 은 두가지 기능을 한다.
1. 스프링이 자동으로 스프링 빈으로 등록한다.
2. 스프링 MVC 에서 에노테이션 기반 컨트롤러로 인식한다.
   - `RequestMappingHandlerMapping` 에서 꺼낼 수 있는 정보가 된다는 뜻!

`RequestMappingHandlerMapping`은 이게 내가 인식할 수 있는 핸들러야 아니야 를 구분하는방법은,
스프링 빈 중에서 `@RequestMapping` 또는 `@Controller` 가 클래스 레벨에 붙어 있는 경우에 매핑 정보로 인식한다.

### `@RequestMapping`
1. HTTP 요청 정보를 맵핑한다. 해당 URL 이 호출되면 해당 메서드가 호출된다.

### `ModelAndView`
1. 모델과 뷰의 정보를 담아서 반환하면 된다.