---
layout: default
title: IoC, DI, Container 개념
parent: 스프링 프레임워크(Spring Framework)
---

# IoC, DI, Conatiner 개념
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

## 제어의 역전(Ioc: Inversion of Control)

{: .highlight }
**프로그램 제어 흐름의 주도권은 외부에 있다.**  

{: .fs-2 }
**제어의 역전(IoC: Inversion of Control)** 은 소프트웨어 개발에서 컴포넌트 간의 의존성 관리를 위한 디자인 패턴입니다.
일반적으로 프로그램의 흐름은 개발자가 작성한 코드에 의해 결정됩니다.
하지만 IoC는 이러한 제어의 흐름을 역전시켜 프레임워크나 컨테이너가 코드의 흐름을 제어하게 합니다.

{: .fs-2 }
일반적인 방식에서는 개발자가 객체를 생성하고 의존성을 설정하여 사용합니다.
그러나 IoC에서는 개발자가 객체의 생성과 관리를 직접하지 않고, 객체의 생명주기와 의존성 주입을 IoC 컨테이너에게 맡깁니다.
이렇게 하면 객체 간의 결합도가 낮아지고, 코드의 재사용성과 유지보수성이 향상됩니다.

{: .fs-2 }
IoC의 핵심 개념은 **의존성 주입(Dependency Injection)** 입니다.
IoC 컨테이너는 객체의 의존성을 관리하고, 필요한 의존성을 주입하여 객체가 동작할 수 있도록 합니다.
이를 통해 객체 간의 결합도를 낮추고 유연하고 확장 가능한 애플리케이션을 만들 수 있습니다.

{: .fs-2 }
간단히 말하면, IoC는 개발자가 제어의 흐름을 직접 관리하는 것이 아니라 프레임워크나 컨테이너에게 제어의 흐름을 맡기는 것입니다.
이를 통해 애플리케이션의 유연성과 확장성을 높일 수 있으며, 객체 간의 결합도를 줄여서 코드의 유지보수를 용이하게 하는 것을 말합니다.


### 제어역전(IoC) 적용 전: 코드의 유연성, 재사용성 저하

{: .fs-2 }
이 방식은 클라이언트 객체가 서비스 객체에 대한 직접적인 의존성을 가지며, 이를 생성하고 관리하는 책임을 갖게 됩니다.
이로 인해 클라이언트 객체와 서비스 객체 간의 결합도가 높아지고, 코드의 유연성과 재사용성이 저하됩니다.

```java
public class EmailService {
    public void sendEmail(String message) {
        // 이메일 전송 //
    }
}

public class SMSService {
    public void sendSMS(String message) {
        // SMS 전송 //
    }
}

public class Client {
    private EmailService emailService;
    
    public Client() {
        this.emailService = new EmailService();
    }
    
    public void send(String message) {
        emailService.sendEmail(message);
    }
}

public class Main {
    public static void main(String[] args) {
        Client client = new Client();
        client.send("Hello");
    }
}
```

### 제어역전(IoC) 적용: 낮은 결합도, 높은 유연성과 재사용성

{: .fs-2 }
이 예제에서 중요한 점은 의존성을 생성하는 제어의 흐름이 역전된다는 것입니다.
클라이언트가 MessageService 객체를 직접 생성하는 대신, 외부 엔티티에게 구현을 제공받습니다.
이렇게 함으로써 코드 간의 결합도를 낮출 수 있으며, 유연성과 재사용성을 높힐 수 있습니다.

```java
public interface MessageService {
    void sendMessage(String message);
}

public class EmailService implements MessageService {
    void sendMessage(String message) {
        // 이메일 전송 //
    }
}

public class SMSService implements MessageService {
    void sendMessage(String message) {
        // SMS 전송 //
    }
}

public class Client {
    private MessageService messageService;
    
    public Client(MessageService messageService) {
        this.messageService = messageService;
    }
   
    
    public void send(String message) {
        messageService.sendMessage(message);
    }
}

public class Main {
    public static void main(String[] args) {
        // IoC를 통해 MessageService 객체를 주입받는 제어 흐름
        MessageService emailService = new EmailService();
        Client client = new Client(emailService);
        client.sendNotification("Hello!");
    }
}
```
---

## 의존성 주입(DI: Dependency Injection)

