---
title: Spring MVC와 AJAX를 이용한 다중 변수 전달 방법
date: 2023-09-02 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringMVC
  - AJAX
  - 다중변수
---
## 문제 상황: `@RequestBody`로 다중 변수 전달이 안 됨

Spring MVC에서 AJAX를 이용해 서버로 데이터를 보낼 때, `@RequestBody` 어노테이션을 사용하면 간단하게 JSON 형태의 데이터를 받을 수 있습니다. 그런데 이 때 다수의 변수를 어떻게 전달할 수 있을까요? 다음과 같은 오류가 자주 발생합니다.

- Error: `Bad Request`

## 해결 방법 1: DTO 사용하기

DTO(Data Transfer Object)는 데이터를 객체화해서 서버와 클라이언트 간에 전송하는 방법입니다. Spring MVC에서는 `@RequestBody`를 사용해서 DTO를 통해 다수의 변수를 한 번에 받을 수 있습니다.

```java
public class MyDTO {
    private String variable1;
    private int variable2;
    // getter와 setter
}
```

컨트롤러에서는 다음과 같이 사용합니다.

```java
@RequestMapping(value="/someEndpoint", method=RequestMethod.POST)
public ResponseEntity<String> someMethod(@RequestBody MyDTO myDTO) {
    // 로직
}
```

## 해결 방법 2: `Map<String, Object>` 사용하기

`Map`은 키와 값 쌍을 저장하는 자료구조입니다. 이를 이용하면 `@RequestBody`로 여러 변수를 동시에 받을 수 있습니다.

```java
@RequestMapping(value="/someEndpoint", method=RequestMethod.POST)
public ResponseEntity<String> someMethod(@RequestBody Map<String, Object> payload) {
    String variable1 = (String) payload.get("variable1");
    int variable2 = (int) payload.get("variable2");
    // 로직
}
```

## 해결 방법 3: JSON 객체를 이용하기

AJAX 호출을 할 때, JSON 객체를 만들어 여러 변수를 묶어 전송할 수 있습니다.

```javascript
$.ajax({
    url: '/someEndpoint',
    type: 'POST',
    contentType: 'application/json',
    data: JSON.stringify({variable1: 'someValue', variable2: 123}),
    // 로직
});
```

이렇게 세 가지 방법을 이용하면 Spring MVC와 AJAX에서 `@RequestBody`를 사용해 여러 변수를 효과적으로 전달할 수 있습니다.