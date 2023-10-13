---
title: RESTTemplate을 이용한 POST 요청(JSON)
date: 2023-10-01 20:00:00 +0900
categories:
  - Spring
tags:
  - RESTTemplate
  - MultipartPOST
---
## 오류 요약
`HttpClientErrorException` - 400 Bad Request

## 오류 해결 방법
이 문제는 일반적으로 POST 요청을 보낼 때 요청 본문(body)에 JSON 데이터가 올바르게 설정되지 않아 발생합니다. 해결 방법은 다음과 같습니다.

### HttpHeaders 설정하기
먼저 `HttpHeaders` 객체를 생성하여 `Content-Type`을 `application/json`으로 설정합니다.

```java
HttpHeaders headers = new HttpHeaders();
headers.setContentType(MediaType.APPLICATION_JSON);
```

### HttpEntity 설정하기
그 다음으로 `HttpEntity` 객체를 생성합니다. 이 객체는 `HttpHeaders`와 JSON 데이터를 함께 보낼 때 사용됩니다.

```java
HttpEntity<String> entity = new HttpEntity<>(jsonString, headers);
```

여기서 `jsonString`은 전송하려는 JSON 형식의 문자열입니다.

### RESTTemplate 사용하기
마지막으로 `RestTemplate`을 사용하여 POST 요청을 보냅니다.

```java
RestTemplate restTemplate = new RestTemplate();
ResponseEntity<String> response = restTemplate.exchange(url, HttpMethod.POST, entity, String.class);
```

## 추가 팁
- `HttpHeaders`와 `HttpEntity`는 Spring Framework에서 제공하는 클래스입니다. 이들을 이용하면 HTTP 헤더와 본문을 쉽게 설정할 수 있습니다.
- `MediaType.APPLICATION_JSON`은 `application/json` MIME 타입을 나타냅니다. MIME 타입은 데이터 형식을 명시하기 위해 사용됩니다.
- `RestTemplate` 클래스는 Spring에서 제공하는 강력한 HTTP 클라이언트 라이브러리입니다. 이를 통해 다양한 HTTP 메서드를 쉽게 사용할 수 있습니다.
  
이 정보를 바탕으로 문제를 해결해 보세요.