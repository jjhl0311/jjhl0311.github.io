---
title: Spring Data JPA에서 setMaxResults 사용하기
date: 2023-08-26 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringData
  - JPA
  - setMaxResults
---
## setMaxResults의 기능과 필요성

`setMaxResults`는 JPA(Java Persistence API)에서 제공하는 메서드로, 쿼리 결과의 최대 행 수를 설정합니다. 예를 들어, 데이터베이스에서 100개의 레코드가 있을 때, `setMaxResults(10)`을 설정하면 쿼리 결과는 최대 10개의 레코드만을 반환합니다. 이러한 기능은 페이지네이션을 구현할 때나 데이터를 부분적으로 로딩할 때 유용합니다.

## Spring Data JPA에서의 사용법

Spring Data JPA에서는 `Pageable` 인터페이스를 사용하여 이러한 제한을 설정할 수 있습니다. `Pageable`은 페이지 크기(`pageSize`)와 현재 페이지 번호(`pageNumber`)를 인자로 받아서, 내부적으로 `setMaxResults`를 적용합니다.

```java
public interface UserRepository extends JpaRepository<User, Long> {
    Page<User> findAll(Pageable pageable);
}
```

위 코드에서 `Pageable` 객체를 파라미터로 전달하면, Spring Data JPA가 알아서 `setMaxResults`와 같은 제한을 적용하여 결과를 반환합니다.

```java
Pageable pageable = PageRequest.of(0, 10); // 첫 페이지에 10개의 결과를 가져옴
Page<User> users = userRepository.findAll(pageable);
```

## 주의사항

Spring Data JPA의 `Pageable`을 사용할 때, 반환되는 `Page` 객체는 자동으로 쿼리 결과의 전체 개수도 계산합니다. 이는 성능에 영향을 줄 수 있으니, 실제 서비스에서는 이 부분을 고려해야 합니다.

## setMaxResults와 Pageable의 차이점

`setMaxResults`는 단순히 쿼리 결과의 최대 행 수를 제한하는 반면, `Pageable`은 더 많은 정보를 제공합니다. 예를 들어, 전체 페이지 수, 현재 페이지의 레코드 수, 이전 페이지나 다음 페이지로 넘어갈 수 있는지 등의 정보를 함께 제공합니다. 따라서 `Pageable`은 복잡한 페이지네이션 로직을 간편하게 처리할 수 있습니다.

## 결론

Spring Data JPA에서는 `Pageable`을 사용하여 쿼리 결과를 제한할 수 있습니다. 이는 내부적으로 `setMaxResults`를 사용하여 구현되며, 페이지네이션 등의 복잡한 로직을 간편하게 처리할 수 있습니다. 하지만 성능 이슈에 주의해야 하며, 필요에 따라 직접 `setMaxResults`를 사용할 수도 있습니다.