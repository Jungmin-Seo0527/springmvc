# TIL

## 도움말

[Inflearn_SpringMVC](https://github.com/Jungmin-Seo0527/Inflearn_SpringMVC) 에 이어서 강의 6장에 해당하는 내용 정리

## 6. 스프링 MVC - 기본 기능

### 6-1. 프로젝트 생성

#### build.gradle

```
plugins {
	id 'org.springframework.boot' version '2.5.0'
	id 'io.spring.dependency-management' version '1.0.11.RELEASE'
	id 'java'
}

group = 'hello'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = '11'

configurations {
	compileOnly {
		extendsFrom annotationProcessor
	}
}

repositories {
	mavenCentral()
}

dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
	implementation 'org.springframework.boot:spring-boot-starter-web'
	compileOnly 'org.projectlombok:lombok'
	annotationProcessor 'org.projectlombok:lombok'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
}

test {
	useJUnitPlatform()
}

```

* 프로젝트 선택
    * Project: Gradle Project
    * Language: Java
    * Spring Boot: 2.5.0

* ProjectMetaData
    * Group: hello
    * Artifact: springmvc
    * Name: springmvc
    * Package name: hello.springmvc
    * Packaging: **Jar(주의!)**
    * Java: 11

* Dependencies: **Spring Web, Thymeleaf, Lombok**

> **주의!**   
> Packaging는 War가 아니라 **Jar를 선택**해야한다. JSP를 사용하지 않기 때문에 Jar를 사용하는 것이 좋다. 앞으로 스프링 부트를 사용하면 이 방식을 주로 사용하게 될것이다.   
> Jar를 사용하면 항상 내장 서버(톰캣등)을 사용하고 `webapp`경로도 사용하지 않는다. 내장 서버 사용에 최적화 되어 있는 기능이다. 최근에는 주로 이 방식을 사용한다.   
> War를 사용하면 내장 서버도 사용가능 하지만, 주로 외부 서버에 배포하는 목적으로 사용한다.

#### index.html - Welcome 페이지

* `src/main/resources/static/index.html`
* 스프링 부터에 `Jar`를 사용하면 `/resources/static/index.html`위치에 `index.html`파일을 두면 Welcome 페이지로 처리해준다.(스프링 부트가 지원하는 정적 컨텐츠
  위치에 `/index.html`이 있으면 된다.)

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<ul>
    <li>로그 출력
        <ul>
            <li><a href="/log-test">로그 테스트</a></li>
        </ul>
    </li>
    <!-- -->
    <li>요청 매핑
        <ul>
            <li><a href="/hello-basic">hello-basic</a></li>
            <li><a href="/mapping-get-v1">HTTP 메서드 매핑</a></li>
            <li><a href="/mapping-get-v2">HTTP 메서드 매핑 축약</a></li>
            <li><a href="/mapping/userA">경로 변수</a></li>
            <li><a href="/mapping/users/userA/orders/100">경로 변수 다중</a></li>
            <li><a href="/mapping-param?mode=debug">특정 파라미터 조건 매핑</a></li>
            <li><a href="/mapping-header">특정 헤더 조건 매핑(POST MAN 필요)</a></
            li>
            <li><a href="/mapping-consume">미디어 타입 조건 매핑 Content-Type(POST
                MAN 필요)</a></li>
            <li><a href="/mapping-produce">미디어 타입 조건 매핑 Accept(POST MAN
                필요)</a></li>
        </ul>
    </li>
    <li>요청 매핑 - API 예시
        <ul>
            <li>POST MAN 필요</li>
        </ul>
    </li>
    <li>HTTP 요청 기본
        <ul>
            <li><a href="/headers">기본, 헤더 조회</a></li>
        </ul>
    </li>
    <li>HTTP 요청 파라미터
        <ul>
            <li><a href="/request-param-v1?username=hello&age=20">요청 파라미터
                v1</a></li>
            <li><a href="/request-param-v2?username=hello&age=20">요청 파라미터v2</a></li>
            <li><a href="/request-param-v3?username=hello&age=20">요청 파라미터
                v3</a></li>
            <li><a href="/request-param-v4?username=hello&age=20">요청 파라미터
                v4</a></li>
            <li><a href="/request-param-required?username=hello&age=20">요청
                파라미터 필수</a></li>
            <li><a href="/request-param-default?username=hello&age=20">요청
                파라미터 기본 값</a></li>
            <li><a href="/request-param-map?username=hello&age=20">요청 파라미터
                MAP</a></li>
            <li><a href="/model-attribute-v1?username=hello&age=20">요청 파라미터
                @ModelAttribute v1</a></li>
            <li><a href="/model-attribute-v2?username=hello&age=20">요청 파라미터
                @ModelAttribute v2</a></li>
        </ul>
    </li>
    <li>HTTP 요청 메시지
        <ul>
            <li>POST MAN</li>
        </ul>
    </li>
    <li>HTTP 응답 - 정적 리소스, 뷰 템플릿
        <ul>
            <li><a href="/basic/hello-form.html">정적 리소스</a></li>
            <li><a href="/response-view-v1">뷰 템플릿 v1</a></li>
            <li><a href="/response-view-v2">뷰 템플릿 v2</a></li>
        </ul>
    </li>
    <li>HTTP 응답 - HTTP API, 메시지 바디에 직접 입력
        <ul>
            <li><a href="/response-body-string-v1">HTTP API String v1</a></li>
            <li><a href="/response-body-string-v2">HTTP API String v2</a></li>
            <li><a href="/response-body-string-v3">HTTP API String v3</a></li>
            <li><a href="/response-body-json-v1">HTTP API Json v1</a></li>
            <li><a href="/response-body-json-v2">HTTP API Json v2</a></li>
        </ul>
    </li>
</ul>
</body>
</html>
```

### 6-2. 로깅 간단히 알아보기

운영 시스템에서는 `System.out.println()`같은 시스템 콘솔을 사용해서 필요한 정보를 출력하지 않고, 별도의 로깅 라이브러리를 사용해서 로그를 출력한다.   
참고로 로그 관련 라이브러리도 많고, 싶게 들어가면 끝이 없기 때문에, 여기서는 최소한의 사용 방법만 알아본다.

#### 로깅 라이브러리

스프링 부트 라이브러리를 사용하면 스프링 부트 로깅 라이브러리(`spring-boot-starter-logging`)가 함께 포함된다.   
스프링 부트 로깅 라이브러리는 기본으로 다음 로깅 라이브러리를 사용한다.

* SLF4J - http://www.slf4j.org
* Logback - http://logback.qos.ch

로그 라이브러리는 Logback, Log4J, Log4J2 등등 수 많은 라이브러리가 있는데, 그것을 통합해서 인터페이스로 제공하는 것이 바로 SLF4J 라이브러리다.

#### 로그 선언

* `private Logger log = LoggerFactory.getLogger(getClass());`
* `private static final Logger log = LoggetFavtory.getLogget(Xxx.class)`
* `@Slf4j`: 롬복 사용 가능

#### 로그 호출

* `log.info("hello")`
* `System.out.println("hello)`
  시스템 콘솔로 직접 출력하는 것 보다 로그를 사용하면 다음과 같은 장점이 있다. 실무에서는 항상 로그를 사용해야 한다.

#### LogTestController

* `src/main/java/hello/springmvc/basic/LogTestController.java`

```java
package hello.springmvc.basic;

import lombok.extern.slf4j.Slf4j;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

// @Slf4j
@RestController
public class LogTestController {

    private final Logger log = LoggerFactory.getLogger(getClass());

    @RequestMapping("/log-test")
    public String logTest() {
        String name = "Spring";

        System.out.println("name = " + name);

        log.trace("trace log={}", name);
        log.debug("debug log={}", name);
        log.info("info log={}", name);
        log.warn("warn log={}", name);
        log.error("error log={}", name);

        log.debug("String concat log=" + name);

        return "ok";
    }
}

```

* `@RequestController`
    * `@Controller`는 반환 값이 `String`이면 뷰 이름으로 인식된다. 그래서 **뷰를 찾고 뷰가 랜더링 된다.**
    * `@RestController`는 반환 값으로 뷰를 찾는 것이 아니라, **HTTP 메시지 바디에 바로 입력**한다. 따라서 실행 결과로 ok 메세지를 받을 수 있다. `@ResponseBody`와 관련이
      있는데, 뒤에서 더 자세히 설명한다.

#### 테스트

* 로그가 출력되는 포멧 확인
    * 시간, 로그 레벨, 프로세스 ID, 쓰레드 명, 클래스명, 로그 메시지
* 로그 레벨 설정을 변경해서 출력 결과를 보자.
    * LEVEL: `TRACE > DEBUG > INFO > WARN > ERROR`
    * 개발 서버는 debug 출력
    * 운영 서버는 info 출력
* `@Slf4j`로 변경

#### 로그 레벨 설정

* `application.properties`

```
# 전체 로그 레벨 설정(기본 info)
logging.level.root=info
# hello.springmvc 패키지와 그 하위 로그 레벨 설정
logging.level.hello.springmvc=debug

```

#### 올바른 로그 사용법

* `log.debug("data="+data)`
    * 로그 출력 레벨을 info로 설정해도 해당 코드에 있는 "data="+data 가 실행이 되어 버린다. 결과적으로 문자 더하기 연산이 발생한다.
* `log.debug("data={}", data)`
    * 로그 출력 레벨을 info로 설정하면 아무일도 발생하지 않는다. 따라서 앞과 같은 의미없는 연산이 발생하지 않는다.

#### 로그 사용시 장점

* 쓰레드 정보, 클래스 이름 같은 부가 정보를 함께 볼 수 있고, 출력 모양을 조정할 수 있다.
* 로그 레벨에 따라 개발 서버에서는 모든 로그를 출력하고, 운영서버에서는 출력하지 않는 등 로그를 상황에 맞게 조절할 수 있다.
* 시스템 아웃 콘솔에만 출력하는 것이 아니라, 파일이나 네트워크 등, 로그를 별도의 위치에 남길 수 있다. 특히 파일로 남길 때는 일별, 특정 용량에 따라 로그를 분할하는 것도 가능하다.
* 성능도 일반 System.out보다 좋다.(내부 버퍼링, 멀티 쓰레드 등등) 그래서 실무에서는 꼭 로그를 사용해야 한다.


* 스프링 부트가 제공하는 로그 기능 참고
    * https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#boot-features-logging

### 6-3. 요청 매핑

#### MappingController

* `src/main/java/hello/springmvc/basic/requestmapping/MappingController.java`

```java
package hello.springmvc.basic.requestmapping;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.web.bind.annotation.*;

@RestController
public class MappingController {
    private Logger log = LoggerFactory.getLogger(getClass());

    /**
     * 기본 요청
     * 둘다 허용 /hello-basic, /hello-basic/
     * HTTP 메서드 모두 허용 GET, HEAD, POST, PUT, PATCH, DELETE
     */
    @RequestMapping("/hello-basic")
    public String helloBasic() {
        log.info("helloBasic");
        return "ok";
    }
}
```

* `@RestController` **매핑 정보(한번 더)**
    * `@Controller`는 반환 값이 `String`이면 뷰 이름으로 인식된다. 그래서 **뷰를 찾고 뷰가 랜더링 된다.**
    * `@RestController`는 반환 값으로 뷰를 찾는 것이 아니라, **HTTP 메시지 바디에 바로 입력**한다. 따라서 실행 결과로 ok 메시지를 받을 수 있다. `@ResponseBody`와 관련이
      있는데, 뒤에서 더 자세히 설명한다.

* `@RequestMapping("/hello-basic)`
    * `/hello-basic`URL 호출이 오면 이 메서드가 실행되도록 매핑한다.
    * 대부분의 속성을 `배열[]`로 제공하므로 다중 설정이 가능하다.`{"/hello-basic", "/hello-go"}`

##### 둘다 허용

다음 두가지 요청은 다른 URL이지만, 스프링은 다음 URL 요청들을 같은 요청으로 매핑한다.

* 매핑: `/hello-basic`
* URL 요청: `/hello-basic`, `/hello-basic/`

##### HTTP 메서드

`@RequestMapping`에 `method`속성으로 HTTP 메서드를 지정하지 않으면 HTTP 메서드와 무관하게 호출된다.   
모두 허용 GET, HEAD, POST, PUT, PATCH, DELETE

#### HTTP 메서드 매핑

```java

@RestController
public class MappingController {
    /**
     * method 특정 HTTP 메서드 요청만 허용
     * GET, HEAD, POST, PUT, PATCH, DELETE
     */
    @RequestMapping(value = "/mapping-get-v1", method = RequestMethod.GET)
    public String mappingGetV1() {
        log.info("mappingGetV1");
        return "ok";
    }
}
```

만약 여기서 POST 요청을 하면 스프링 MVC는 HTTP 405 상태코드(Method Not Allowed)를 반환한다.

#### HTTP 메서드 매핑 축약

```java

@RestController
public class MappingController {
    /**
     * 편리한 축약 애노테이션 (코드 보기)
     *
     * @GetMapping
     * @PostMapping
     * @PutMapping
     * @DeleteMapping
     * @PatchMapping
     */
    @GetMapping(value = "/mapping-get-v2")
    public String mappingGetV2() {
        log.info("mapping-get-v2");
        return "ok";
    }
}
```

HTTP 메서드를 축약한 애노테이션을 사용하는 것이 더 직관적이다. 코드를 보면 내부에서 `@RestMapping`과 `method`를 지정해서 사용하는 것을 확인할 수 있다.

#### PathVariable(경로 변수)사용

```java
public class MappingController {
    /**
     * PathVariable 사용
     * 변수명이 같으면 생략 가능
     *
     * @PathVariable("userId") String userId -> @PathVariable userId
     */
    @GetMapping("/mapping/{userId}")
    public String mappingPath(@PathVariable("userId") String data) {
        log.info("mappingPath userId={}", data);
        return "ok";
    }
}
```

최근 HTTP API는 다음과 같이 리소스 경로에 식별자를 넣는 스타일을 선호한다.

* `/mapping/userA`
* `/users/1`
* `@RequestMapping`은 URL 경로를 템플릿화 할 수 있는데, `@PathVariable`을 사용하면 매칭 되는 부분을 편리하게 조회할 수 있다.
* `@PathVariable`의 이름과 파라미터 이름이 같으면 생략할 수 있다.

#### PathVariable사용 - 다중

```java
public class MappingController {
    /**
     * PathVariable 사용 다중
     */
    @GetMapping("/mapping/users/{userId}/orders/{orderId}")
    public String mappingPath(@PathVariable String userId, @PathVariable Long orderId) {
        log.info("mappingPath userId={}, orderId={}", userId, orderId);
        return "ok";
    }
}
```

#### 특정 파라미터 조건 매핑

```java
public class MappingController {
    /**
     * 파라미터로 추가 매핑
     * params="mode",
     * params="!mode"
     * prams="mode=debug"
     * params="mode!=debug"
     * params={"mode=debug", "data=good"}
     */
    @GetMapping(value = "/mapping-param", params = "mode=debug")
    public String mappingParam() {
        log.info("mappingParam");
        return "ok";
    }
}
```

특정 파라미터가 있거나 없는 조건을 추가할 수 있다. 잘 사용하지는 않는다.

#### 특정 헤더 조건 매핑

```java
public class MappingController {
    /**
     * 특정 헤더로 추가 매핑
     * headers="mode",
     * headers="!mode"
     * headers="mode=debug"
     * headers="mode!=debug"
     */
    @GetMapping(value = "/mapping-header", headers = "mode=debug")
    public String mappingHeader() {
        log.info("mappingHeader");
        return "ok";
    }
}
```

파라미터 매핑과 비슷하지만, HTTP 헤더를 사용한다.

#### 미디어 타입 조건 매핑 - HTTP 요청 Content-Type, consume

```java
public class MappingController {
    /**
     * Content-Type 헤더 기반 추가 매핑 Media Type
     * consumes="application/json"
     * consumes="!application/json"
     * consumes="application/*"
     * consumes="*\/*"
     * MediaType.APPLICATION_JSON_VALUE
     */
    @PostMapping(value = "/mapping-consume", consumes = MediaType.APPLICATION_JSON_VALUE)
    public String mappingConsumes() {
        log.info("mappingConsumes");
        return "ok";
    }
}
```

HTTP 요청의 Content-Type 헤더를 기반으로 미디어 타입으로 매핑한다.   
만약 맞지 않으면 HTTP 415 상태코드(Unsupported Media Type)을 반환한다.

* 예시) consumes

```
consumes = "text/plain"
consumes = {"text/plain", "application/*"}
consumes = MediaType.TEXT_PLAIN_VALUE
```

#### 미디어 타입 조건 매핑 - HTTP 요청 Accept, produce

```java
public class MappingController {
    /**
     * Accept 헤더 기반 Media Type
     * produces = "text/html"
     * produces = "!text/html"
     * produces = "text/*"
     * produces = *\/*"
     */
    @PostMapping(value = "/mapping-produce", produces = MediaType.TEXT_HTML_VALUE)
    public String mappingProduces() {
        log.info("mappingProduces");
        return "ok";
    }
}
```

HTTP 요청의 Accept 헤더를 기반으로 미디어 타입으로 매핑한다.   
만약 맞지 않으면 HTTP 406 상태코드(Not Acceptable)을 반환한다.

* 예시

```
produces = "text/plain"
produces = {"text/plain", "application/*"}
produces = MediaType.TEXT_PLAIN_VALUE
produces = "text/palin;charset=UTF-8"
```

### 6-4. 요청 매핑 - API 예시

실제 데이터가 넘아가는 부분은 생략하고 URL 매핑만

#### 회원 관리 API

* 회원 목록 조회: GET `/user`
* 회원 등록: POST `/users`
* 회원 조회: GET `/users/{userId}`
* 회원 수정: PATCH `/users/{userId}`
* 회원 삭제: DELETE `/users/{userId}`

#### MappingClassController

```java
package hello.springmvc.basic.requestmapping;

import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/mapping/users")
public class MappingClassController {
    /**
     * GET /mapping/users
     */
    @GetMapping
    public String users() {
        return "get users";
    }

    /**
     * POST /mapping/users
     */
    @PostMapping
    public String addUser() {
        return "post user";
    }

    /**
     * GET /mapping/users/{userId}
     */
    @GetMapping("/{userId}")
    public String findUser(@PathVariable String userId) {
        return "get userId=" + userId;
    }

    /**
     * PATCH /mapping/users/{userId}
     */
    @PatchMapping("/{userId}")
    public String updateUser(@PathVariable String userId) {
        return "update userId=" + userId;
    }

    /**
     * DELETE /mapping/users/{userId}
     */
    @DeleteMapping("/{userId}")
    public String deleteUser(@PathVariable String userId) {
        return "delete userId=" + userId;
    }
}
```

* `/mapping`: 강의의 다른 예제들과 구분하기 위해 사용
* `@RequestMapping("/mapping/users")`
    * 클래스 레벨에 매핑 정보를 두면 메서드 레벨에서 해당 정보를 조합해서 사용한다.

* Postman으로 테스트
    * 회원 목록 조회: GET `/mapping/users`
    * 회원 등록: POST `/mapping/users`
    * 회원 조회: GET `/mapping/users/id1`
    * 회원 수정: PATCH `/mapping/users/id1`
    * 회원 삭제: DELETE `/mapping/users/id1`

### 6-5. HTTP 요청 - 기본, 헤더 조회

애노테이션 기반의 스프링 컨트롤러는 다양한 파라미터를 지원한다.

#### RequestHeaderController

* `src/main/java/hello/springmvc/basic/request/RequestHeaderController.java`

```java
package hello.springmvc.basic.request;

import lombok.extern.slf4j.Slf4j;
import org.springframework.http.HttpMethod;
import org.springframework.util.MultiValueMap;
import org.springframework.web.bind.annotation.CookieValue;
import org.springframework.web.bind.annotation.RequestHeader;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.util.Locale;

@Slf4j
@RestController
public class RequestHeaderController {

    @RequestMapping("/headers")
    public String headers(HttpServletRequest request,
                          HttpServletResponse response,
                          HttpMethod httpMethod,
                          Locale locale,
                          @RequestHeader MultiValueMap<String, String> headerMap,
                          @RequestHeader("host") String host,
                          @CookieValue(value = "myCookie", required = false) String cookie) {
        log.info("request={}", request);
        log.info("response={}", response);
        log.info("httpMethod={}", httpMethod);
        log.info("locale={}", locale);
        log.info("headerMap={}", headerMap);
        log.info("host={}", host);
        log.info("cookie={}", cookie);

        return "ok";
    }
}

```

* `HttpServletRequest`
* `HttpServletResponse`
* `HttpMethod`
    * HTTP 메서드를 조회한다. `org.springframework.http.HttpMethod`

* `Locale`
    * Locale 정보를 조회한다. (언어)

* `@RequestHeader MultiValueMap<String, String> headerMap`
    * 모든 HTTP 헤더를 MultiValueMap 형식으로 조회한다.

* `@RequestHeader("host") String host`
    * 특정 HTTP 헤더를 조회한다.
    * 속성
        * 필수 값 여부: `required`
        * 기본 값 속성: `defaultValue`

* `@CookieValue(value = "myCookie", required = false) String cookie`
    * 특정 쿠키를 조회한다.
    * 속성
        * 필수 값 여부: `required`
        * 기본 값: `defaultValue`

* `MutiValueMap`
    * Map과 유사한데, 하나의 키에 여러 값을 받을 수 있다.
    * HTTP header, HTTP 쿼리 파라미터와 같이 하나의 키에 여러 값을 받을 때 사용한다.
        * **keyA=value1&keyA=value2**
    ```
    MultiValueMap<String, String> map = new LinkedMultiValueMap();
    map.add("keyA", "value1");
    map.add("keyA", "value2");
    
    // [value1, value2]
    List<String> values = map.get("keyA");
    ```
* `@Slf4j`
    * 다음 코드를 자동으로 생성해서 로그를 선언해준다. 개발자는 편리하게 `log`라고 사용하면 된다.
    ```
    private static final org.slf4j.Logger log = 
        org.slf4j.LoggerFactory.getLogget(RequestHeaderController.class);
    ```

> 참고    
> `@Controller`의 사용 가능한 파라미터 목록은 다음 공식 메뉴얼에서 확인할 수 있다.    
> https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-ann-arguments

> 참고    
> `@Controller`의 사용 가능한 응답 값 목록은 다음 공식 메뉴얼에서 확인할 수 있다.    
> https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-ann-return-types

### 6-6. HTTP 요청 파라미터 - 쿼리 파라미터, HTML Form

#### HTTP 요청 데이터 조회 - 개요

서블릿에서 학습했던 HTTP 요청 데이터를 조회 하는 방법을 다시 떠올려보자. 그리고 서블릿으로 학습했던 내용을 스프링이 얼마나 깔끔하고 효율적으로 바꾸어주는지 알아보자.

HTTP 요청 메시지를 통해 클라리언트에서 서버로 데이터를 전달하는 방법을 알아보자.

**클라이언트에서 서버로 요청 데이터를 전달할 때는 주로 다음 3가지 방법을 사용한다.**

* GET - 쿼리 파라미터
    * /url?username=hello%age=20
    * 메시지 바디 없이, URL의 쿼리 파라미터에 데이터를 포함해서 전달
    * 예) 검색, 필터, 페이징등에서 많이 사용하는 방식

