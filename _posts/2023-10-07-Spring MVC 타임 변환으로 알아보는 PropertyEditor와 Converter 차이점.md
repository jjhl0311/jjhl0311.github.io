---
title: Spring MVC 타임 변환으로 알아보는 PropertyEditor와 Converter 차이점
date: 2023-10-07 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringMVC
  - PropertyEditor
  - Converter
---
## 서론

Spring MVC에서 데이터를 변환하거나 처리할 때 가장 중요한 것 중 하나는 타입 변환이다. 이 글에서는 `PropertyEditor`와 `Converter`라는 두 가지 메커니즘이 어떻게 다르고 어떻게 사용되는지를 자세하게 살펴볼 것입니다. 이 두 가지 메커니즘은 흔히 사용되지만, 그 차이점을 정확하게 이해하지 못하면 문제가 발생할 수 있습니다.

## PropertyEditor란?

`PropertyEditor`는 Java Beans에서 제공하는 인터페이스입니다. 이를 통해 문자열과 다른 타입 사이의 변환을 할 수 있습니다. 예를 들어, 사용자가 입력한 문자열을 Date 객체로 바꾸거나, 반대로 Date 객체를 문자열로 표현할 수 있습니다.

### 사용 방법

```java
public class CustomDateEditor extends PropertyEditorSupport {
    @Override
    public void setAsText(String text) throws IllegalArgumentException {
        // 문자열을 Date 객체로 변환하는 로직
    }

    @Override
    public String getAsText() {
        // Date 객체를 문자열로 변환하는 로직
    }
}
```

## Converter란?

`Converter`는 Spring 프레임워크에서 제공하는 인터페이스입니다. 이것도 `PropertyEditor`와 마찬가지로 두 개의 다른 타입 사이의 변환을 수행합니다.

### 사용 방법

```java
public class StringToDateConverter implements Converter<String, Date> {
    @Override
    public Date convert(String source) {
        // 문자열을 Date 객체로 변환하는 로직
    }
}
```

## 차이점

1. **API 출처**: `PropertyEditor`는 Java의 일반적인 인터페이스이지만, `Converter`는 Spring 프레임워크에 특화되어 있습니다.
2. **유연성**: `Converter`는 더 많은 유연성을 제공하고, `PropertyEditor`보다 코드가 간결합니다.
3. **에러 처리**: `PropertyEditor`에서는 `IllegalArgumentException`을 던져야 하지만, `Converter`에서는 타입 변환 실패 시 `ConversionFailedException`을 던집니다.

## 결론

`PropertyEditor`와 `Converter` 모두 타입 변환에 유용하지만, 각각의 사용 케이스와 선호도에 따라 선택할 수 있습니다. `Converter`가 더 최근에 나왔고, 코드가 간결해서 대부분의 경우에 이를 선호하게 됩니다. 그러나 둘 다 알고 있으면 Spring MVC에서 더 다양한 상황에 대응할 수 있습니다.