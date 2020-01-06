# Spring Boot
-----------
### 개발 환경
- Java : 8
- IDE : Eclipse + STS
- DB : MySql

-----------
### 1. Eclipse 설치
https://www.eclipse.org/

### 2. 플러그인 설치 (STS, Gradle)
Eclipse Marketplace에서 STS, Gradle 플러그인 설치

### 3. 프로젝트 생성
File -> New -> Spring Starter Project

![starter1](../img/Spring/Spring-boot-start/starter1.png)

![starter2](../img/Spring/Spring-boot-start/starter2.png)

### 4. 정상 실행 테스트
```Java
package com.ms.study;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@SpringBootApplication
public class BootStudyApplication {

	public static void main(String[] args) {
		SpringApplication.run(BootStudyApplication.class, args);
	}

	@GetMapping("/")
	public String home() {

		return "Hello Spring Boot";
	}

}
```
Run As -> Spring Boot App (없으면 Java Application)

![starter3](../img/Spring/Spring-boot-start/starter3.png)


### 5. JSP view 연동
```Java
// src/main/rescources/application.properties

# MVC View
spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp
```
main 디렉토리 밑에 디렉토리 생성

![starter4](../img/Spring/Spring-boot-start/starter4.png)

views 폴더에 test.jsp 생성 후

```html
<%@ page language="java" contentType="text/html; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Insert title here</title>
</head>
<body>
	<h1>test.jsp</h1>
</body>
</html>
```

views와 연동을 확인하기 위한 컨트롤러 생성
```Java
package com.ms.study;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class testController {

	@RequestMapping("/")
	private String index() {
		return "test";
	}
}
```

![starter5](../img/Spring/Spring-boot-start/starter5.png)

(404 error가 발생할 경우)
```Java
//build.gradle

plugins {
	id 'org.springframework.boot' version '2.2.2.RELEASE'
	id 'io.spring.dependency-management' version '1.0.8.RELEASE'
	id 'java'
}

group = 'com.ms'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = '1.8'

repositories {
	mavenCentral()
}

dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
	implementation 'org.springframework.boot:spring-boot-starter-web'
	runtimeOnly 'com.h2database:h2'
	testImplementation('org.springframework.boot:spring-boot-starter-test') {
		exclude group: 'org.junit.vintage', module: 'junit-vintage-engine'
	}
	compile('org.apache.tomcat.embed:tomcat-embed-jasper') //추가
	compile('javax.servlet:jstl:1.2') //추가
}

test {
	useJUnitPlatform()
}
```
