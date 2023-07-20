---
layout: default
title: 인터페이스 분리 원칙(ISP)
parent: 5가지 원칙(SOLID)
grand_parent: 디자인 패턴(Design Pattern)
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

# 인터페이스 분리 원칙(ISP: Interface Segregation Principle)
인터페이스 분리 원칙은 인터페이스를 어떤 기준으로 분리해야하는가에 대한 원칙입니다.
즉 클라이언트는 자신이 이용하지 않는 메서드에 의존해서는 안됩니다.

인터페이스 분리가 잘 되어 있지 않을때 구현체에서 불필요한 인터페이스를 구현해야하는 문제를 만나게 됩니다.

## 문제
프린트, 스캔, 팩스를 할 수 있는 다목적프린터를 구현해야할 때 우리는 아래와 같이 코드를 짤 수 있습니다.

```java
class Document {
}

interface Machine {
    void print(Document d);
    void scan(Document d);

    void fax(Document d);
}

class MultiFunctionPrinter implements Machine {

    @Override
    public void print(Document d) {
        // 프린트 로직...
    }

    @Override
    public void scan(Document d) {
        // 스캔 로직...

    }

    @Override
    public void fax(Document d) {
        // 팩스 로직...
    }
}

```

하지만 다목적프린터가 아닌 오직 프린트 작업만 할 수 있는
프린터를 만들어야 한다면 불필요한 메서드를 구현해야한다는 문제가 생깁니다.

```java
/** 프린트 작업만 수행해야하는 프린터 */
class OldFashionedPrinter implements Machine {

    @Override
    public void print(Document d) {
        // 프린트 로직
    }

    @Override
    public void scan(Document d) {
        // 불필요
    }

    @Override
    public void fax(Document d) {
        // 불필요
    }
}
```
`OldFashionedPrinter` 구현체는 프린트 기능만 수행해야하지만
`Machine` 인터페이스를 구현했기 때문에 모든 메서드를 구현해야합니다.

이를 해결하기 위해 아래와 같은 방법을 사용할 수 있지만
추가적으로 문제를 발생시키기 때문에 사용해서는 안됩니다.

1. 아무것도 안하기  
`OldFashionedPrinter` 클래스를 사용하는 입장에서는 scan과 fax 메서드를 호출할 수 있지만,
실제로 아무런 동작이 수행되지 않기 때문에 클래스를 구현하는 입장에서 혼란스러울 수 있습니다.
```java
    @Override
    public void scan(Document d) {
        // 아무것도 안하기
    }

    @Override
    public void fax(Document d) {
        // 아무것도 안하기
    }
```
2. 예외 던지기  
```java
    @Override
    public void scan(Document d) {
        throw new Exception();
    }
    
    interface Machine {
        void print(Document d);
        void scan(Document d) throws Exception;
    }
```
예외를 던지는 방법을 사용한다면 인터페이스에서 추가로 예외를 처리해주는 작업이 늘어나게 됩니다.


## 해결
인터페이스 분리 법칙을 사용해서 이 문제를 해결할 수 있습니다.
`Machine` 인터페이스를 적절하게 기능에 맞게
프린팅, 스캐닝, 팩싱 인터페이스로 분리하는 것입니다.


이제 프린트 작업만 수행하는 프린터를 만드려면 단순히 `Printer` 인터페이스를 구현하면됩니다.

>YAGNI = You Ain't Going to Need it
> 
프린터는 프린팅 작업만 해야하기 때문에 `Scanner` 인터페이스는 구현하지 않습니다.

```java
interface Printer {
    void print(Document d);
}

interface Scanner {
    void scan(Document d);
}

class JustPrinter implements Printer {

    @Override
    public void print(Document d) {
        // 프린트 작업
    }
    
    // YAGNI: Scanner 인터페이스는 구현할 필요가 없습니다!
    
}

class Photocopier implements Printer, Scanner {

    @Override
    public void print(Document d) {
        // ...
    }

    @Override
    public void scan(Document d) {
        // ...
    }
}
```

인터페이스 분리를 통해 구현체는 불필요한 메서드를 처리할 필요가 없어지고
꼭 필요한 기능만 구현하여 사용할 수 있게 되었습니다.