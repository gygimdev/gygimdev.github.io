---
layout: default
title: 엔티티
grand_parent: 스프링(Spring)
parent: JPA(Java Persistence API)
nav_order: 1
---

## 엔티티(Entity)
엔티티는 JPA 에서 데이터베이스 레코드와 매핑되는 자바객체입니다.
이 엔티티를 통해서 데이터베이스 작업을 객체지향적으로 사용할 수 있습니다.
엔티티는 영속성 컨텍스트에 등록되어 사용됩니다.
{: .fs-3 }

```java
@Entity
@Table(name = "member")
public class Member {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String name;

    // Constructors, getters, setters, and other methods

}
```
