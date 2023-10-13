---
title: Spring MVC에서 GET 요청으로 날짜 파라미터 받기
date: 2023-09-20 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringMVC
  - GET요청
  - 날짜파라미터
---
## 요약
이 글에서는 Spring MVC에서 GET 요청을 통해 날짜 파라미터를 받는 방법을 자세히 살펴봅니다. 이 과정에서 `@RequestParam` 어노테이션과 `SimpleDateFormat` 클래스의 중요성에 대해 알아볼 것입니다.

## @RequestParam 어노테이션 사용하기
Spring MVC에서는 `@RequestParam` 어노테이션을 사용하여 HTTP 요청의 파라미터를 메서드 인자로 받을 수 있습니다. 날짜를 처리하기 위해선, 해당 인자를 `java.util.Date` 타입으로 선언하고, 날짜 형식을 지정할 수 있습니다.

```java
@RequestMapping("/getDate")
public String getDate(@RequestParam("date") @DateTimeFormat(pattern="yyyy-MM-dd") Date date) {
    // 코드 구현
}
```

여기서 `@DateTimeFormat`은 날짜 형식을 지정해주는 어노테이션입니다. 이를 사용하면 문자열 형태의 날짜를 `Date` 객체로 자동 변환해줍니다.

## SimpleDateFormat 클래스를 이용한 수동 변환
`SimpleDateFormat` 클래스를 사용하면 수동으로 날짜 파라미터를 변환할 수 있습니다. 이 방법은 `@RequestParam`을 `String` 타입으로 받아서, 코드 내에서 날짜로 변환하는 경우에 사용됩니다.

```java
@RequestMapping("/getDate")
public String getDate(@RequestParam("date") String dateString) throws ParseException {
    SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd");
    Date date = format.parse(dateString);
    // 코드 구현
}
```

`ParseException`은 날짜 형식이 잘못되었을 경우 발생하는 예외입니다. 그래서 이를 처리하기 위해 `throws ParseException`을 메서드에 추가해줍니다.

## 장단점 비교
- `@RequestParam`과 `@DateTimeFormat`: 코드가 간결하고, Spring이 자동으로 처리해줍니다. 하지만 형식이 고정되어 유연성이 떨어집니다.
- `SimpleDateFormat`: 유연성이 높고, 다양한 날짜 형식을 수용할 수 있습니다. 하지만 코드가 복잡해질 수 있고, 예외 처리가 필요합니다.

## 결론
Spring MVC에서 날짜 파라미터를 받는 방법은 주로 두 가지입니다. `@RequestParam`과 `@DateTimeFormat`을 사용하는 방법은 간결하지만 유연성이 떨어집니다. 반면 `SimpleDateFormat`을 사용하는 방법은 유연하지만 코드가 복잡해질 수 있습니다. 상황과 요구사항에 따라 적절한 방법을 선택하면 됩니다.