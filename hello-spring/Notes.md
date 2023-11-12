## View 환경설정

- resources/static/index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
<title>Hello</title>
</head>
<body>
Hello
<a href="/hello">hello</a>
</body>
</html>
```
- 스프링 부트가 제공하는 Welcome Page 기능
- 'static/index.html'을 올려두면 Welcome page 기능을 제공한다.
- https://docs.spring.io/spring-boot/docs/2.7.17/reference/html/web.html#web.servlet.spring-mvc.static-content

### thymeleaf 템플릿 엔진
- thymeleaf 공식 사이트 : https://www.thymeleaf.org/
- 스프링 공식 튜토리얼 : https://spring.io/guides/gs/serving-web-content/
- 스프링부트 메뉴얼 : https://docs.spring.io/spring-boot/docs/2.7.17/reference/html/


### viewResolver
- 컨트롤러에서 리턴 값으로 문자를 반환하면 뷰 리졸버 (`viewResolver`)가 화면을 찾아서 처리함.
- 스프링 부트 템플릿엔진 기본  viewName 매핑
- `resources:template/` + {ViewName} + `.html`

> 참고 : `spring-boot-devtools` 라이브러리를 추가하면, `.html`파일을 컴파일만 해주면 서버 재시작 없이 View 파일 변경이 가능하다.
> 인텔리제이 컴파일 방법 : build -> Recompile

## 빌드하고 실행하는 방법
1. cmd로 이동
2. `./gradlew build`
3. `cd build/libs`
4. `java -jar hello-spring-0.0.1-SNAPSHOT.jar`
5. 실행확인

### 빌드 지우는 방법
1. `./gradlew clean`
2. `./gradlew clean build`

* 1번이 잘 안되면 2번으로 실행


## 스프링 웹 개발 기초

- 정적 컨텐츠
- MVC & 템플릿 엔진
- API

### 정적 컨텐츠
- 스프링 부트 정적 컨텐츠 기능

### MVC & 템플릿 엔진
- MVC : Model, View, Controller

```java
@Controller
public class HelloController {

@GetMapping("hello-mvc")
public String helloMvc(@RequestParam("name") String name, Model model) {
model.addAttribute("name", name);
return "hello-template";
}
}
```

### API

```java
@Controller
public class HelloController {

@GetMapping("hello-string")
@ResponseBody
public String helloString(@RequestParam("name") String name) {
return "hello " + name;
}
}
```
- `ResponseBody`를 사용하고, 객체를 반환하면 객체가 JSON으로 변환됨.

#### ResponseBody 사용원리
- HTTP의 BODY에 문자 내용을 직전 반환
- `viewResolver`대신에 `HttpMessageConverter`가 동작
- 기본 문자처리 : `StringHttpMessageConverter`
- 기본 객체처리 : `MappingJackson2HttpMessageConverter`
- byte 처리 등등 기타 여러 HttpMessageConverter가 기본으로 등록되어 있음
> 참고 : 클라이언트의 HTTP Accept 헤더와 서버의 컨트롤러 반환 타입 정보 둘을 조합해서 `HttpMessageConverter`가 선택된다.

