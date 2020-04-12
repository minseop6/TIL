# Spring Security
--------------
## Spring Security란?
- 강력하고 늪은 커스터마이징 인증과 필터를 통한 접근제어 제공하는 프레임워크
- Spring 기반 어플리케이션의 보안을 위한 사실상의 표준

## 주요 기능
- 사용자 권한에 따른 URI 접근 제어
- DB와 연동하는 Local Strategy 로그인
- 쿠키를 이용한 자동 로그인
- 패스워드 암호와

## 인증(Authentication)과 인가(Authorization)
- `인증`은 `증명하다`라는 의미로 유저 id와 pw를 이용하여 로그인하는 과정
- `인가`는 `권한부여`나 `허가`와 같은 의미로 어떤 대상이 특정 목적을 실현하도록 허용(Access)하는것
- Web에서 `인증`은 해당 URI는 보안 절차를 거친 사용자들만 접근할 수 있음
- Web에서 `인가`는 URL에 접근한 사용자가 특정한 자격이 있다는 것을 의미

## 사용법
#### 1. 의존성 추가
- Spring Framework 5.1.4 version 기준

```xml
<!-- pom.xml -->

<!-- Spring Security -->
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-core</artifactId>
    <version>4.2.3.RELEASE</version>
</dependency>
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-web</artifactId>
    <version>4.2.3.RELEASE</version>
</dependency>
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-config</artifactId>
    <version>4.2.3.RELEASE</version>
</dependency>
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-taglibs</artifactId>
    <version>5.2.2.RELEASE</version>
</dependency>
```

#### 2. web.xml 설정
- Spring Security는 `DelegatingFilterProxy`를 사용
  - `DelegatingFilterProxy`는 모든 요청을 가로채는 filter

```xml
<!-- web.xml-->

<!-- Spring Security -->
<filter>
    <filter-name>springSecurityFilterChain</filter-name>
    <filter-class>org.springframework.web.filter.DelegatingFilterProxy</filter-class>
</filter>
<filter-mapping>
    <filter-name>springSecurityFilterChain</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```
