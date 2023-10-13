---
title: Spring Boot에서 다양한 HTTP 상태 코드 반환하기
date: 2023-09-12 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - HTTP상태
---
## 서론: 왜 HTTP 상태 코드는 중요한가?

HTTP 상태 코드는 웹 서버와 클라이언트 사이의 상호작용에서 매우 중요한 역할을 합니다. 코드를 통해 클라이언트에게 어떤 일이 발생했는지 알려주기 때문입니다. 예를 들어, `200 OK`는 성공적인 요청을 의미하고, `404 Not Found`는 원하는 리소스가 없다는 것을 나타냅니다. 이번에는 Spring Boot를 사용하여 다양한 HTTP 상태 코드를 어떻게 반환할 수 있는지 알아보겠습니다.

## 방법 1: `ResponseEntity`를 이용한 방법

`ResponseEntity`는 HTTP 응답을 상세하게 설정할 수 있습니다. 상태 코드, 헤더, 본문 등을 모두 포함시킬 수 있습니다.

```java
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class MyController {
    @GetMapping("/example")
    public ResponseEntity<String> example() {
        return new ResponseEntity<>("Hello World", HttpStatus.OK);
    }
}
```

이 코드에서 `HttpStatus.OK`는 HTTP 상태 코드 200을 의미합니다.

## 방법 2: `@ResponseStatus` 어노테이션 사용

메서드 또는 예외 클래스에 `@ResponseStatus` 어노테이션을 붙여서 상태 코드를 지정할 수 있습니다.

```java
import org.springframework.web.bind.annotation.ResponseStatus;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.http.HttpStatus;

@RestController
public class MyController {
    @ResponseStatus(HttpStatus.NOT_FOUND)
    @GetMapping("/example")
    public String example() {
        return "Resource not found";
    }
}
```

이 방법을 사용하면 해당 메서드가 호출될 때 자동으로 `HttpStatus.NOT_FOUND` 상태 코드가 반환됩니다.

## 방법 3: 예외 처리기를 이용한 방법

커스텀 예외를 생성하고, `@ControllerAdvice`나 `@ExceptionHandler`를 이용하여 해당 예외가 발생했을 때 반환할 상태 코드를 지정할 수 있습니다.

```java
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;

@ControllerAdvice
public class MyExceptionHandler {
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<String> handleResourceNotFoundException() {
        return new ResponseEntity<>("Resource not found", HttpStatus.NOT_FOUND);
    }
}
```

이 방법은 전역적으로 예외를 처리할 때 유용합니다.

## 결론: 어떤 방법을 선택할까?

여러 방법이 있지만, 상황에 따라 적절한 방법을 선택하는 것이 중요합니다. `ResponseEntity`는 상세한 설정이 필요할 때, `@ResponseStatus`는 간단한 경우에, 예외 처리기는 전역적인 설정에 유용합니다. 이로써 Spring Boot에서 다양한 HTTP 상태 코드를 반환하는 방법을 알아보았습니다. 이를 통해 더 효과적인 웹 서비스를 개발할 수 있을 것입니다.