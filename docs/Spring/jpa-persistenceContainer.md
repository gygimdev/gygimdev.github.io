---
layout: default
title: 영속성 컨테이너
parent: JPA(Java Persistence API)
nav_order: 1
---

# 영속성 컨테이너(Persistence Container)
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
   {:toc}

---

## 영속성 컨테이너(Persistence Container) 란?
![jpa-persistenceContainer.png](..%2F..%2Fstatic%2Fjpa-persistenceContainer.png)

개발자는 EntityManager 를 통해 영속성컨테이너와 상호작용합니다.
그리고 영속성컨테이너는 엔티티의 상태변화를 감지하고 데이터베이스와의 상호작용을 담당합니다.
이를 통해 개발자는 객체 지향적인 방식으로 데이터를 다룰수 있습니다.
{: .fs-3 }



### EntityManager 사용방법
```java
public class EntityManagerExample {
    private static final String PERSISTENCE_UNIT_NAME = "hibernate";

    public static void main(String[] args) {
        // EntityManagerFactory 생성
        EntityManagerFactory entityManagerFactory =
                Persistence.createEntityManagerFactory(PERSISTENCE_UNIT_NAME);

        try {
            // EntityManager 얻기
            EntityManager entityManager = entityManagerFactory.createEntityManager();

            // 트랜잭션 시작
            entityManager.getTransaction().begin();

            try {
                // EntityManager를 사용하여 엔티티 관련 작업수행
                //...
               
                // 작업한 내용을 DB에 반영
                entityManager.getTransaction().commit();
            } catch (Exception e) {
                // 작업 중 예외 발생 시 롤백
                entityManager.getTransaction().rollback();
                e.printStackTrace();
            } finally {
                // EntityManager 사용 후에는 닫아주어야 합니다.
                entityManager.close();
            }
        } finally {
            // EntityManagerFactory를 종료합니다.
            entityManagerFactory.close();
        }
    }
}
```

---

## 영속성컨테이너의 기능

### 반복적인 엔티티 조회시 캐싱기능 제공
```java
// EntityManagerFactory 생성
EntityManagerFactory entityManagerFactory = 
        Persistence.createEntityManagerFactory("hibernate");

// EntityManager 생성
EntityManager entityManager = entityManagerFactory.createEntityManager();

// 첫 번째 조회
Long entityId = 1L;
Entity entity1 = entityManager.find(Entity.class, entityId);
System.out.println("첫 번째 조회: " + entity1);

// 두 번째 조회 (캐싱된 데이터를 사용)
Entity entity2 = entityManager.find(Entity.class, entityId);
System.out.println("두 번째 조회: " + entity2);

// 세 번째 조회 (데이터베이스 쿼리 실행)
entityManager.clear(); // 캐시 초기화
Entity entity3 = entityManager.find(Entity.class, entityId);
System.out.println("세 번째 조회: " + entity3);

// EntityManager 종료
entityManager.close();

// EntityManagerFactory 종료
entityManagerFactory.close();
```
첫 번째 조회시 데이터베이스에서 가져온 데이터를 영속성컨테이너에 저장합니다.
두 번째 조회시에는 영속성 컨테이너에 캐싱된 데이터를 사용합니다.
세번째 조회시에는 `entityManger.claer()` 를 호출함으로써 영속성컨테이너를 초기화 해주었으므로 데이터베이스 쿼리가 실행됩니다.
{: .fs-3 }

### 엔티티 변경감지기능을 통해 변경이 필요한 데이터만 업데이트
``` java
// EntityManagerFactory 생성
EntityManagerFactory entityManagerFactory = 
Persistence.createEntityManagerFactory("hibernate");

// EntityManager 생성
EntityManager entityManager = entityManagerFactory.createEntityManager();
EntityTransaction transaction = entityManager.getTransaction();

// 트랜잭션 시작
transaction.begin();

// 엔티티 조회
Long entityId = 1L;
Entity entity = entityManager.find(Entity.class, entityId);

// 엔티티 데이터 변경
entity.setName("Updated Name");

// 트랜잭션 커밋 (변경 감지)
transaction.commit();

// EntityManager 종료
entityManager.close();

// EntityManagerFactory 종료
entityManagerFactory.close();
```
위의 코드에서 엔티티를 조회한 후에 setName 메서드를 통해 엔티티의 데이터를 변경합니다.
그리고 트랜잭션을 커밋할 때 변경 감지가 동작하여 변경된 데이터만 업데이트됩니다.
이는 JPA의 영속성 컨테이너가 엔티티의 상태 변화를 추적하여 필요한 변경사항만을 데이터베이스에 반영하는 기능입니다.
{: .fs-3 }

{: .important } 
엔티티 변경 감지는 변경된 필드를 추적하기 때문에 변경된 값이 이전 값과 다를 때에만 업데이트가 발생합니다.
따라서 setName() 메서드로 기존 엔티티와 같은 이름으로 변경하면 엔티티 변경 감지가 동작하지 않아 데이터베이스에 업데이트 쿼리가 실행되지 않습니다.
{: .fs-3 }



### 지연로딩을 통해 쿼리 최적화
```java
@Entity
public class Parent {
    @Id
    @GeneratedValue
    private Long id;

    private String name;

    @OneToMany(mappedBy = "parent", fetch = FetchType.LAZY)
    private List<Child> children;

    // getter, setter, constructors
}

@Entity
public class Child {
    @Id
    @GeneratedValue
    private Long id;

    private String name;

    @ManyToOne(fetch = FetchType.LAZY)
    private Parent parent;

    // getter, setter, constructors
}
```

위의 코드에서 Parent 엔티티에서 children 필드는 `@OneToMany` 관계로 설정되어 있고,
Child 엔티티에서 parent 필드는 `@ManyToOne` 관계로 설정되어 있습니다.
두 관계 모두 fetch = FetchType.LAZY로 설정되어 있습니다.
이제 Parent 엔티티를 조회할 때 children 필드는 초기에는 로딩되지 않고, 실제로 필요한 시점에서 쿼리가 실행됩니다.
즉, children 필드를 사용하는 시점에서 쿼리가 발생하므로 필요한 데이터만 로딩하여 쿼리 최적화를 이루게 됩니다.
{: .fs-3 }

```java
Long parentId = 1L;
Parent parent = entityManager.find(Parent.class, parentId);
List<Child> children = parent.getChildren(); // 이 시점에서 쿼리 실행
```
위의 코드에서 parent.getChildren() 호출 시 children 필드를 사용하는 시점에서 쿼리가 실행되어 필요한 데이터만 가져옵니다.
지연로딩은 fetch = FetchType.LAZY를 사용하여 설정하며,
기본적으로 영속성 컨텍스트 내에서 해당 엔티티가 로드되어 있는 경우에만 쿼리 최적화가 적용됩니다.
{: .fs-3 }







