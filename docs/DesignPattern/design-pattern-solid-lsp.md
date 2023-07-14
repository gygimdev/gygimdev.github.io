---
layout: default
title: 리스코프 치환 원칙(LSP)
parent: 5가지 원칙(SOLID)
grand_parent: 디자인 패턴(Design Pattern)
nav_order: 4
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

# 리스코프 치환 원칙(LSP: Liskov Substitution Principle)

리스코브 치환 원칙은 상위 타입을 하위 타입이 완전히 대체할 수 있어야 한다는 원칙입니다.
이 말은 하위 타입은 상위 타입처럼 행동해야하는 것을 의미합니다.

## 문제
앞서 추상클래스를 통해 여러 종류의 계좌가 생성되더라도 BankingService 의 코드를 수정하지 않고
확장가능한 구조로 설계해 OCP 원칙을 지켰습니다.

하지만 출금이 불가능하고 예금만 가능한 계좌가 생긴다면 어떨까요?
예금만 가능한 SpecialAccount 계좌를 만들어 봅시다.
```java
abstract class Account {
    public int balance;

    protected int getBalance() {
        return balance;
    }

    protected void addBalance(int amount) {
        this.balance += amount;
    }

    protected void subBalance(int amount) {
        this.balance -= amount;
    }
}

class SavingAccount extends Account{}
class NewAccount extends Account{}

// 예금만 가능한 계좌
class SpecialAccount extends Account {

    @Override
    protected void subBalance(int amount) {
        throw new UnsupportedOperationException("Withdrawals are not supported by SpecialAccount");
    }

}
class BankingService {

    private Account account;

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

public class Lsp {
    public static void main(String[] args) {

        SavingAccount savingAccount = new SavingAccount();
        BankingService bankingService = new BankingService(savingAccount);
        bankingService.deposit(10);
        bankingService.getBalance();

        // 스패셜 어카운트
        SpecialAccount specialAccount = new SpecialAccount();
        BankingService specialBankingService = new BankingService(specialAccount);
        specialBankingService.deposit(5);
        specialBankingService.withdraw(1);
    }
}

```
SpecialAccount 는 예금만 가능하기 때문에 출금시 UnsupportedOperationException 에러를 발생시키도록 합니다.
하지만 이렇게 코드를 작성하게되면 LSP 원칙을 위배하게 됩니다.
하위 타입인 SpecialAccount 의 지출 로직 때문에 상위 타입인 Account 와의 행동이 일치하지 않습니다.

Account 와 specialAccount 객체 간의 결합도를 낮추기 위해 WithdrawabalAccount 객체를 만들어 줍시다.

## 해결
```java
abstract class Account {
    public int balance;
    
    protected int getBalance() {
        return balance;
    }

    // 예금만 가능
    protected void addBalance(int amount) {
        this.balance += amount;
    }
}

abstract class WithdrawableAccount extends Account {

    // 출금 기능 추가
    protected void subBalance(int amount) {
        this.balance -= amount;
    }
}

class SpecialAccount extends Account {}
```

SavingAccount 는 WithdrawableAccount 를 상속 받고 SpecialAccount 는 Account 를
상속 받음으로서 LSP 의 원칙을 지킬 수 있게 됩니다.
