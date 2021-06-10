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

