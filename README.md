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

## Note

