---
title: Spring MVC의 @PathVariable 값이 잘리는 현상
date: 2023-09-26 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringMVC
  - PathVariable
---
## 문제 정의

Spring MVC에서 `@PathVariable` 어노테이션을 사용할 때 가끔 값이 잘려 나오는 문제가 발생할 수 있습니다. 이 글에서는 그 현상의 원인과 해결 방법에 대해 설명합니다.

## 원인: 잘림 현상

일반적으로 이러한 문제의 원인은 URL에 특수 문자가 포함되어 있는 경우입니다. 예를 들어, `/something/value1/value2;value3` 이라는 URL에서 `value2;value3` 부분을 `@PathVariable`로 받으려고 하면, `;` 문자 때문에 값이 잘릴 수 있습니다. 이러한 문자는 URL에서 특별한 의미를 가지므로, Spring MVC는 이를 고려하여 처리합니다.

## 해결책: URL 디코딩 설정 변경

이 문제를 해결하기 위해 Spring MVC 설정에서 URL 디코딩을 변경할 수 있습니다. `web.xml` 파일에 다음과 같은 설정을 추가해야 합니다.

```xml
<servlet>
    <servlet-name>appServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
        <param-name>decodePathVariables</param-name>
        <param-value>false</param-value>
    </init-param>
</servlet>
```

이 설정은 `decodePathVariables`를 `false`로 설정하여, URL의 특수 문자를 자동으로 디코딩하지 않게 합니다.

## 주의사항: 보안 측면

위의 설정 변경은 문제를 해결할 수 있지만, URL을 그대로 사용하게 되므로 보안 측면에서 주의가 필요합니다. URL에 민감한 정보가 포함되어 있을 경우, 이를 적절히 처리하는 로직이 추가로 필요합니다.

## 정리

`@PathVariable` 값이 잘리는 문제는 URL에 특수 문자가 포함되어 있을 때 발생하는 경우가 많습니다. 이를 해결하기 위해 `web.xml` 설정에서 `decodePathVariables`를 `false`로 설정할 수 있습니다. 그러나 이 설정 변경에는 보안 측면에서 주의가 필요합니다.