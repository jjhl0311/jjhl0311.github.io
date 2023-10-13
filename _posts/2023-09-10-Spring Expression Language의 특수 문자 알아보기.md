---
title: Spring Expression Language의 특수 문자 알아보기
date: 2023-09-10 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - Expression
  - Language
---
## 무엇이 다른가?

Spring Expression Language(SpEL)은 Spring 프레임워크에서 사용하는 강력한 표현 언어입니다. SpEL을 사용할 때는 주로 두 가지 특수 문자, `$`와 `#`을 볼 수 있습니다. 이 두 특수 문자는 서로 다른 작업을 수행하므로 그 차이를 이해하는 것이 중요합니다.

## `$` 기호의 역할

`$` 기호는 주로 프로퍼티 파일의 값을 불러올 때 사용됩니다. 프로퍼티 파일에 정의된 설정값을 읽어와 Spring 빈에 주입할 때 이 기호를 사용합니다.

```java
@Value("${database.url}")
private String databaseUrl;
```

이 코드는 `database.url`이라는 이름으로 프로퍼티 파일에 저장된 데이터베이스 URL을 `databaseUrl` 변수에 할당합니다.

## `#` 기호의 역할

반면에 `#` 기호는 Spring 빈의 메서드나 속성을 평가하고 실행하는 데 사용됩니다. 이 기호를 사용하면 런타임 시에 동적으로 값을 평가하거나 변경할 수 있습니다.

```java
@Value("#{T(java.lang.Math).random() * 100.0}")
private double randomValue;
```

이 코드는 Java의 `Math.random()` 메서드를 호출하여 0부터 100 사이의 랜덤한 값을 `randomValue` 변수에 할당합니다.

## 어떨 때 어떤 기호를 사용해야 하는가?

- 프로퍼티 파일에서 값을 가져와야 할 경우: `$` 기호를 사용합니다.
- Spring 빈의 메서드나 속성을 동적으로 평가해야 할 경우: `#` 기호를 사용합니다.

따라서 `$`와 `#` 두 기호는 각각의 상황과 필요에 따라 선택하여 사용하면 됩니다. 이 두 기호를 정확하게 이해하고 사용하면 Spring 프레임워크에서 더욱 효율적으로 작업할 수 있습니다.