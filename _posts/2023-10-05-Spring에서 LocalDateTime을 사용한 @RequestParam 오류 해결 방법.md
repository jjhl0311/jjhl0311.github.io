---
title: Spring에서 LocalDateTime을 사용한 @RequestParam 오류 해결 방법
date: 2023-10-05 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - LocalDateTime
  - RequestParam
---
## 문제 상황과 에러 메시지

Java의 Spring 프레임워크에서 웹 애플리케이션을 개발하다 보면, 날짜와 시간을 다루기 위해 `LocalDateTime` 클래스를 사용할 일이 많습니다. 이 클래스를 이용하여 API나 웹 페이지의 파라미터를 처리하려고 할 때 `@RequestParam` 애노테이션을 사용하곤 하는데, 이때 간혹 아래와 같은 에러 메시지를 마주할 수 있습니다.

```plaintext
Failed to convert string to LocalDateTime
```

이 에러 메시지가 의미하는 바는, 문자열을 `LocalDateTime` 객체로 변환하는 과정에서 실패했다는 것입니다.

## 해결 방법 1: DateTimeFormatter 사용하기

첫 번째로 권장하는 방법은 `DateTimeFormatter`를 사용하는 것입니다. `DateTimeFormatter`는 Java에서 날짜와 시간을 문자열로부터 변환하거나, 문자열로 출력할 때 사용하는 클래스입니다.

```java
import java.time.format.DateTimeFormatter;

@RequestMapping(value = "/some-endpoint")
public String someEndpoint(@RequestParam("date") String dateStr) {
    DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
    LocalDateTime dateTime = LocalDateTime.parse(dateStr, formatter);
    // 나머지 코드
}
```

## 해결 방법 2: @DateTimeFormat 애노테이션 사용하기

두 번째 방법은 `@DateTimeFormat` 애노테이션을 사용하는 것입니다. 이 애노테이션을 `@RequestParam` 애노테이션과 함께 사용하여 문제를 해결할 수 있습니다.

```java
import org.springframework.format.annotation.DateTimeFormat;

@RequestMapping(value = "/some-endpoint")
public String someEndpoint(@RequestParam("date") @DateTimeFormat(pattern = "yyyy-MM-dd HH:mm:ss") LocalDateTime date) {
    // 나머지 코드
}
```

## 해결 방법 3: 커스텀 Converter 구현하기

세 번째 방법은 별도의 `Converter` 클래스를 구현하여 Spring에 등록하는 것입니다. 이 방법은 복잡한 변환 로직이 필요할 때 유용합니다.

```java
import org.springframework.core.convert.converter.Converter;

public class StringToLocalDateTimeConverter implements Converter<String, LocalDateTime> {
    @Override
    public LocalDateTime convert(String source) {
        // 변환 로직
    }
}
```

## 결론

`LocalDateTime`과 `@RequestParam`을 함께 사용하면서 발생하는 변환 문제는 여러 가지 방법으로 해결 가능합니다. 프로젝트의 요구 사항과 개발 환경에 맞춰 적절한 방법을 선택하면 됩니다. 이렇게 하면 "Failed to convert string to LocalDateTime" 같은 에러 메시지를 효과적으로 해결할 수 있습니다.