{: .highlight }
객체 간의 의존성을 외부에서 주입하는 방식

{: .fs-2 }
**DI(Dependency Injection)** 는 제어의 역전(IoC) 패턴의 일부로, 객체 간의 의존성을 외부에서 주입하는 방식입니다.
이를 통해 객체 간의 결합도를 낮추고 유연하고 재사용 가능한 코드를 작성할 수 있습니다.

{: .fs-2 }
일반적으로 객체는 다른 객체와 상호작용하기 위해 해당 객체에 의존성을 가집니다.
예를 들어, 클래스 A가 클래스 B의 메서드를 호출한다면, 클래스 A는 클래스 B에 대한 의존성을 가지게 됩니다.
이러한 의존성은 직접 객체를 생성하거나 가져와서 사용하는 방식으로 처리될 수 있습니다.

{: .fs-2 }
DI는 이러한 의존성을 외부에서 관리하고 주입하는 방식을 사용 합니다.
즉, 객체가 필요로 하는 의존성을 직접 생성하지 않고, 외부에서 생성된 의존성을 주입받아 사용합니다.

```java
public class Client {
    private MessageService messageService;
   
    // 생성시점에 어떤 구현체(EmailService, SNSService)가 들어올지
    // 명시적으로 선언하지 않음으로서 객체 간의 결합도를 낮추었다.
    public Client(MessageService messageService) {
        this.messageService = messageService;
    }
    ...
```

### 스프링에서 사용하는 주입방법 종류

#### 생성자 주입 방법(스프링에서 권장)
```java
public class UserService {
    private UserRepository userRepository;

    // 생성자 주입 //
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
    
    // ...
}

public class UserRepository {
    // ...
}

// 사용 예시
UserRepository userRepository = new UserRepository();
UserService userService = new UserService(userRepository);
```

#### 세터 주입 방법
```java
public class UserService {
    private UserRepository userRepository;
    
    // 세터주입
    public void setUserRepository(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
    
    // ...
}

public class UserRepository {
    // ...
}

// 사용 예시
UserRepository userRepository = new UserRepository();
UserService userService = new UserService();
userService.setUserRepository(userRepository);
```

#### 필드 주입 방법
```java
public class UserService {
    @Autowired
    private UserRepository userRepository;
    
    // ...
}

public class UserRepository {
    // ...
}

// 사용 예시
UserService userService = new UserService();
```

---

## IoC 컨테이너 & DI 컨테이너

{: .highlight }
IoC:객체 생성 관리에 집중, DI: 의존성 주입에 집중

{: .fs-2 }
스프링에서 IoC(Inversion of Control) 컨테이너와 DI(Dependency Injection) 컨테이너는 서로 밀접하게 관련되어 있지만, 
약간의 차이가 있습니다.

### IoC(Inversion of Control) 컨테이너:
{: .fs-2 }
- IoC 컨테이너는 애플리케이션의 제어 흐름을 관리하고 객체의 생명주기를 관리하는 핵심 기능을 제공합니다.
- IoC 컨테이너는 애플리케이션의 제어 흐름을 개발자로부터 역전시켜 객체의 생성과 관리를 컨테이너에 위임합니다.

### DI(Dependency Injection) 컨테이너:
{: .fs-2 }
- DI 컨테이너는 IoC 컨테이너의 일종으로, 의존성 주입을 통해 객체 간의 의존 관계를 해결하는 기능을 제공합니다.
- 객체가 필요로 하는 의존성을 컨테이너가 자동으로 주입해줌으로써 객체 간의 결합도를 낮추고 유연한 애플리케이션을 구성할 수 있게 해줍니다.

**차이점:**
{: .fs-2 }
- IoC 컨테이너는 라이프사이클 관리와 객체 생성에 집중하며, DI 컨테이너는 의존성 주입에 집중합니다.
- 스프링은 IoC 컨테이너와 DI 컨테이너를 함께 제공하여 객체의 생성과 의존성 관리를 편리하게 할 수 있도록 지원합니다. IoC 컨테이너의 대표적인 예로는 ApplicationContext가 있으며, DI 컨테이너는 IoC 컨테이너의 일부 기능으로 포함됩니다.
- 객체간의 필요한 의존관계를 생성하고 관리하면서 연결해주는 것을 IoC, DI 컨테이너라고 합니다.