* POST - HTML Form
    * content-Type: application/x-www-form-urlencoded
    * 메시지 바디에 쿼리 파라미터 형식으로 전달 username=hello&age=20
    * 예) 회원 가입, 상품 주문, HTML Form 사용

* HTTP message body에 데이터를 직접 담아서 요청
    * HTTP API에서 주로 사용, JSON, XML, TEXT
    * 데이터 형식은 주로 JSON 사용

#### 요청 파라미터 - 쿼리 파라미터, HTML Form

`HttpServletRequest`의 `request.getParameter()`르 사용하며 다음 두가지 요청 파라미터를 조회할 수 있다.

* GET, 쿼리 파라미터 전송
    * `http://localhost:8080/request-param?username=hello&age=20`

* POST, HTML Form 전송

```
POST /request-param ...
content-type: application/x-www-form-urlencoded
username=hello&age=20
```

GET 쿼리 파라미터 전송 방식이든, POST HTML Form 전송 방식이든 둘다 형식이 같으므로 구분없이 조회할 수 있다.    
이것을 간단히 **요청 파라미터(request parameter)조회**라 한다.

#### RequestParamController

```java
package hello.springmvc.basic.request;

import lombok.extern.slf4j.Slf4j;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@Slf4j
@Controller
public class RequestParamController {

    /**
     * 반환 타입이 없으면서 이렇게 응답에 값을 직접 집어넣으면, view 조회 x
     */
    @RequestMapping("/request-param-v1")
    public void requestParamV1(HttpServletRequest request, HttpServletResponse response) throws IOException {
        String username = request.getParameter("username");
        int age = Integer.parseInt(request.getParameter("age"));
        log.info("username={}, age={}", username, age);

        response.getWriter().write("ok");
    }
}

```

