---
layout: default
title: 단일 책임 원칙(SRP)
parent: 5가지 원칙(SOLID)
grand_parent: 디자인 패턴(Design Pattern)
nav_order: 1
---

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
# 단일 책임 원칙(Single Responsibility Principle)

## 설명

> 클래스를 변경할 이유는 단 하나여야 한다.

풀어서 말하면 하나의 클래스는 단 하나의 책임을 가져야하고 다양한 책임을 가지면 안됩니다.
만약 클래스가 다중 책임을 가지게 된다면 안티 패턴인 "God Object" 을 만들게 되어 프로그램 유지보수에 어려움을 겪을 수 있습니다.
{: .fs-3 }


## 코드 예시

#### 문제 | PROBLEM
아래의 `Jounal` 클래스는 항목을 추가하고 제거하는 기능과
데이터베이스에서 일지를 조회하고 저장하는 메서드를 가지고 있습니다.
{: .fs-3 }

그러나, 해당 클래스에는 문제가 있습니다.
이 상황에서는 관심사 분리(Separation of concerns) 가 필요합니다.
Journal 클래스는 두가지 관심사(책임)을 가지고 있기 때문입니다.
{: .fs-3 }

01. 항목에 대한 책임(추가, 제거)
02. 일지(객체)의 영속성에 대한 관심사(객체 저장, 조회)
{: .fs-3 }

이는 SRP 를 위배하는 사례이며,
관심사를 분리하여 객체의 영속성을 처리하는 별도의 클래스를 생성해야합니다.
{: .fs-3 }

```java
class Journal {
    private final List<String> entries = new ArrayList<>();
    private static int count = 0;

    // 1. 항목 추가
    public void addEntry(String text) {
        entries.add("" + (++count) + ": " + text);
    }

    // 2. 항목 제거
    public void removeEntry(int index) {
        entries.remove(index);
    }

    //
    // --- SRP 위배 ---
    //
    
    // 3. 일지 저장
    public void save(String filename) {
        // ...데이터베이스에 일지를 저장합니다.
    }
   
    // 4. 일지 조회
    public Jounal load(String filename) {
        // ...데이터베이스에서 일지를 조회합니다.
    }
    
    //
    // --- end: SRP 위배 ---
    //
    
    @Override
    public String toString() {
        return String.join(System.lineSeparator(), entries);
    }
}

```

#### 해결 | Solution

객체의 영속성을 처리하는 책임을 가진 클래스를 따로 생성하여 클래스마다 하나의 책임을 갖도록 변경합니다.
이제 Persistence 클래스는 객체의 영속성에 대한 책임을 갖고 있으며, 데이터베이스와의 상호작용을 담당합니다.
{: .fs-3 }

이렇게 함으로써 Journal 클래스는 항목 추가 및 제거와 같은 항목 관련 책임만을 가지게 되고,
Persisttence 클래스는 객체의 영속성을 처리하는 책임을 담당합니다.
{: .fs-3 }

이렇게 클래스 간의 책임을 분리함으로써 SRP 를 준수하고, 코드의 구조와 유지보수성을 향상시킬 수 있습니다.
{: .fs-3 }

```java
class Persistence {

    public void save(Jounal jounal, String filename) {
        // 저장 로직
    }

    public Jounal load() {
        // 불러오기 로직
    }
}
```
#### 요점 | Takeaway

SRP의 핵심 개념은 각 클래스가 단 하나의 책임을 가지도록 설계하는 것입니다.
한 클래스가 다양한 책임을 갖게 되면 프로그램 관리가 어려워질 수 있습니다.
{: .fs-3 }

이러한 다중 책임을 갖는 클래스를 `God Object` 라고 부르며,
이는 프로그램의 유지보수를 어렵게 만드는 Anti-pattern 중 하나입니다.
{: .fs-3 }

예를 들어, 프로그램에 수백 개의 객체가 있다고 가정해 봅시다.
어느 순간  데이터베이스 URL 변경 등 수정사항이 생기면,
책임이 분리되어 있지 않은 경우에는 수백개의 객체의 저장 로직을 변경해야 할 수도 있습니다.
{: .fs-3 }

SRP를 통해 클래스의 책임을 분리하면, 저장 로직이 변경되더라도
`Persistence` 클래스의 save 메서드만 수정하면 됩니다.
{: .fs-3 }

이로서 유지보수가 용이한 프로그램을 만들 수 있습니다.
SRP는 클래스의 기능을 관리 가능한 단위로 분리하여 코드의 응집성을 높히고
객채간의 결합도를 낮추는데 도움이 됩니다.
{: .fs-3 }

