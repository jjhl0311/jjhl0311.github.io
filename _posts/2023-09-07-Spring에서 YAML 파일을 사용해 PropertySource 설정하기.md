---
title: Spring에서 YAML 파일을 사용해 PropertySource 설정하기
date: 2023-09-07 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - YAML파일
  - PropertySource
---
## PropertySource란 무엇인가?

PropertySource는 Spring Framework에서 애플리케이션 설정을 관리하기 위한 메커니즘 중 하나입니다. 주로 `.properties` 또는 `.yml` 파일을 이용하여 변수나 설정값을 외부에서 불러옵니다. 이를 통해 코드 내부에서 값을 직접 정의하는 것보다 유연한 설정 변경이 가능합니다.

## YAML 파일 사용의 장점

YAML(Yet Another Markup Language)은 JSON과 비슷한 형식이지만, 사람이 읽고 쓰기 쉬운 구조를 가집니다. 들여쓰기를 사용하여 계층 구조를 나타내므로, 복잡한 설정도 쉽게 정의할 수 있습니다.

## YAML과 PropertySource 연동하기

Spring에서 YAML 파일을 사용하려면 다음과 같은 방법을 사용할 수 있습니다.

### Maven 또는 Gradle에 의존성 추가하기

Spring Boot를 사용한다면, `spring-boot-starter-data-yaml` 의존성을 프로젝트에 추가합니다.

### `@PropertySource` 애노테이션 사용하기

일반적으로 `.properties` 파일은 `@PropertySource("classpath:application.properties")`와 같이 쉽게 불러올 수 있습니다. 그러나 이 방법은 YAML 파일에는 적용되지 않습니다. 대신, `@ConfigurationProperties` 또는 `@Value` 애노테이션을 사용해야 합니다.

### `application.yml` 파일 작성하기

`src/main/resources` 디렉토리에 `application.yml` 파일을 생성하고 설정값을 입력합니다.

```yml
server:
  port: 8080
```

### 설정값 불러오기

Java 클래스에서 `@Value("${server.port}")`와 같은 방법으로 설정값을 불러옵니다.

## 주의사항: `FileNotFoundException`

`@PropertySource` 애노테이션을 YAML 파일에 사용하려고 하면, `FileNotFoundException`이 발생할 수 있습니다. 이는 Spring이 기본적으로 `.properties` 파일만 지원하기 때문입니다.

## 결론

Spring에서 YAML 파일을 사용하려면 몇 가지 추가적인 설정이 필요합니다. 특히, `@PropertySource` 애노테이션은 YAML 파일에 직접 사용할 수 없으므로, `@Value`나 `@ConfigurationProperties` 애노테이션을 사용해야 합니다. 이러한 방법을 통해 Spring 애플리케이션의 설정을 더욱 유연하게 관리할 수 있습니다.