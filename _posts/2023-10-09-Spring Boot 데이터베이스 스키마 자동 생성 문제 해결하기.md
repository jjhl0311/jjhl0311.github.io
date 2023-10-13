---
title: Spring Boot 데이터베이스 스키마 자동 생성 문제 해결하기
date: 2023-10-09 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - 데이터베이스
  - 스키마
---
## 오류 내용 및 문제 상황

Spring Boot 프로젝트에서 자동으로 데이터베이스 스키마를 생성할 수 없다는 문제가 있습니다. 특히, 이 문제는 `spring.jpa.hibernate.ddl-auto` 설정과 관련이 있습니다. 오류 이름은 "Unable to get Spring Boot to automatically create database schema" 입니다.

## 기본 설정 검토하기

Spring Boot에서 데이터베이스 스키마를 자동으로 생성하려면 `application.properties` 또는 `application.yml` 파일에 몇 가지 설정을 추가해야 합니다. `spring.jpa.hibernate.ddl-auto` 설정은 데이터베이스 스키마의 생성 및 업데이트 방식을 제어합니다. 이 설정에는 `create`, `update`, `create-drop`, `validate`, `none` 등의 값을 사용할 수 있습니다.

- `create`: 애플리케이션 시작 시 데이터베이스 스키마를 생성합니다.
- `update`: 애플리케이션 시작 시 필요한 경우 데이터베이스 스키마를 업데이트합니다.
- `create-drop`: 애플리케이션 종료 시 데이터베이스 스키마를 삭제합니다.
  
## 데이터베이스 드라이버와의 호환성 확인

데이터베이스 드라이버와 Hibernate 버전이 서로 호환되는지 확인해야 합니다. `pom.xml` 또는 `build.gradle` 파일에서 의존성을 정확하게 설정했는지 검토하세요. 또한, 이 설정은 데이터베이스 엔진 (MySQL, PostgreSQL, H2 등)에 따라 다르게 동작할 수 있으므로 주의가 필요합니다.

## 로깅 레벨 조정

문제를 해결하기 위해 Hibernate가 내부에서 어떤 작업을 수행하는지 알고 싶다면, 로깅 레벨을 조정할 수 있습니다. `application.properties` 파일에 `logging.level.org.hibernate=DEBUG`를 추가하여 로그의 세부 정보를 확인할 수 있습니다.

## 추가적인 설정

만약 위의 방법으로 문제가 해결되지 않는다면, `@EntityScan` 어노테이션을 사용하여 스캔할 패키지를 지정할 수 있습니다. 이 방법은 특히 여러 모듈을 사용하는 대형 프로젝트에서 유용합니다.

## 정리

Spring Boot에서 데이터베이스 스키마를 자동으로 생성하는 문제는 주로 설정과 의존성, 버전 호환성에 관한 문제입니다. `application.properties` 파일의 `spring.jpa.hibernate.ddl-auto` 설정을 조정하고, 필요한 의존성과 버전을 확인하여 문제를 해결할 수 있습니다.