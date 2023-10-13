---
title: 스프링에서 동일 인터페이스로 구현한 빈 Autowiring 문제 해결
date: 2023-09-24 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - Autowiring문제
---
## 'NoSuchBeanDefinitionException' 오류와 그 원인

스프링(Spring) 프레임워크에서 빈(Bean)을 자동 주입(Autowiring)할 때, 동일한 인터페이스를 구현한 두 개 이상의 빈이 존재하면 `NoSuchBeanDefinitionException` 오류가 발생할 수 있습니다. 이 오류는 스프링이 어떤 빈을 주입해야 할지 결정하지 못해서 나타납니다. 여기서 빈은 스프링 컨테이너에서 관리되는 객체를 의미하며, 인터페이스는 두 개 이상의 클래스가 공통 기능을 가지도록 도와주는 구조입니다.

## 해결 방법 1: `@Primary` 애너테이션 사용

먼저, `@Primary` 애너테이션을 사용하여 기본 빈을 지정할 수 있습니다. 이 애너테이션을 클래스에 추가하면, 해당 클래스가 기본 빈으로 설정됩니다. 그렇게 하면 동일한 인터페이스를 구현한 다른 빈들보다 우선순위가 높아집니다.

```java
@Primary
public class DefaultMyService implements MyService {
  // 구현 코드
}
```

## 해결 방법 2: `@Qualifier` 애너테이션 사용

두 번째로는 `@Qualifier` 애너테이션을 사용할 수 있습니다. 이 애너테이션은 어떤 빈을 주입할지 명시적으로 지정해 줄 수 있습니다. `@Autowired` 애너테이션과 함께 사용되며, 다음과 같이 코드를 작성할 수 있습니다.

```java
@Autowired
@Qualifier("specificMyService")
public void setMyService(MyService myService) {
  // 구현 코드
}
```

## 해결 방법 3: `@Resource` 애너테이션 사용

세 번째 방법은 `@Resource` 애너테이션을 사용하는 것입니다. 이 방법도 빈을 명시적으로 지정해 줄 수 있으며, `@Resource(name = "specificMyService")` 처럼 작성합니다.

```java
@Resource(name = "specificMyService")
public void setMyService(MyService myService) {
  // 구현 코드
}
```

## 결론

동일한 인터페이스를 구현한 두 개 이상의 빈이 있을 때, 스프링에서 자동 주입을 처리하기 위한 방법은 여러 가지입니다. `@Primary`, `@Qualifier`, `@Resource` 애너테이션을 통해 이 문제를 해결할 수 있으므로, 상황에 따라 적절한 방법을 선택하면 됩니다.