* `request.getParameter()`
    * 여기서는 단순히 `HttpServletRequest`가 제공하는 방식으로 요청 파라미터를 조회했다.

#### hello-form.html - Post Form 페이지 생성

* 테스트용 HTML Form
* 리소스는 `/resources/stakc`아래에 두면 스프링 부트가 자동으로 인식한다.
* `src/main/resources/static/index.html`

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<form action="/request-param-v1" method="post">
    username: <input type="text" name="username"/>
    age: <input type="text" name="age"/>
    <button type="submit">전송</button>
</form>
</body>
</html>
```

> 참고  
> `Jar`를 사용하면 `webapp`경로를 사용할 수 없다. 이제부터 정적 리소스도 클래스 경로에 함께 포함해야 한다.

### 6-7. HTTP 요청 파라미터 - @RequestParam

#### requestParamV2

* `RequestParamController`의 메소드로 작성

```java
public class RequestParamController {
    @ResponseBody
    @RequestMapping("/request-param-v2")
    public String requestParamV2(
            @RequestParam("username") String memberName,
            @RequestParam("age") int memberAge) {

        log.info("username={}, age={}", memberName, memberAge);
        return "ok";
    }
}
```

* `@RequestParam`
    * 파리미터 이름으로 바인딩

* `@ResponseBody`
    * View 조회를 무시하고, HTTP message body에 직접 해당 내용 입력

**@RequestParam**의 `name(value)`속성이 파라미터 이름으로 사용

* `@RequestParam("username") String memberName`
* -> `request.getParameter("username")`

#### requestParamV3

```java
public class RequestParamController {
    @ResponseBody
    @RequestMapping("/request-param-v3")
    public String requestParamV3(
            @RequestParam String username,
            @RequestParam int age) {

        log.info("username={}, age={}", username, age);
        return "ok";
    }

}
```

HTTP 파라미터 이름이 변수 이름과 같으면 `@RequestParam(name = "xx")`생각 가능

#### requestParamV4

```java
public class RequestParamController {
    @ResponseBody
    @RequestMapping("/request-param-v4")
    public String requestParamV4(String username, int age) {
        log.info("username={}, age={}", username, age);
        return "ok";
    }
}
```

`String`, `int`, `Integer`등의 단순 타입이면 `@RequestParam`도 생략 가능

> 주의    
> `@RequestParam`애노테이션을 생략하면 스프링 MVC는 내부에서 `required=false`를 적용한다.    
> `required`옵션은 바로 다음에 설명한다.

> 참고    
> 이렇게 애노테이션을 완전히 생략해도 되는데, 너무 없는 것도 약간 과하다는 강사님의 주관적인 생각...   
> `@RequestParam`이 있으면 명확하게 요청 파라미터에서 데이터를 읽는 다는 것을 알 수 있다.

#### requestParam - 파라미터 필수 여부

```java
public class RequestParamController {
    @ResponseBody
    @RequestMapping("/request-param-required")
    public String requestParamRequired(
            @RequestParam(required = true) String username,
            @RequestParam(required = false) Integer age) {

        log.info("username={}, age={}", username, age);
        return "ok";
    }
}
```

* `@RequestParam.required`
    * 파라미터 필수 여부
    * 기본값이 파리미터 필수(`true`)이다.

* `/request-param`요청
    * `username`이 없으므로 400 예외가 발생한다.

**주의! - 파라미터 이름만 사용**
`/request-param?username=`    
파리미터 이름만 있고 값이 없는 경우 -> 빈문자로 통과

**주의! - 기본형(primitive)에 null 입력

* `/request-param`요청
* `@RequestParam(required = false) int age`
    * `null`을 `int`에 입력하는 것은 불가능 (500 예외 발생)
    * `null`을 받을 수 있는 `Integer`로 변경하거나, 또는 다음에 나오는 `defaultValue`사용

#### requestParamDefault - 기본 값 적용

```java
public class RequestParamController {
    @ResponseBody
    @RequestMapping("/request-param-default")
    public String requestParamDefault(
            @RequestParam(required = true, defaultValue = "guest") String username,
            @RequestParam(required = false, defaultValue = "-1") int age) {

        log.info("username={}, age={}", username, age);
        return "ok";
    }
}
```

파라미터 값이 없는 겨우 `defaultValue`를 사용하면 기본 값을 적용할 수 있다.    
이미 기본 값이 있기 때문에 `required`는 의미가 없다.

`defalutValue`는 빈 문자의 경우에도 설정한 기본 값이 적용된다.    
`/request-param?username=`

#### requestParamMap - 파라미터를 Map으로 조회하기

```java
public class RequestParamController {
    @ResponseBody
    @RequestMapping("/request-param-map")
    public String requestParamMap(@RequestParam Map<String, Object> paramMap) {
        log.info("username={}, age={}", paramMap.get("username"), paramMap.get("age"));
        return "ok";
    }
}
```

파라미터를 Map, MultiValueMap으로 조회할 수 있다.

* `@RequestParam Map`
    * `Map(key=value)`

* `@RequestParam MultiValueMap`
    * `MutiValueMap (key=[value1, value2, ...] ex) (key=userIds, value=[id1, id2])`

파라미터의 값이 1개가 확실하다면 `Map`을 사용해도 되지만, 그렇지 않다면 `MutiValueMap`을 사용하자.

> MTH   
> 헤더 정보를 가져오는 `@RequestHeader`의 사용법과 별반 다르지 않아서 쉽게 익힐 수 있을것이다.    
> 어짜피 둘다 key, value 형태의 데이터를 뽑아오는 것이다.

### 6-8. HTTP 요청 파라미터 - @ModelAttribute

실제 개발을 하면 요청 파라미터를 받아서 필요한 객체를 만들고 그 객체에 값을 넣어주어야 한다. 보통 다음과 같이 코드를 작성할 것이다.

```
@RequestParam String username;
@RequestParam int age;

