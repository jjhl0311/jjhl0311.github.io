---
title: Spring Boot 애플리케이션 프로그래밍 방식으로 종료하기
date: 2023-09-06 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## 오류: ExitCodeException

스프링 부트(Spring Boot)는 자바 웹 애플리케이션을 쉽고 빠르게 개발할 수 있도록 도와주는 프레임워크입니다. 그런데 때로는 스프링 부트 애플리케이션을 코드로 종료해야 할 경우가 있습니다. 오늘은 이러한 시나리오에 어떻게 대응할 수 있는지 알아보겠습니다.

## ApplicationContext와 SpringApplication.exit() 사용

스프링 부트에서는 `ApplicationContext`라는 중심적인 인터페이스를 통해 다양한 기능을 제어할 수 있습니다. 이 `ApplicationContext`를 사용해 프로그램을 안전하게 종료할 수 있습니다.

```java
import org.springframework.boot.SpringApplication;
import org.springframework.context.ConfigurableApplicationContext;

public class Application {
    public static void main(String[] args) {
        ConfigurableApplicationContext context = SpringApplication.run(Application.class, args);
        
        // 여기에 종료 조건 또는 로직
        int exitCode = SpringApplication.exit(context);
        System.exit(exitCode);
    }
}
```

이 코드는 `SpringApplication.exit()` 메소드를 호출하여 스프링 부트 애플리케이션을 종료합니다. 이 메소드는 `ApplicationContext`를 매개변수로 받아 애플리케이션을 안전하게 종료시키고, 시스템에 전달할 종료 코드를 반환합니다.

## EventListener 활용하기

`ApplicationListener` 인터페이스를 구현하여 커스텀 이벤트 리스너를 만들 수도 있습니다. 이를 통해 애플리케이션의 다양한 생명주기 이벤트에 반응할 수 있습니다.

```java
import org.springframework.context.ApplicationListener;
import org.springframework.context.event.ContextClosedEvent;

public class CustomShutdownListener implements ApplicationListener<ContextClosedEvent> {
    @Override
    public void onApplicationEvent(ContextClosedEvent event) {
        // 종료 로직
    }
}
```

이 방법은 애플리케이션의 다양한 이벤트에 반응해야 할 때 유용합니다. 예를 들어, 데이터베이스 연결을 해제하거나 특정 리소스를 해제해야 할 때 이 방식을 사용할 수 있습니다.

## 결론

스프링 부트 애플리케이션을 프로그래밍 방식으로 종료하는 방법은 크게 두 가지입니다. `ApplicationContext`와 `SpringApplication.exit()`을 사용하는 방법, 그리고 `ApplicationListener`를 활용하는 방법입니다. 상황과 필요에 따라 적절한 방법을 선택하여 애플리케이션을 안전하게 종료할 수 있습니다.