---
layout: default
title: 개방 폐쇄 원칙(OCP)
parent: 5가지 원칙(SOLID)
grand_parent: 디자인 패턴(Design Pattern)
nav_order: 2
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
# 개방 폐쇄 원칙(OCP: Open-Close Principle)

> 확장에는 개방적이고, 수정에는 폐쇄적이어야 한다.

## 설명
개방 폐쇄 원칙(OCP) 란 기존의 코드를 변경하지 않고, 기능을 추가할 수 있도록 설계해야한다는 원칙입니다.
쉽게 말하면, 작성된 기능의 코드를 수정하지 않고 확장해가면서 기능 추가가 가능해야된다는 말인데요.
아래의 예제를 보면서 이해해봅시다.




## 문제
상품을 필터링 하는 프로그램이 필요하다고 가정합니다.
클라이언트의 요구사항은 상품을 색상 별로 필터링 하는 것입니다.
요구사항을 구현해봅시다.

```java
enum Color {
    RED, GREEN, BLUE
}

enum Size {
    SMALL, MEDIUM, LARGE
}

class Product {
    public String name;
    public Color color;
    public Size size;

    public Product(String name, Color color, Size size) {
        this.name = name;
        this.color = color;
        this.size = size;
    }
}

class ProductFilter {

    public Stream<Product> filterByColor(List<Product> products, Color color) {
        return products.stream().filter(p -> p.color == color);
    }
}


public class Ocp {

    public static void main(String[] args) {
        Product apple = new Product("Apple", Color.RED, Size.SMALL);
        Product tree = new Product("Tree", Color.GREEN, Size.MEDIUM);
        Product house = new Product("House", Color.BLUE, Size.LARGE);

        List<Product> products = List.of(apple, tree, house);

        ProductFilter pf = new ProductFilter();
        pf.filterByColor(products, Color.GREEN)
                .forEach(p -> System.out.println(" - " + p.name + " is Green"));

    }
}
```
색상, 크기의 enum 을 만들어주고, product 와 productFilter 클래스를 구현해줌으로 클라이언트의 요구사항을 만족 시켰습니다.
하지만 클라이언트의 추가 요구사항이 발생한다면 어떨까요?
크기, 가격, 타입 등 추가 요구사항이 발생한다면, `ProductFilter' 클래스를 계속 수정해야하는 상황이 발생합니다.
이러한 방법은 OCP 위배 사항에 해당합니다. 프로그램은 확장에는 열려있고 수정에는 닫혀있어야합니다.

```java
class ProductFilter {

    public Stream<Product> filterByColor(List<Product> products, Color color) {
        return products.stream().filter(p -> p.color == color);
    }
    // 추가
    public Stream<Product> filterBySize(List<Product> products, Size size)  {
        return products.stream().filter(p -> p.size == size);
    }
    
    public Stream<Product> filterBySize(List<Product> products, Size size)  {
        return products.stream().filter(p -> p.size == size);
    }

    public Stream<Product> filterBySizeAndColor(List<Product> products, Size size, Color color)  {
        return products.stream().filter(p -> p.size == size && p.color == color);
    }
    // 계속 추가 ...
}

```

## 해결

인터페이스를 활용해서 이 문제를 해결해야합니다.
이 문제를 해결하기 위해 `specification` 과 `filter` 인터페이스를 만들어주고
각 인터페이스를 구현한 구현체를 만들어 줍니다.
```java
interface Specification<T> {
    boolean isSatisfied(T item);
}

interface Filter<T> {
    Stream<T> filter(List<T> items, Specification<T> spec);
}

// Filter 인터페이스를 구현한 구현체
class BetterFilter implements Filter<Product> {

    @Override
    public Stream<Product> filter(List<Product> items, Specification<Product> spec) {
        return items.stream().filter(p -> spec.isSatisfied(p));
    }
}

// Specification 인터페이스를 구현한 구현체
class ColorSpecification implements Specification<Product> {
    private Color color;

    public ColorSpecification(Color color) {
        this.color = color;
    }

    @Override
    public boolean isSatisfied(Product item) {
        return item.color == color;
    }
}

// 추가 요구사항: 상품을 크기로 필터한다.
class SizeSpecification implements Specification<Product> {
    private Size sizie;

    public SizeSpecification(Size size) {
        this.size = size;
    }

    @Override
    public boolean isSatisfied(Product item) {
        return item.size == size;
    }
}
```

```java
public class Ocp {
    public static void main(String[] args) {
        Product apple = new Product("Apple", Color.RED, Size.SMALL);
        Product tree = new Product("Tree", Color.GREEN, Size.MEDIUM);
        Product house = new Product("House", Color.BLUE, Size.LARGE);
        List<Product> products = List.of(apple, tree, house);
        
        BetterFilter bf = new BetterFilter();
        bf.filter(products, new ColorSpecification(Color.GREEN))
                .forEach(p -> System.out.println(" - " + p.name + " is Green"));
    }
}

```
`Specification` 과 `Filter` 인터페이스의 구현체를 통해서 클라이언트의 추가 요청이 들어오더라도
기존 소스코드 수정없이 Specification 인터페이스를 구현한 구현체를 구현해줌으로써, 클라이언트의 요구사항을 반영할 수 있습니다.
