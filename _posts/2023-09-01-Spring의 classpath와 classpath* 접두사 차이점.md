---
title: Spring의 classpath와 classpath* 접두사 차이점
date: 2023-09-01 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - classpath
---
## classpath와 classpath* 개요

`classpath`와 `classpath*`는 Spring Framework에서 자주 사용되는 두 가지 경로 접두사입니다. 이 두 접두사는 리소스를 로드할 때 사용되며, 둘 사이에는 중요한 차이점이 있습니다.

## classpath 사용시 특징

`classpath` 접두사를 사용할 경우, Spring은 클래스 경로(Classpath)에서 **첫 번째로 발견되는 리소스만 로드**합니다. 이는 주로 하나의 설정 파일이나 리소스 파일을 로드할 때 유용합니다. 클래스 경로는 컴파일된 클래스 파일이나 라이브러리 파일이 저장되어 있는 디렉토리 경로를 의미합니다.

예를 들어, `classpath:application.properties` 형식을 사용하면, Spring은 클래스 경로에서 `application.properties`라는 이름의 첫 번째 파일만 찾아 로드합니다.

## classpath* 사용시 특징

`classpath*` 접두사를 사용하면, Spring은 **클래스 경로상의 모든 일치하는 리소스를 로드**합니다. 이는 여러 모듈 또는 라이브러리에서 동일한 이름의 설정 파일이 있을 경우 유용합니다.

예를 들어, `classpath*:application.properties` 형식을 사용하면, 클래스 경로에 있는 모든 `application.properties` 파일을 찾아 로드합니다.

## 주의할 점

- `classpath`는 보통 빠른 로딩 속도를 제공하지만, 여러 설정 파일 중 하나만 로드됩니다.
- `classpath*`는 모든 일치하는 파일을 로드하지만, 로딩 속도가 느릴 수 있고, 리소스가 중복되어 로드될 가능성이 있습니다.

## 정리

간단히 말해, `classpath`는 효율성을 위해 하나의 파일만 로드하는 반면, `classpath*`는 유연성을 위해 모든 일치하는 파일을 로드합니다. 어떤 접두사를 사용할지는 프로젝트의 요구사항과 상황에 따라 결정해야 합니다.