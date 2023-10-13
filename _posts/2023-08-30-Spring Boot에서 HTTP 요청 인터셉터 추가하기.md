---
title: Spring Boot에서 HTTP 요청 인터셉터 추가하기
date: 2023-08-30 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - HTTP
---
## 들어가기 전에: 인터셉터란?

인터셉터(interceptor)란 클라이언트와 서버 사이의 통신 과정에서 특정 로직을 수행하도록 설계된 컴포넌트입니다. 이를 통해 로깅, 인증과 같은 작업을 중앙에서 처리할 수 있습니다.

## 주요 문제: `WebMvcConfigurer` 인터페이스 활용

Spring Boot 프로젝트에서 HTTP 요청 인터셉터를 추가하려면 `WebMvcConfigurer` 인터페이스를 구현해야 합니다. 이 인터페이스에는 `addInterceptors`라는 메소드가 있어서 여기에 인터셉터를 등록할 수 있습니다.

### 예제 코드: 인터셉터 등록하기

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
  
  @Override
  public void addInterceptors(InterceptorRegistry registry) {
    registry.addInterceptor(new MyInterceptor());
  }
}
```

`@Configuration` 애너테이션을 사용하여 설정 클래스임을 명시합니다. 그리고 `WebMvcConfigurer`의 `addInterceptors` 메소드를 오버라이딩합니다. 여기서 `MyInterceptor`는 우리가 구현한 인터셉터 클래스입니다.

## 오류 해결: `NoSuchBeanDefinitionException`

`NoSuchBeanDefinitionException`이 발생하면 스프링이 요청한 빈(Bean)을 찾을 수 없다는 의미입니다. 이 문제는 주로 빈의 스코프와 관련이 있을 가능성이 높습니다.

### 해결방법

1. `@Component` 또는 `@Service` 애너테이션을 사용하여 인터셉터 클래스에 빈으로 등록하십시오.
2. 빈의 스코프를 확인하고 필요하면 조정하십시오.

```java
@Component
public class MyInterceptor extends HandlerInterceptorAdapter {
  // ...
}
```

## 마치며

Spring Boot에서 인터셉터를 설정하는 방법은 매우 단순합니다. 이를 통해 여러 HTTP 요청에 대한 중앙 관리가 가능하므로, 로깅이나 인증 같은 기능을 효율적으로 구현할 수 있습니다. `NoSuchBeanDefinitionException` 같은 문제가 발생하면, 빈 설정을 확인하여 문제를 해결할 수 있습니다.