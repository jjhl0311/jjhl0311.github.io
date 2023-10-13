---
title: Spring Boot REST 서비스에서 파일 다운로드하기
date: 2023-09-15 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - setMaxResults
---
## 문제 상황: 'FileNotFoundException' 오류

보통 Spring Boot REST 서비스에서 파일을 다운로드하는 과정에서 `FileNotFoundException`이라는 오류가 발생하는 경우입니다. 이 오류는 요청한 파일이 서버상에서 존재하지 않을 때 일어납니다. 그럼 이 문제를 어떻게 해결해야 할까요?

## 해결 방법 1: 경로 확인

첫 번째로 확인해야 할 것은 파일 경로입니다. 파일 경로가 정확한지 다시 한 번 검토해보세요. 경로가 잘못되면 `FileNotFoundException` 오류가 발생합니다. 예를 들어, 서버에서 파일을 제공하는 디렉터리를 지정할 때 절대 경로와 상대 경로 중 어떤 것을 사용했는지 확인해 보세요.

## 해결 방법 2: 파일 권한 설정

서버에서 실행되는 사용자가 파일에 접근할 수 있는 권한이 있는지 확인하세요. 권한이 없다면, 이 역시 `FileNotFoundException`을 일으킬 수 있습니다. 리눅스나 맥에서는 `chmod` 명령어를 사용해서 파일 권한을 변경할 수 있습니다.

## 해결 방법 3: REST API 구현 검토

서버에서 파일을 제공하는 REST API 코드가 올바른지 검토해 보세요. `@GetMapping` 또는 `@PostMapping` 어노테이션을 사용해 요청을 처리하는 메서드에서 `Resource` 또는 `ResponseEntity` 객체를 올바르게 반환하고 있는지 확인이 필요합니다.

```java
@GetMapping("/download")
public ResponseEntity<Resource> downloadFile() {
    // 파일 다운로드 로직
}
```

이런 식으로 구현할 수 있고, `Resource` 객체에 파일 정보를 담아 `ResponseEntity`를 통해 클라이언트에게 반환할 수 있습니다.

## 해결 방법 4: 로그 분석

마지막으로, 오류가 발생했을 때의 로그를 자세히 분석해 보세요. 로그에는 오류의 원인과 해결 방법에 대한 중요한 정보가 담겨 있을 수 있습니다.

## 결론

`FileNotFoundException` 오류는 주로 파일 경로의 문제, 파일 권한, REST API 구현의 문제, 또는 이러한 여러 가지 요인이 복합적으로 작용할 때 발생합니다. 따라서 이러한 각 요인을 차례로 검토하면 문제를 효과적으로 해결할 수 있습니다.