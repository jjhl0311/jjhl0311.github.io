---
title: Spring Boot Maven 플러그인 찾을 수 없음 문제 해결 방법
date: 2023-10-08 20:00:00 +0900
categories:
  - Spring
tags:
  - SpringBoot
  - Maven
---
## 문제 상황

Spring Boot 프로젝트를 Maven을 사용하여 빌드할 때, `plugin org.springframework.boot:spring-boot-maven-plugin not found` 이라는 오류가 발생할 수 있습니다. 이 오류는 Maven이 Spring Boot Maven 플러그인을 찾지 못할 때 나타납니다.

## 원인 파악

이 문제는 주로 다음과 같은 상황에서 발생합니다.

1. **인터넷 연결 문제**: Maven은 외부 저장소에서 플러그인을 다운로드 받는데, 인터넷 연결이 불안정하면 플러그인을 찾을 수 없습니다.
2. **설정 파일 오류**: `pom.xml` 파일에 플러그인 관련 설정이 잘못되어 있을 수 있습니다.
3. **로컬 저장소 문제**: Maven의 로컬 저장소에 문제가 있을 경우에도 이 오류가 발생할 수 있습니다.

## 해결 방법

### 인터넷 연결 확인

먼저 인터넷 연결이 안정적인지 확인해야 합니다. 불안정한 연결은 Maven 저장소에 접근하는 것을 방해할 수 있습니다.

### pom.xml 파일 검사

`pom.xml` 파일에서 Spring Boot Maven 플러그인 설정이 올바른지 확인하세요. 플러그인 섹션은 다음과 같이 설정되어야 합니다.

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

### Maven 로컬 저장소 재설정

Maven 로컬 저장소에 문제가 있다면, 이를 초기화 할 수 있습니다. 저장소는 보통 사용자 홈 디렉터리에 `.m2` 폴더 내에 있습니다. 이 폴더를 삭제한 후, `mvn clean install` 명령어를 실행하여 저장소를 재생성할 수 있습니다.

### Maven 명령어 실행

마지막으로, 명령 프롬프트 또는 터미널에서 다음과 같은 Maven 명령어를 실행합니다.

```
mvn clean install
```

이 명령어는 프로젝트를 깨끗이 하고 필요한 모든 의존성과 플러그인을 다운로드 받습니다.

## 정리

`plugin org.springframework.boot:spring-boot-maven-plugin not found` 오류는 여러 원인으로 발생할 수 있습니다. 인터넷 연결을 확인하고, `pom.xml` 설정을 점검한 후, Maven 로컬 저장소를 초기화하는 등의 단계를 거쳐 문제를 해결할 수 있습니다.