- \<filter-name> : Filter 이름 등록
- \<filter-class> : Filter로 사용할 클래스
- \<filter-mapping> : 등록한 Filter 이름과 url을 매핑 (/* : 모든 request)
- 이 Filter를 사용하면 Spring이 요청을 가로채서 해당 사용자의 `인증`, `권한`을 자동으로 확인해줌

```xml
<!-- web.xml -->

<!-- The definition of the Root Spring Container shared by all Servlets and Filters -->
<context-param>
  <param-name>contextConfigLocation</param-name>
  <param-value>classpath:spring/*-context.xml</param-value>
</context-param>

<!-- Creates the Spring Container shared by all Servlets and Filters -->
<listener>
  <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
</listener>
```

#### 3. security-context.xml 설정
##### 1. beans 설정

```xml
<!-- security-context.xml -->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:security="http://www.springframework.org/schema/security"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/security
       http://www.springframework.org/schema/security/spring-security.xsd">

</beans>
```

##### 2. Authentication 설정

```xml
<!-- Authentication(인증) 설정 -->

<!--방법 1. User Authentication with In-Memory definition-->
<security:authentication-manager>
    <security:authentication-provider>
        <security:user-service>
            <security:user name="admin" password="1234" authorities="ROLE_ADMIN"/>
            <security:user name="testUser" password="test" authorities="ROLE_USER"/>
        </security:user-service>
    </security:authentication-provider>
</security:authentication-manager>

<!--방법 2. Other Authentication Provider (Using Database)-->
<security:authentication-manager>
    <security:authentication-provider>
    <security:jdbc-user-service
        data-source-ref="dataSource"
        users-by-username-query="select id, pw, enabled from user where id=?"
        authorities-by-username-query="select id, authority from user where id=?"/>
    </security:authentication-provider>
</security:authentication-manager>
```
- \<security:user-service>
  - 메모리상에 일시적으로 사용자를 정의
- \<security:jdbc-user-service>
  - DB에 사용자 계정 정보를 저장

##### 3. Authorization 설정

```xml
<!-- Authorization(권한) 설정 -->
<security:http auto-config="true" use-expressions="true">
    <security:intercept-url pattern="/secured/**" access="hasRole('ROLE_USER')" />
    <security:intercept-url pattern="/admin/**" access="hasRole('ROLE_ADMIN')" />
    <security:intercept-url pattern="/login" access="permitAll()" />
    <security:intercept-url pattern="/security/**" access="permitAll()" />
    <security:intercept-url pattern="/" access="permitAll()" />
    <security:intercept-url pattern="/resources/**" access="permitAll()" />
    <security:intercept-url pattern="/**" access="denyAll()" />
    <security:form-login login-page="/login"
      username-parameter="id"
      password-parameter="pw"
      login-processing-url="/login"
      default-target-url="/security/home"
     />
    <security:logout logout-url="/logout"
      logout-success-url="/security/home"
    />
</security:http>
```
- auto-config="true"
  - form기반 로그인, 기본 인증 및 로그아웃 메커니즘을 자동으로 활성화
- use-expressions="ture"
  - Spring EL Expressions 사용을 활성화
  - Expression-Based Access Control
  |Expression|Description|
  |------|------|
  |hasRole([role])|현재 로그인한 주체(principal)가 권한을 가지고 있으면 true 리턴|
  |hasAnyRole([role1, role2])|현재 로그인한 주체가 제공된 권한 중 하나라도 가지고 있으면 true 리턴|
  |principal|현재 로그인한 사용자를 나타내는 객체에 직접 액세스|
  |authentication|security-context에서 얻은 현재 Authentication 객체에 직접 액세스|
  |permitAll|모든 사용자 접근 가능|
  |denyAll|모든 사용자 접근 불가능|
  |isAnonymous()|현재 로그인한 사용자가 익명 사용자인 경우 true 리턴|
  |isRememberMe()|현재 로그인한 사용자가 기억하고 있는 사용자인 경우 true 리턴|
  |isAuthenticated()|현재 로그인한 사용자가 익명이 아닌경우 true 리턴(인증만 되어있으면 접근 허용)|
  |isFullyAuthenticated()|현재 로그인한 사용자가 익명 또는 기억하고 있는 사용자가 아닌 경우 true 리턴|

- \<security:intercept-url>
  - 보안이 필요한 요청 URL에 대한 패턴을 정의
  - access
    - 해당 패턴과 일치하는 요청된 URL을 볼 수 있는 권한이 있는 사용자의 역할을 정의
    - 권한은 특정 사용자에게 할당된 역할 목록을 쉼표로 분라하여 사용할 수 있음
- \<security:form-login>
  - `login-page="/login"`
    - 로그인 페이지 주소지정
  - `username-parameter="id"`, `password-parameter`
    - ID, PW로 사용할 변수명(view에서 name 속성으로 지정)
  - `login-processing-url`
    - 인증 절차를 진행할 URL
  - `default-target-url`
    - 로그인 성공시 호출할 주소 지정
  - `authentication-failure-url="/login?error"`
    - Default로 적용됨
    - 잘못된 로그인을 할 때 동일한 로그인 페이지로 가지만 인증 실패를 알리기 위해 URL뒤에 `error`라는 `request parameter`를 붙임
- \<security:logout>
  - `logout-success-url="/login?logout"`
    - Default로 적용
    - 성공적을 로그아웃 하면 브라우저를 "/login?logout"로 redirect

#### 4. Controller

```java
@Controller
@RequestMapping("/security")
public class SecurityController {

	@GetMapping("/home")
	public ModelAndView home(HttpSession session) {

		ModelAndView model = new ModelAndView();
		model.setViewName("security/index");

		String user = (String) session.getAttribute("user");
		model.addObject("user", user);

		return model;
	}

	@GetMapping("/login")
	public String login(@RequestParam(value="error", required=false) String error,
			@RequestParam(value="logout", required=false) String logout,
			Model model) {

		if(error != null) {
			model.addAttribute("error", "Login Fail");
		}
		if(logout != null) {
			model.addAttribute("logout", "Logout Success");
		}

		return "security/login";
	}

}
```

##### 5. Views

```html
<!-- index.html -->
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form"%>
<%@ taglib prefix="sec" uri="http://www.springframework.org/security/tags" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Insert title here</title>
</head>
<body>
  <sec:authorize access="isAuthenticated()">
    <sec:authentication property="principal.username" />
    <form action="/board/logout" method="POST">
      <button type="submit" name="button">LOGOUT</button>
      <input type="hidden" name="${_csrf.parameterName}" value="${_csrf.token}"/>
    </form>
  </sec:authorize>
  <sec:authorize access="isAnonymous()">
    <button type="button" id="login">LOGIN</button>
  </sec:authorize>
</body>
</html>

<script src="https://code.jquery.com/jquery-3.4.1.js" integrity="sha256-WpOohJOqMqqyKL9FccASB9O0KwACQJpFTUBLTYOVvVU=" crossorigin="anonymous"></script>
<script>
  $('#login').click(function(){
    location.href="/board/security/login";
  })
</script>

```

```html
<!-- login.jsp -->
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Insert title here</title>
</head>
<body>
  <form action="/board/login" method="POST">
    <input type="text" name="id" /><br>
    <input type="password" name="pw" /><br>
    <button type="submit" name="button">LOGIN</button>
    <input type="hidden" name="${_csrf.parameterName}" value="${_csrf.token}"/>
  </form>
</body>
</html>
```
