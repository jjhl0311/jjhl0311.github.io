---
title: Spring Boot에서 통합 테스트를 위한 기본 프로필 설정 방법
date: 2023-09-05 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
---
## 서론
Spring Boot는 자바 기반의 웹 개발 프레임워크입니다. Spring Boot를 사용할 때 테스트 환경과 실제 운영 환경을 분리하기 위해 다양한 프로필을 사용할 수 있습니다. 이 글에서는 Spring Boot에서 통합 테스트를 위한 기본 프로필을 설정하는 방법에 대해 자세히 알아보겠습니다.

## 통합 테스트란 무엇인가?

통합 테스트(Integration Test)는 개별 컴포넌트가 서로 연결될 때 올바르게 작동하는지 검사하는 테스트입니다. 예를 들어, 데이터베이스, 캐싱 시스템 등과의 연동을 검증할 수 있습니다.

## 프로필(Profile)이란?

프로필은 특정 환경에 맞는 설정을 담고 있는 구성 파일입니다. 예를 들어, 개발 환경(`dev`), 테스트 환경(`test`), 운영 환경(`prod`) 등을 다르게 설정할 수 있습니다.

## `@ActiveProfiles` 어노테이션 사용하기

JUnit을 사용하는 Spring Boot 테스트에서는 `@ActiveProfiles` 어노테이션을 사용하여 테스트에 사용할 프로필을 지정할 수 있습니다. 이 어노테이션을 사용하면 테스트를 실행할 때 지정한 프로필이 활성화됩니다.

```java
@SpringBootTest
@ActiveProfiles("test")
public class MyIntegrationTest {
    // 테스트 코드
}
```

## `application.properties`와 `application-test.properties`

`application.properties` 파일은 기본 설정을 담고 있습니다. 테스트 전용 프로필을 사용하려면 `application-test.properties` 파일을 생성하고 그 안에 테스트 환경에 맞는 설정을 입력하세요. `@ActiveProfiles("test")` 어노테이션을 사용하면 `application-test.properties` 파일의 설정이 적용됩니다.

## 정리

Spring Boot에서는 통합 테스트를 위한 별도의 프로필을 쉽게 설정할 수 있습니다. `@ActiveProfiles` 어노테이션과 `application-test.properties` 파일을 활용하여 테스트 환경을 구성할 수 있습니다. 이를 통해 개발과 테스트, 운영 간의 설정을 명확하게 분리하여 효율적인 개발이 가능합니다.