---
title: Spring의 @Component 어노테이션과 빈(Bean)의 관계
date: 2023-09-23 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - Component
  - Bean
---
## 어노테이션과 빈의 기본 이해

어노테이션(annotation)이란 코드에 메타데이터를 추가하는 방법입니다. 메타데이터는 '데이터에 대한 데이터'라고 이해하면 됩니다. Spring 프레임워크에서는 `@Component`라는 어노테이션을 사용하여 클래스를 빈(bean)으로 등록합니다. 빈은 Spring 컨테이너가 관리하는 객체입니다.

## @Component 어노테이션의 역할

`@Component` 어노테이션은 클래스에 붙여서 해당 클래스가 Spring 빈으로 자동 등록되게 하는 역할을 합니다. 이렇게 등록된 빈은 Spring 컨테이너에서 단일 인스턴스로 관리됩니다. 따라서 애플리케이션 전반에서 해당 빈의 인스턴스를 재사용할 수 있습니다.

## 클래스를 빈으로 만드는 다른 방법

`@Component` 외에도 `@Service`, `@Repository`, `@Controller` 등의 어노테이션을 사용하여 클래스를 빈으로 만들 수 있습니다. 이 어노테이션들은 내부적으로 `@Component`를 포함하고 있어, 결국은 빈으로 등록되는 것이 동일합니다.

## 주의할 점: Component-Scan

단순히 `@Component` 어노테이션을 붙이는 것만으로 빈이 자동으로 등록되지는 않습니다. Spring 설정에서 `component-scan`을 활성화하여 해당 패키지 내의 클래스를 빈으로 등록할 수 있도록 설정해야 합니다.

## 정리

`@Component` 어노테이션은 해당 클래스가 Spring 빈으로 동작하게 만들어 줍니다. 하지만 이것만으로는 충분하지 않고, `component-scan` 설정을 통해 Spring이 해당 클래스를 빈으로 인식하도록 해야 합니다. 다양한 어노테이션과 설정을 활용하여 빈을 효과적으로 관리할 수 있습니다.