HelloData data = new HelloData();
data.setUserNamd(username);
data.setAge(age);
```

스프링은 이 과정을 완전히 자동화해주는 `@ModelAttribute`기능을 제공한다.

#### HelloData

* 요청 파리미터를 바인딩 받을 객체
* `src/main/java/hello/springmvc/basic/HelloData.java`

```java
package hello.springmvc.basic;

import lombok.Data;

@Data
public class HelloData {
    private String username;
    private int age;
}
```

* 롬복 `@Data`
    * `@Getter`, `@Setter`, `@ToString`, `@EqualsAndHashCode`, `@RequiredArgsContructor`를 자동으로 적용해준다.

#### modelAttributeV1

* `RequestParamController`의 메소드로 작성
* `@ModelAttrubute`적용

```java
public class RequestParamController {
    @ResponseBody
    @RequestMapping("/model-attribute-v1")
    public String modelAttributeV1(@ModelAttribute HelloData helloData) {
        log.info("username={}, age={}", helloData.getUsername(), helloData.getAge());
        return "ok";
    }
}
```

마치 마법처럼 `HelloData`객체가 생성되고, 요청 파리미터의 값도 모두 들어가 있다.   
스프링 MVC는 `@ModelAttribute`가 있으면 다음을 실행한다.

* `HelloData`객체를 생성한다.
* 요청 파라미터의 이름으로 `HelloData`객체의 프로퍼티를 찾는다. 그리고 해당 프로퍼티의 setter를 호출해서 파라미터의 값을 입력(바인딩)한다.
* 예) 파라미터 이름이 `uwername`이면 `setUsername()`메서드를 찾아서 호출하면서 값을 입력한다.

#### 프로퍼티

객체에 `getUsername()`, `setUsername()`메서드가 있으면, 이 객체는 `username`이라는 프로퍼티를 가지고 있다.   
`username`프로퍼티의 값을 변경하면 `setUsername()`이 호출되고, 조회하면 `getUsername()`이 호출된다.

#### 바인딩 오류

`age=abe`처럼 숫자가 들어가야 할 곳에 문자를 넣으면 `BindException`이 발생한다. 이런 바인딩 오류를 처리하는 방법은 검증 부분에서 다룬다.

#### modelAttributeV2 - @ModelAttribute 생략

```java
public class RequestParamController {
    @ResponseBody
    @RequestMapping("/model-attribute-v2")
    public String modelAttributeV2(HelloData helloData) {
        log.info("username={}, age={}", helloData.getUsername(), helloData.getAge());
        return "ok";
    }
}
```

`@ModelAttribute`는 생략할 수 있다.    
그런데 `@RequestParam`도 생략할 수 있으니 혼란이 발생할 수 있다.

스프링은 해당 생략시 다음과 같은 규칙을 적용한다.

* `String`, `int`, `Integer`같은 단순 타입 = `@RequestParam`
* 나머지 = `@ModelAttrubute`(argument resolver로 지정해둔 타입 외)

> 참고    
> argument resolver는 뒤에서 학습한다.

### 6-9. Http 요청 메시지 - 단순 텍스트

* **HTTP message body**에 데이터를 직접 담아서 요청
    * HTTP API에서 주로 사용, JSON, XML, TEXT
    * 데이터 형식을 주로 JSON 사용
    * POST, PUT, PATCH

요청 파라미터와 다르게, HTTP 메시지 바디를 통해 데이터가 직접 데이터가 넘어오는 경우는 `@RequestParam`, `@ModelAttrubute`를 사용할 수 없다.(물론 HTML Form 형식으로 전달되는
경우는 요청 파라미터로 인정된다.)

#### RequestBodyStringController

* 텍스트 메시지를 HTTP 메시지 바디에 담아서 전송하고 읽기
* `src/main/java/hello/springmvc/basic/request/RequestBodyStringController.java`

```java
public class RequestBodyStringController {
    @PostMapping("/request-body-string-v1")
    public void requestBodyString(HttpServletRequest request, HttpServletResponse response) throws IOException {
        ServletInputStream inputStream = request.getInputStream();
        String messageBody = StreamUtils.copyToString(inputStream, StandardCharsets.UTF_8);

        log.info("messageBody={}", messageBody);

        response.getWriter().write("ok");
    }
}
```

* HTTP 메시지 바디의 데이터를 `InputStream`을 사용해서 직접 읽을 수 있다.
* 서블릿 단계에서 배웠던 가장 원시적?!인 방법

#### requestBodyStringV2 - Input, Output 스트림

```java
public class RequestBodyStringController {
    @PostMapping("/request-body-string-v2")
    public void requestBodyStringV2(InputStream inputStream, Writer responseWriter) throws IOException {
        String messageBody = StreamUtils.copyToString(inputStream, StandardCharsets.UTF_8);
        log.info("messageBody={}", messageBody);
        responseWriter.write("ok");
    }
}
```

* 파라미터 자체를 `InputStream`으로 받아서 `HttpServletRequest`객체를 `ServletInputStream`으로 변환하는 코드를 생략했다.

스프링 MVC는 다음 파라미터를 지원한다.

* InputStream(Reader): HTTP 요청 메시지 바디의 내용을 직접 조회
* OutputStream(Writer): HTTP 응답 메시지의 바디에 직접 결과 출력

#### requestBodyStringV3 - HttpEntity

```java
public class RequestBodyController {
    @PostMapping("/request-body-string-v3")
    public HttpEntity<String> requestBodyStringV3(HttpEntity<String> httpEntity) throws IOException {
        String messageBody = httpEntity.getBody();
        log.info("messageBody={}", messageBody);

        return new HttpEntity<>("ok");
    }
}
```

스프링 MVC는 다음 파라미터를 지원한다.

* `HttpEntity`
    * HTTP header, body 정보를 편리하게 조회
    * 메시지 바디 정보를 직접 조회
    * 요청 파라미터를 조회하는 기능과 관계 없음 `@RequestParam`X, `@ModelAttrubute`X
    * **응답에도 사용 가능**
        * 메시지 바디 정보 직접 반환
        * 헤더 정보 포함 가능
        * view 조회x

`HttpEntity`를 상속받은 다음 객체들도 같은 기능을 제공한다.

* `RequestEntity`
    * HttpMethod, url 정보가 추가, 요청에서 사용

* `ResponseEntity`
    * Http 상태 코드 설정 가능, 응답에서 사용
    * `return new ResponseEntity<String>("Hello World", responseHeaders, HttpStatus.CREATED)`

> 참고    
> 스프링MVC 내부에서 HTTP 메시지 바디를 읽어서 문자나 객체로 변환해서 전달해주는데, 이때 HTTP 메시지 컨버터(`HttpMessageConverter`)라는 기능을 사용한다. 이것은 조금 뒤에 HTTP 메시지 컨커터에서 자세히 설명한다.

#### requestBodyStringV4 - @RequestBody

```java
public class RequestBodyStringController {
    @ResponseBody
    @PostMapping("/request-body-string-v4")
    public String requestBodyStringV4(@RequestBody String messageBody) throws IOException {
        log.info("messageBody={}", messageBody);

        return "ok";
    }
}
```

* `@RequestBody`
    * `@RequestBody`를 사용하면 HTTP 메시지 바디 정보를 편리하게 조회 가능
    * 헤더 정보가 필요하다면 `HttpEntity`를 사용하거나 `@RequestHeader`를 사용하면 된다.
    * 이렇게 메시지 바디를 직접 조회하는 기능은 요청 파라미터를 조회하는 `@RequestParam`, `@ModelAttrubute`와는 전혀 관계가 없다.

#### 요청 파라미터 vs HTTP 메시지 바디

* 요청 파라미터를 조회하는 기능: `@RequestParam`, `@ModelAttrubute`
* HTTP 메시지 바디를 직접 조회하는 기능: `@RequestBody`

##### @ResponseBody

`@ResponseBody`를 사용하면 응답 결과를 HTTP 메시지 바디에 직접 담아서 전달할 수 있다.    
물론 이 경우에도 view를 사용하지 않는다.

### 6-10. HTTP 요청 메시지 - JSON

#### RequestBodyJsonController

* `src/main/java/hello/springmvc/basic/request/RequestBodyJsonController.java`

```java
public class RequestBodyJsonController {

