---
title: Spring Security 인증 예외 처리하기
date: 2023-10-02 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringSecurity
---
## 예외란 무엇인가?

프로그래밍에서 예외(Exception)는 일반적인 프로그램 흐름을 방해하는 이벤트입니다. 예를 들어, 사용자 인증(Authentication) 실패, 데이터베이스 접근 오류 등이 이에 해당합니다. Spring Security에서는 이러한 예외를 잡아서 적절히 처리할 수 있는 방법을 제공합니다.

## Spring Security 인증 예외의 종류

Spring Security에서는 다양한 인증 예외가 있습니다. 주요한 예외는 `AuthenticationException`이며, 이것은 다시 여러 하위 예외로 나뉩니다. 가장 흔한 하위 예외는 `BadCredentialsException`으로, 잘못된 아이디나 패스워드를 입력했을 때 발생합니다. 다른 하위 예외로는 `AccountExpiredException`, `DisabledException` 등이 있습니다.

## `@ExceptionHandler`를 이용한 예외 처리

Spring Framework에서는 `@ExceptionHandler` 어노테이션을 사용하여 특정 예외를 잡아서 처리할 수 있습니다. 이 어노테이션은 Controller 클래스 안에서 사용되며, 메소드에 적용됩니다.

```java
@ControllerAdvice
public class GlobalExceptionHandler {

  @ExceptionHandler(AuthenticationException.class)
  public ResponseEntity<String> handleAuthenticationException(AuthenticationException e) {
    return new ResponseEntity<>("Authentication failed", HttpStatus.UNAUTHORIZED);
  }
}
```

이 코드에서 `@ControllerAdvice`는 전역 예외 처리기를 정의합니다. `@ExceptionHandler(AuthenticationException.class)`는 `AuthenticationException`을 잡아서 처리하겠다는 뜻입니다. 이 메소드 내에서는 HTTP 상태 코드 `401 Unauthorized`를 반환하고 "Authentication failed"라는 메시지를 보내고 있습니다.

## 정리

Spring Security에서 인증 예외를 처리하는 것은 중요한 작업 중 하나입니다. `@ExceptionHandler`를 사용하면 이를 깔끔하게 해결할 수 있습니다. 이 방법을 통해 사용자에게 명확한 에러 메시지와 적절한 상태 코드를 전달할 수 있어, 더 나은 사용자 경험을 제공할 수 있습니다.