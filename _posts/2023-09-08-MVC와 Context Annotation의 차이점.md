---
title: MVC와 Context Annotation의 차이점
date: 2023-09-08 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - MVC
  - ContextAnnotation
---
## 개요

이 글에서는 웹 개발에서 자주 사용되는 두 가지 스프링 프레임워크 어노테이션, `<mvc:annotation-driven>`과 `<context:annotation-config>`의 차이점을 자세히 알아보겠습니다. 이 두 어노테이션은 비슷해 보이지만, 각자 다르게 활용되며 특정 작업에 더 적합합니다.

## `<mvc:annotation-driven>`의 특징

`<mvc:annotation-driven>`은 스프링 MVC에 관련된 설정을 활성화합니다. 이 어노테이션을 사용하면 다음과 같은 기능이 자동으로 설정됩니다.

- `@Controller` 어노테이션이 달린 클래스를 찾아서 빈(Bean)으로 등록
- 요청 매핑, 데이터 바인딩, 데이터 유효성 검사 등
- JSON, XML과 같은 데이터 포맷으로 자동 변환

여기서 빈(Bean)이라는 것은 스프링에서 관리하는 객체를 의미합니다. 요청 매핑이라는 것은 클라이언트의 HTTP 요청을 어떤 메서드가 처리할지 연결해주는 것을 의미합니다.

## `<context:annotation-config>`의 특징

`<context:annotation-config>`은 스프링의 핵심 컨테이너에 관련된 어노테이션 설정을 활성화합니다. 이 어노테이션을 사용하면 다음과 같은 기능이 활성화됩니다.

- `@Component`, `@Repository`, `@Service` 등의 일반 어노테이션을 활용한 빈 설정
- `@Autowired`, `@Resource` 등을 통한 의존성 주입

의존성 주입이라는 것은 하나의 객체가 다른 객체를 사용할 수 있게 연결해주는 기능을 의미합니다.

## 언제 어떤 것을 사용해야 할까?

- 웹 애플리케이션을 개발할 때는 `<mvc:annotation-driven>`을 사용하면 좋습니다.
- 핵심 비즈니스 로직을 개발하거나 일반적인 애플리케이션 설정을 할 때는 `<context:annotation-config>`를 사용합니다.

## 결론

`<mvc:annotation-driven>`과 `<context:annotation-config>`은 각각 다른 목적과 책임을 가지고 있습니다. `<mvc:annotation-driven>`은 주로 웹 관련 설정을, `<context:annotation-config>`는 일반적인 스프링 설정을 담당합니다. 두 설정은 명확한 구분이 있으며, 특정 상황에서 더 적합한 설정을 선택하여 사용하면 됩니다.