    private ObjectMapper objectMapper = new ObjectMapper();

    @PostMapping("/request-body-json-v1")
    public void requestBodyJsonV1(HttpServletRequest request, HttpServletResponse response) throws IOException {
        ServletInputStream inputStream = request.getInputStream();
        String messageBody = StreamUtils.copyToString(inputStream, StandardCharsets.UTF_8);

        log.info("messageBody={}", messageBody);
        HelloData helloData = objectMapper.readValue(messageBody, HelloData.class);
        log.info("username={}, age={}", helloData.getUsername(), helloData.getAge());

        response.getWriter().write("ok");
    }
}
```

* 서블릿 방식과 유사하다.(원시적...)
* `HttpServletRequest`를 직접 사용해서 직접 HTTP 메시지 바디에서 데이터를 읽어와서, 문자로 변환한다.
* 문자로 된 JSON 데이터를 Jackson 라이브러리인 `objectMapper`를 사용해서 자바 객체로 변환한다.

#### requestBodyJsonV2 = @RequestBody 문자 변환

```java
public class RequestBodyJsonController {

    @ResponseBody
    @PostMapping("/request-body-json-v2")
    public String requestBodyJsonV2(@RequestBody String messageBody) throws IOException {

        log.info("messageBody={}", messageBody);
        HelloData helloData = objectMapper.readValue(messageBody, HelloData.class);
        log.info("username={}, age={}", helloData.getUsername(), helloData.getAge());

        return "ok";
    }
}
```

* `@RequestBody`
    * `HttpMessageConverter` 사용 -> `StringHttpMessageConverter`적용

* `@ResponseBody`
    * 모든 메서드에 `@ResponseBody`적용
    * 메시지 바디 정보 직접 반환(view 조회x)
    * `HttpMessageConverter`사용 -> StringHttpMessageConverter 적용

* 이전에 학습했던 `@RequestBody`를 사용해서 HTTP 메시지에 데이터를 꺼내고 messageBody에 저장한다.
* 문자로 된 JSON 데이터인 `messageBody`를 `objectMapper`를 통해서 자바 객체로 변환한다.
* 문자로 변환하고 다시 json으로 변환하는 과정이 불편... `@ModelAttribute`처럼 한번에 객체로 변환할 수는 없을까?

#### requestBodyJsonV3 - @RequestBody 객체 변환

```java
public class RequestBodyJsonController {
    @ResponseBody
    @PostMapping("/request-body-json-v3")
    public String requestBodyJsonV3(@RequestBody HelloData helloData) {
        log.info("username={}, age={}", helloData.getUsername(), helloData.getAge());

        return "ok";
    }
}
```

* `@RequestBody`객체 파리미터
    * `@RequestBody HelloData data`
    * `@RequestBody`에 직접 만든 객체를 지정할 수 있다.

`HttpEntity`, `@RequestBody`를 사용하면 HTTP 메시지 컨버터가 HTTP 메시지 바디의 내용을 우리가 원하는 문자나 객체 등으로 변환해준다.   
HTTP 메시지 컨버터는 문자 뿐만 아니라 JSON도 객체로 변환해주는데, 우리가 방금 V2에서 했던 작업을 대신 처리해준다.    
자세한 내용은 뒤에 HTTP 메시지 컨버터에서 다룬다.

* `@RequestBody`는 생략 불가능
    * `@ModelAttrubute`에서 학습한 내용을 떠올려 보면...
    * 스프링은 `@ModelAttrubute`, `@RequestParam`해당 생략시 다음과 같은 규칙을 적용한다.
        * `String`, `int`, `Integet` 같은 단순 타입 = `@RequestParam`
        * 나머지 = `@ModelAttribute`(argument resolver로 지정해둔 타입 외)
    * 따라서 이 경우 `HelloData`에 `@RequestBody`를 생략하면 `@ModelAttribute`가 적용되어 버린다.
        * `HelloData data` -> `@ModelAttrubute HelloData data`
        * 따라서 생략하면 HTTP 메시지 바디가 아니라 요청 파라미터를 처리하게 된다.

> 주의    
> HTTP 요청시에 content-type이 application/json인지 꼭! 확인해야 한다. 그래야 JSON을 처리할 수 있는 HTTP 메시지 컨버터가 실행된다.

#### requestBodyJsonV4 - HttpEntity

* 앞서 배운 것과 같이 `HttpEntity`를 사용해도 무방하다.

```java
public class RequestBodyJsonController {
    @ResponseBody
    @PostMapping("/request-body-json-v4")
    public String requestBodyJsonV4(HttpEntity<HelloData> httpEntity) {
        HelloData data = httpEntity.getBody();
        log.info("username={}, age={}", data.getUsername(), data.getAge());
        return "ok";
    }
}
```

##### requestBodyJsonV5

```java
public class RequestBodyJsonController {

    /**
     * @RequestBody 생략 불가능(@ModelAttrubute 가 적용되어 버림)
     * HttpMessageConverter 사용 -> MappingJackson2HttpMessageConverter (content-type: application/json)
     *
     * @RequestBody 적용
     *    * 메시지 바디 정보 직접 반환(view 조회x)
     *    * HttpMessageConverter 사용 -> MappingJackson2HttpMessageConverter 적용 (Accept: application/json)
     */
    @ResponseBody
    @PostMapping("/request-body-json-v5")
    public HelloData requestBodyJsonV5(@RequestBody HelloData data) {
        log.info("username={}, age={}", data.getUsername(), data.getAge());
        return data;
    }
}
```

* `@ResponseBody`
    * 응답의 경우에도 `@ResponseBody`를 사용하면 해당 객체를 HTTP 메시지 바디에 직접 넣어줄 수 있다. 물론 이 경우에도 `HttpEntity`를 사용해도 된다.

* `@RequestBody`요청
    * JSON 요청 -> HTTP 메시지 컨버터 -> 객체
* `@ResponseBody`응답
    * 객체 -> HTTP 메시지 컨버터 -> JSON 응답

## Note