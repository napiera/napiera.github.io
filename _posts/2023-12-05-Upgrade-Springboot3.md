---
layout: post
title: "Upgrade Springboot 3.x"
date:   2023-12-05 11:30:44 +0900
categories: spring
---


기존 SpringBoot 2.6.6을 사용하고 있었습니다.
SpringBoot의 최신 버전인 3.x 로의 업그레이드를 위한 Guide를 개인적인 차원에서 정리해 두었습니다.


# 1. Java Upgrade (Over 17)

SpringBoot3에서는 Java 17이상을 지원합니다.

![java lts](https://private-user-images.githubusercontent.com/8067371/287926313-b3d1c8ed-2437-46a9-ba4b-43023da0bdcf.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTEiLCJleHAiOjE3MDE3NTg0MzEsIm5iZiI6MTcwMTc1ODEzMSwicGF0aCI6Ii84MDY3MzcxLzI4NzkyNjMxMy1iM2QxYzhlZC0yNDM3LTQ2YTktYmE0Yi00MzAyM2RhMGJkY2YucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMTIwNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzEyMDVUMDYzNTMxWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9NzMyMWVlZDBjZmZhNzNlN2EzNDgzZmE1YmZlNzMzZWJmOTQ2Njk4OGNiNDA5YTRmMDY0NjQ2MzlkNDY5OWQyNSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QmYWN0b3JfaWQ9MCZrZXlfaWQ9MCZyZXBvX2lkPTAifQ.X8B9_eqhbgQQk6FhCcbsag9UXMicRxbcB2Cez9HPS0Y)
*(Java 17 Version은 2021년 9월 새로 공개한 LTS(Long-Term Support) 버전으로, Oracle JDK 기준 2029년 9월까지 지원)*


그렇기 때문에, 기존 Java 16이하의 버전을 사용하고 있었다면, Java 17 이상으로 Upgrade 해 주어야 합니다.

```gradle
plugins {
  id "java"
  ...
}

java {
  sourceCompatibility = JavaVersion.VERSION_17
  targetCompatibility = JavaVersion.VERSION_17
}
```


# 2. 스프링 부트 2.7.X 업그레이드

![springboot2.7](https://private-user-images.githubusercontent.com/8067371/287928297-d6823b8e-f1c6-452c-b25b-fa519d14132f.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTEiLCJleHAiOjE3MDE3NTg0MzEsIm5iZiI6MTcwMTc1ODEzMSwicGF0aCI6Ii84MDY3MzcxLzI4NzkyODI5Ny1kNjgyM2I4ZS1mMWM2LTQ1MmMtYjI1Yi1mYTUxOWQxNDEzMmYucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQUlXTkpZQVg0Q1NWRUg1M0ElMkYyMDIzMTIwNSUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyMzEyMDVUMDYzNTMxWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9YjlmMzRhZTFmNzc5ZGQ4ODlmMTY0MmNmZTViNzBjYWQyNWQxZDY2NmE4NjZhN2RlYWY5YjFiNGQ3OTU3MTI3YSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QmYWN0b3JfaWQ9MCZrZXlfaWQ9MCZyZXBvX2lkPTAifQ.P981ATk_y7ZAhh7gfWqiMMMGHGFX7bHceu6BpHO2iH0)
SpringBoot3 버전으로 Upgrade 전에, 2.x 버전의 최신인 2.7.7으로 먼저 패치를 한 이후, Deprecated되어있는 함수들을 Migration 이후에 3.x 버전으로 Upgrade 하는 것이 좋습니다.

저는 현재 2.6.6 버전을 사용하고 있기 때문에, 다음과 같은 순서로 진행하였습니다.

* 2.6.6 -> 2.7.7 -> 3.1.6

Gradle 파일의 "org.springframework.boot" 버전을 변경하시면 됩니다.
```gradle
plugins {
  ...
  id "org.springframework.boot" version "2.7.7"
  ...
}
```
2.7.7 버전으로 올리고, 이슈들을 수정 후에, 3.1.6으로 올려서 다시 진행합니다.
```gradle
plugins {
  ...
  id "org.springframework.boot" version "3.1.6"
  id "io.spring.dependency-management" version "1.1.4"
  ...
}
```
(23.12.05 현재 SpringBoot의 최신 버전은 3.2.0 이지만, dependency-management 1.1.4와의 호환은 3.1.x 까지 지원하기 때문에 3.1.6으로 진행하였습니다)


# 3. javax에서 jakarta로 변경

SpringBoot3 에서는 javax를 jakarta로 변경해야 합니다. Java가 오라클 재단에서 이클립스 재던이로 이관되었기 때문엡니다. ([Java EE에서 Jakarta EE로의 전환](https://www.samsungsds.com/kr/insights/java_jakarta.html))

먼저 Gradle 파일을 수정합니다.
```gradle
plugins {
  ...
  //implementation "javax.servlet:javax.servlet-api"
  implementation "jakarta.servlet:jakarta.servlet-api"
  ...
}
```

코드에서도 javax로 시작하는 패키지 이름을 jakarta로 변경합니다.
* javax.persistence.* ➔ jakarta.persistence.*
* javax.validation.* ➔ jakarta.validation.*
* javax.servlet.* ➔ jakarta.servlet.*
* javax.annotation.* ➔ jakarta.annotation.*
* javax.transaction.* ➔ jakarta.transaction.*


# 4. Querydsl 설정 변경

javax.persistence 에서 jakarta.persistence 로 변경되면서 Querydsl 관련 설정도 변경이 필요하게 되었습니다.

먼저, Gradle의 설정을 아래와 같이 변경합니다.
```gradle
allprojects {
  group "com.skt.watchman"

  ext {
    ...
    //queryDslVersion = "5.0.0"
    queryDslVersion = "5.0.0:jakarta"
    ...
  }
}

...

  dependencies {
    //implementation "com.querydsl:querydsl-jpa:${queryDslVersion}"
    //implementation "com.querydsl:querydsl-apt:${queryDslVersion}"
    implementation "com.querydsl:querydsl-jpa:${queryDslVersion}"
    annotationProcessor "com.querydsl:querydsl-apt:${queryDslVersion}"
    annotationProcessor "jakarta.annotation:jakarta.annotation-api"
    annotationProcessor "jakarta.persistence:jakarta.persistence-api"
  }

  def querydslDir = "$buildDir/generated/querydsl"

  sourceSets {
    main.java.srcDirs += [ querydslDir ]
  }

  tasks.withType(JavaCompile) {
    options.annotationProcessorGeneratedSourcesDirectory = file(querydslDir)
  }

  clean.doLast {
    file(querydslDir).deleteDir()
  }
...
```

또한, JPA의 기본 namging 전략도 "SpringPhysicalNamingStrategy"을 사용하고 있다면, 수정해 주어야 합니다. ([JPA & Hibernate Naming Strategy](
https://velog.io/@ashappyasikonw/JPA-Hibernate-Naming-Strategy-CamelCase-SNAKECASE-%EB%8C%80%EB%AC%B8%EC%9E%90-%EB%A7%8C%EB%93%A4%EA%B8%B0))

```java
//properties.put("hibernate.physical_naming_strategy",
//  "org.springframework.boot.orm.jpa.hibernate.SpringPhysicalNamingStrategy");
properties.put("hibernate.physical_naming_strategy",
  "org.hibernate.boot.model.naming.CamelCaseToUnderscoresNamingStrategy");
```


# 5. Spring Security 변경

Spring Security 및 WebFluxSecurity를 기술하는 방법도 변경되었습니다. ([WebFlux Security](https://docs.spring.io/spring-security/reference/reactive/configuration/webflux.html))

예를 들어 httpBasic() 의 disable() 함수가 deprecated 되었습니다.
아래와 같이 함수 내부에서 값을 통해 설정해 주어야 합니다.

* httpBasic().disable() -> httpBasic(c -> c.disable())

또한 해당 설정은 Spring Security Configuration Class로 관리하여야 설정 적용됩니다. (@Configuration Annotaion을 붙여야 합니다) ([Spring Security 5 for Reactive Applications](https://www.baeldung.com/spring-security-5-reactive))


WebFluxSecurity 변경 전/후 코드입니다.

수정전
```java
@EnableWebFluxSecurity
public class WebSecurityConfig {

  @Bean
  public SecurityWebFilterChain springSecurityFilterChain(ServerHttpSecurity http) {
    return http
      .httpBasic().disable()
      .formLogin().disable()
      .csrf().disable()
      .logout().disable()
      .authorizeExchange()
        .matchers(EndpointRequest.to("health"))
          .permitAll()
        .anyExchange()
          .permitAll()
      .and()
      .exceptionHandling()
        .authenticationEntryPoint(new HttpStatusServerEntryPoint(HttpStatus.FORBIDDEN))
        .accessDeniedHandler(new HttpStatusServerAccessDeniedHandler(HttpStatus.FORBIDDEN))
      .and()
      .build();
    }

}
```

수정후
```java
@Configuration
@EnableWebFluxSecurity
public class WebSecurityConfig {

  @Bean
  public SecurityWebFilterChain springSecurityFilterChain(ServerHttpSecurity http) {
    return http
      .httpBasic(c -> c.disable())
      .formLogin(c -> c.disable())
      .csrf(c -> c.disable())
      .logout(c -> c.disable())
      .authorizeExchange((exchanges) -> {
        exchanges.matchers(EndpointRequest.to("health")).permitAll();
        exchanges.anyExchange().permitAll();
      })
      .exceptionHandling(c -> c
        .authenticationEntryPoint(new HttpStatusServerEntryPoint(HttpStatus.FORBIDDEN))  // UNAUTHORIZED
        .accessDeniedHandler(new HttpStatusServerAccessDeniedHandler(HttpStatus.FORBIDDEN))
      )
      .build();
    }
}
```


# 6. Redis Config 변경

redis 앞부분에 data가 추가하도록 config 값이 변경 되었습니다.
저는 yml 파일을 통해 config 설정을 하기 때문에, 아래와 같이 변경하였습니다.

```xml
#redis:
#  host: x.x.x.x
#  port: xx
#  password: xx

data:
  redis:
    host: x.x.x.x
    port: xx
    password: xx
```


# 7. MySQL Connector의 Gradle 설정 변경

Gradle에서 MySQL Connector 기술 방법도 변경되었습니다.
아래와 같이 수정합니다.

```gradle
plugins {
  ...
  //runtimeOnly "mysql:mysql-connector-java"
  runtimeOnly "com.mysql:mysql-connector-j"
  ...
}
```


# 8. Base64Utils에서 Base64로 변경

SpringFramework의 Base64Utils도 deprecated되었습니다.
java.util의 Base64로 변경합니다.

* import org.springframework.util.Base64Utils; -> import java.util.Base64;
* Base64Utils.decode() -> Base64.getDecoder().decode()


# Ref
* [Preparing for Spring Boot 3.0](https://spring.io/blog/2022/05/24/preparing-for-spring-boot-3-0)
* [공식 Guide](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.0-Migration-Guide)
* [SpringBoot 2 와 3](https://velog.io/@ililil9482/Spring-3.x-Security-%EC%84%A4%EC%A0%95)
* [스프링 부트 2에서 스프링 부트 3로 업그레이드 가이드](https://covenant.tistory.com/279)