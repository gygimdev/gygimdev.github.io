---
layout: default
title: 개방 폐쇄 원칙(OCP) 2
parent: 5가지 원칙(SOLID)
grand_parent: 디자인 패턴(Design Pattern)
nav_order: 3
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
abstract class 사용 예시




## 문제

```java
package solid;

class SavingAccount {
    private int balance;

    public int getBalance() {
        return this.balance;
    }

    public void addBalance(int amount) {
        this.balance += amount;
    }

    public void subBalance(int amount) {
        this.balance -= amount;
    }
}

class BankingService {

    private SavingAccount account;

    public BankingService(SavingAccount currentAccount) {
        this.account = currentAccount;
    }
    public void deposit(int amount) {
        account.addBalance(amount);
    }

    public void withdraw(int amount) {
        account.subBalance(amount);
    }

    public void getBalance() {
        System.out.println(account.getBalance());
    }
}

public class Test {
    public static void main(String[] args) {

        SavingAccount savingAccount = new SavingAccount();
        BankingService bankingService = new BankingService(savingAccount);
        bankingService.deposit(10);
        bankingService.getBalance();

        bankingService.withdraw(5);
        bankingService.getBalance();
    }
}

```

다른 종류의 Account 가 늘어나면 BankingService 가 영향을 받는다.

```java
```

## 해결

abstract class 를 도입해서 해결한다.

```java
package solid;

abstract class Account {
    public int balance;

    public int getBalance() {
        return balance;
    }

    public void addBalance(int amount) {
        this.balance += amount;
    }

    public void subBalance(int amount) {
        this.balance -= amount;
    }
}

class SavingAccount extends Account{}

class CurrentAccount extends Account{}
class BankingService {

    private Account account;

    public BankingService(Account currentAccount) {
        this.account = currentAccount;
    }
    public void deposit(int amount) {
        account.addBalance(amount);
    }

    public void withdraw(int amount) {
        account.subBalance(amount);
    }

    public void getBalance() {
        System.out.println(account.getBalance());
    }
}

public class Test {
    public static void main(String[] args) {

        SavingAccount savingAccount = new SavingAccount();
        BankingService bankingService = new BankingService(savingAccount);
        bankingService.deposit(10);
        bankingService.getBalance();

        bankingService.withdraw(5);
        bankingService.getBalance();
    }
}

```
`Specification` 과 `Filter` 인터페이스의 구현체를 통해서 클라이언트의 추가 요청이 들어오더라도
기존 소스코드 수정없이 Specification 인터페이스를 구현한 구현체를 구현해줌으로써, 클라이언트의 요구사항을 반영할 수 있습니다.
