---
title: Spring Boot에서 @RequestParam 빈 값 처리하기
date: 2023-08-27 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - RequestParam
---
## defaultValue 속성을 사용하여 빈 값 처리

Spring Boot에서는 `@RequestParam` 어노테이션을 사용하여 HTTP 요청에서 파라미터를 가져옵니다. 이 어노테이션은 `defaultValue` 속성을 가지고 있는데, 이것은 파라미터 값이 없거나 빈 문자열일 경우 사용됩니다.

예를 들어, 아래의 코드는 `name` 파라미터가 빈 문자열이거나 없을 때 "Anonymous"라는 기본값을 설정합니다.

```java
@RequestMapping("/greet")
public String greet(@RequestParam(name = "name", defaultValue = "Anonymous") String name) {
    return "Hello, " + name;
}
```

## `required` 속성과 `defaultValue` 속성의 조합

`@RequestParam`에서 `required` 속성과 `defaultValue` 속성을 동시에 사용할 수도 있습니다. `required` 속성이 `false`로 설정되면, 해당 파라미터가 없어도 에러가 발생하지 않습니다. 그러나 이 경우에도 `defaultValue`가 설정되어 있다면 그 값이 사용됩니다.

```java
@RequestMapping("/sayHello")
public String sayHello(@RequestParam(name = "name", required = false, defaultValue = "Guest") String name) {
    return "Hello, " + name;
}
```

## 주의할 점

만약 `required` 속성이 `true`로 설정되고 `defaultValue`가 설정되지 않았다면, 해당 파라미터가 없을 경우 `MissingServletRequestParameterException`이 발생합니다. 이 예외는 요청에 필요한 파라미터가 없을 때 발생하는 예외입니다.

## 요약

Spring Boot에서 `@RequestParam` 어노테이션을 사용할 때, `defaultValue`와 `required` 속성을 적절히 조합하여 빈 값이나 누락된 파라미터를 효과적으로 처리할 수 있습니다. 이를 통해 더 안정적인 웹 애플리케이션을 만들 수 있습니다.