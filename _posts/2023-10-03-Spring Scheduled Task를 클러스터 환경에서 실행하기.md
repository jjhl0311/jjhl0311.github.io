---
title: Spring Scheduled Task를 클러스터 환경에서 실행하기
date: 2023-10-03 20:00:00 +0900
categories:
  - Spring
tags:
  - Spring
  - ScheduledTask
---
## 문제 상황 및 배경

스프링 프레임워크에서는 `@Scheduled` 어노테이션을 이용하여 정기적인 작업을 수행할 수 있습니다. 하지만, 이 기능을 클러스터 환경에서 사용하면 문제가 발생할 수 있습니다. 클러스터란, 여러 대의 서버가 하나의 서비스를 제공하는 구조를 의미합니다. 이런 환경에서 `@Scheduled`를 그대로 사용하면, 각 서버에서 동일한 작업이 동시에 발생할 위험이 있습니다.

## `@Scheduled`의 한계점

`@Scheduled` 어노테이션은 단순하고 빠르게 스케줄링을 설정할 수 있어 많이 사용되지만, 클러스터 환경에서는 적합하지 않습니다. 각 서버가 독립적으로 작업을 스케줄링하기 때문에 데이터 중복 처리나 리소스 낭비가 발생할 수 있습니다.

## 대안 솔루션: 분산 스케줄링

### Quartz 스케줄러

Quartz 스케줄러는 클러스터 환경에서도 안정적으로 작동합니다. 데이터베이스를 이용하여 스케줄링 정보를 공유하므로, 여러 서버가 동일한 작업을 중복으로 실행하는 문제를 해결할 수 있습니다.

### Spring Cloud Task

Spring Cloud Task는 마이크로서비스 아키텍처를 위한 스프링 프로젝트 중 하나입니다. 이를 이용하면 각 작업에 대한 메타데이터를 데이터베이스에 저장할 수 있으며, 이 정보를 이용하여 클러스터 내에서 작업을 조율할 수 있습니다.

## 코드 수정 예시

원래 코드에서 `@Scheduled`를 사용하던 부분을 Quartz 스케줄러로 대체하는 경우 아래와 같이 수정할 수 있습니다.

```java
// Spring의 @Scheduled
// @Scheduled(fixedRate = 5000)
// public void doSomething() {
//     // 작업 코드
// }

// Quartz를 이용한 예
public class MyJob implements Job {
    public void execute(JobExecutionContext context) throws JobExecutionException {
        // 작업 코드
    }
}
```

## 결론

클러스터 환경에서 스케줄링 작업을 안정적으로 실행하기 위해서는 `@Scheduled` 어노테이션 대신 Quartz 스케줄러나 Spring Cloud Task 같은 분산 스케줄링 방법을 사용하는 것이 좋습니다. 이러한 방법들은 클러스터 내의 여러 서버 간에 작업을 적절히 분배하여 리소스를 효율적으로 활용할 수 있습니다.