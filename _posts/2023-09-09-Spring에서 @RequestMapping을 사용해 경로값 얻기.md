---
title: Spring에서 @RequestMapping을 사용해 경로값 얻기
date: 2023-09-09 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - RequestMapping
---
## @RequestMapping 이해하기

Spring Framework에서는 HTTP 요청을 Java 메서드에 매핑할 때 `@RequestMapping` 애노테이션을 사용합니다. 이 애노테이션을 메서드 위에 추가하면 해당 메서드가 특정 URL에 응답하게 됩니다.

## 경로 변수(Path Variable) 가져오기

코드에서 경로의 일부분을 변수로 사용하려면 `{}`로 묶어 변수명을 지정합니다. 이러한 변수를 경로 변수(Path Variable)라고 합니다. 예를 들어, `/greeting/{name}`와 같이 URL을 지정하면 `{name}` 부분이 변수가 됩니다.

Java 메서드에서는 `@PathVariable` 애노테이션을 사용해 경로 변수를 가져올 수 있습니다. 예를 들어, 다음과 같이 작성할 수 있습니다.

```java
@RequestMapping("/greeting/{name}")
public String greeting(@PathVariable String name) {
    return "Hello, " + name;
}
```

## `@RequestMapping`에서 경로 가져오기

질문에서는 `@RequestMapping`을 사용하여 전체 경로를 얻으려는 것으로 보입니다. 이를 위해서는 `HttpServletRequest` 객체를 파라미터로 받아야 합니다.

```java
@RequestMapping("/example")
public String example(HttpServletRequest request) {
    String path = request.getRequestURI();
    return "The path is: " + path;
}
```

이 메서드에서 `HttpServletRequest` 객체의 `getRequestURI` 메서드를 호출하면 요청 경로를 얻을 수 있습니다.

## 요약

- `@RequestMapping`은 Spring에서 HTTP 요청을 Java 메서드에 매핑합니다.
- `{}`를 사용해 URL의 일부를 변수로 만들 수 있고, `@PathVariable`로 가져올 수 있습니다.
- 전체 경로를 얻으려면 `HttpServletRequest` 객체의 `getRequestURI` 메서드를 사용하면 됩니다.

이러한 방법들을 적절히 활용하면 Spring 애플리케이션에서 다양한 URL 패턴과 데이터를 쉽게 다룰 수 있습니다.