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
# 개방 폐쇄 원칙(OCP: Open-Close Principle) 2
Abstract class 사용 예시

> 확장에는 개방적이고, 수정에는 폐쇄적이어야 한다.

## 설명
개방 폐쇄 원칙(OCP) 란 기존의 코드를 변경하지 않고,
기능을 추가할 수 있도록 설계해야한다는 원칙입니다.

## 문제
계좌에서 돈을 입금, 출금할 수 있는 은행서비스 프로그램을 만들어 봅시다.
아래와 같은 코드에서는 BankingService 를 사용해서 SavingAccount 에 돈을 입금, 출금 할 수 있습니다.

```java
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

    public BankingService(SavingAccount savingAccount) {
        this.account = savingAccount;
    }
    
    // 예금
    public void deposit(int amount) {
        account.addBalance(amount);
    }

    // 출금
    public void withdraw(int amount) {
        account.subBalance(amount);
    }

    public void getBalance() {
        System.out.println(account.getBalance());
    }
}

public class Ocpw {
    public static void main(String[] args) {

        SavingAccount savingAccount = new SavingAccount();
        BankingService bankingService = new BankingService(savingAccount);
        bankingService.deposit(10);
        bankingService.getBalance();

    }
}
```

#### OCP 위반!
하지만 만약 새로운 계좌가 생긴다면 기존 BankingService 의 소스코드가 수정되야함으로 OCP를 위반하게 됩니다.

```java
class NewAccount {
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

    // 수정필요!!
    public BankingService(SavingAccount savingAccount) {
        this.account = savingAccount;
    }

    // 예금
    public void deposit(int amount) {
        account.addBalance(amount);
    }

    // 출금
    public void withdraw(int amount) {
        account.subBalance(amount);
    }

    public void getBalance() {
        System.out.println(account.getBalance());
    }
}
```

## 해결
추상클래스(Abstract class) 상속을 통해 이 문제를 해결할 수 있습니다.
SavingAccount, NewAccount 모두 추상클래스 상속을 통해서
BankingService 소스코드의 수정 없이 새로운 계좌 객체를 확장할수있는 구조가 되었습니다.

```java
// 추상 클래스
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

// 추상 클래스 상속
class SavingAccount extends Account{}
class NewAccount extends Account{}

class BankingService {

    private Account account;

    
    // BankingService -> Account
    public BankingService(Account account) {
        this.account = account;
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

public class Ocp2 {
    public static void main(String[] args) {

        SavingAccount savingAccount = new SavingAccount();
        BankingService bankingService = new BankingService(savingAccount);
        bankingService.deposit(10);
        bankingService.getBalance();
        
        SavingAccount newAccount = new NewAccount();
        BankingService bankingService = new BankingService(newAccount);
        bankingService.deposit(10);
        bankingService.getBalance();

    }
}
```
