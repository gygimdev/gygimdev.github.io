1. 스프링부트 콘솔에 색상추가
``` yaml
spring:
  output:
    ansi:
      enabled: always
```

2. 메세지 컨버터

3. ModelAttribute 는 프로퍼티 접근법을 쓰기때문에 사용할 객체에 setter 가 정의되어 있지 않으면 작동하지 않는다.

4. Entity 를 Dto 로 변환하는 작업은 controller 가 좋을까? service 가 좋을까?
```
스프링에서 Entity를 DTO로 변환하는 작업은 일반적으로 Service 레이어에서 수행하는 것이 좋습니다. 이는 아래와 같은 이유로 권장됩니다:

역할과 책임의 분리: Service 레이어는 비즈니스 로직을 담당하는 곳으로, 데이터의 가공 및 처리와 관련된 작업을 수행합니다. Entity를 DTO로 변환하는 것은 비즈니스 로직의 일부로 간주될 수 있으며, 이를 Service 레이어에서 처리하는 것이 좋은 설계 원칙입니다. 이렇게 하면 Controller는 요청과 응답을 처리하는 역할에 집중할 수 있습니다.

재사용성과 유연성: DTO 변환 로직은 종종 여러 곳에서 필요로 하게 될 수 있습니다. Service 레이어에서 DTO 변환을 수행하면 다른 비즈니스 로직에서도 동일한 DTO 변환을 재사용할 수 있습니다. 또한, 필요에 따라 DTO 변환 로직을 수정하거나 대체하기도 쉽습니다.

테스트 용이성: Service 레이어는 일반적으로 단위 테스트 및 통합 테스트를 수행하는 데 적합한 위치입니다. Entity를 DTO로 변환하는 로직을 Service 레이어에서 테스트할 수 있으며, 이를 통해 변환 과정의 정확성을 검증할 수 있습니다.

하지만 이는 절대적인 규칙은 아니며, 상황에 따라 다를 수 있습니다. 프로젝트의 구조와 복잡성, 개발자의 선호도 등을 고려하여 결정하는 것이 중요합니다. 때로는 Controller에서 DTO 변환을 수행하는 것이 더 간편하거나 유용할 수도 있습니다. 따라서 해당 프로젝트의 요구 사항과 개발 팀의 결정에 따라 최적의 방법을 선택하는 것이 좋습니다.
```

5. 스프링 시큐리티

6. 필터, 인터셉트

7. X DI

8. AOP

9. X 서블릿

10. 트랜젝션

11. X 스프링컨테이너와 빈 

12. JPA 영속성 컨테이너

13. 양방향 연관관계