## 프로젝트 생성 (2023-11-12)

Project : Gradle  
Spring Boot : 2.7.17  
Language : Java  
Packaging : Jar  
Java : 11  
Dependencies : Spring Web, Thymeleaf

## 라이브러리
### 스프링부트 라이브러리
- spring-boot-starter-web
  - spring-boot-starter-tomcat : 톰캣(웹서버)
  - spring-webmvc : 스프링 웹 MVC
- spring-boot-starter-thymeleaf : 타임리프 템플릿 엔진 (view)
- spring-boot-starter(공통) : 스프링부트 + 스프링코어 + 로깅
  - spring-boot
    - spring-core
  - spring-boot-starter-logging
    - logback, slf4j

### 테스트 라이브러리
- spring-boot-starter-test
  - junit : 테스트 프레임워크
  - mockito : 목 라이브러리
  - assertj : 테스트 코드를 좀더 편하게 작성하게 도와주는 라이브러리
  - spring-test : 스프링 통합 테스트 지원