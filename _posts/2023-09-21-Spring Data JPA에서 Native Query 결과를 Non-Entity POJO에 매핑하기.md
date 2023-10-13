---
title: Spring Data JPA에서 Native Query 결과를 Non-Entity POJO에 매핑하기
date: 2023-09-21 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringDataJPA
  - NativeQuery
  - Non-EntityPOJO
---
## 문제 상황: Native Query와 Non-Entity POJO

Spring Data JPA는 자바 개발자가 데이터베이스와 통신할 수 있도록 도와주는 라이브러리입니다. 때로는 SQL 쿼리를 직접 작성해야 하는 경우도 있는데, 이러한 쿼리를 Native Query라고 합니다. 문제는 이러한 Native Query의 결과를 JPA Entity가 아닌 일반 Java 객체, 즉 Non-Entity POJO (Plain Old Java Object)에 어떻게 매핑할 수 있는지입니다.

## 해결 방법: `@SqlResultSetMapping`과 `@NamedNativeQuery` 사용

### @SqlResultSetMapping 이란?

`@SqlResultSetMapping`은 JPA에서 제공하는 어노테이션입니다. 이를 사용하면 SQL 쿼리 결과를 특정 Java 클래스에 매핑할 수 있습니다.

### @NamedNativeQuery 이란?

`@NamedNativeQuery` 역시 JPA 어노테이션 중 하나입니다. 이 어노테이션을 사용하면 SQL 쿼리를 이름있는 쿼리로 저장할 수 있어, 여러 번 재사용이 가능합니다.

### 예제 코드

다음은 `@SqlResultSetMapping`과 `@NamedNativeQuery`를 사용한 예제 코드입니다. 이 코드는 Native Query의 결과를 `MyNonEntityClass`라는 Non-Entity POJO에 매핑합니다.

```java
@SqlResultSetMapping(
    name = "MyMapping",
    classes = @ConstructorResult(
        targetClass = MyNonEntityClass.class,
        columns = {
            @ColumnResult(name = "column1", type = String.class),
            @ColumnResult(name = "column2", type = Integer.class)
        }
    )
)
@NamedNativeQuery(
    name = "MyQuery",
    query = "SELECT column1, column2 FROM MyTable",
    resultSetMapping = "MyMapping"
)
```

### EntityManager를 이용한 쿼리 실행

마지막으로 `EntityManager`를 사용하여 이름있는 쿼리를 실행합니다.

```java
List<MyNonEntityClass> results = entityManager
    .createNamedQuery("MyQuery", MyNonEntityClass.class)
    .getResultList();
```

## 주의사항: SQL과 객체의 컬럼 매칭

이 방법을 사용할 때는 SQL 쿼리의 컬럼 이름과 Java 클래스의 필드 이름이 일치해야 합니다. 불일치하면 `MappingException`이라는 에러가 발생합니다.

## 결론

Spring Data JPA와 Native Query를 활용하여 비-엔터티 클래스에 데이터를 매핑하는 방법은 복잡하지 않습니다. `@SqlResultSetMapping`과 `@NamedNativeQuery` 어노테이션을 적절히 활용하면 강력한 데이터 매핑이 가능합니다. 이 방법을 활용하면 복잡한 쿼리도 자유롭게 다룰 수 있어, 데이터베이스 작업이 훨씬 더 유연해집니다.