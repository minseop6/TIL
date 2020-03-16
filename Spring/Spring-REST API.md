# Spring-REST API
-------------------------
- 웹 브라우저에는 GET과 POST방식만 지원하고 있어서 PUT,PATCH,DELETE방식의 요청은 전송할 수 없음
-  스프링은 HiddenHttpMethodFilter를 이용해 PUT, PATCH, DELETE방식의 요청을 할 수 있음
- `form`태그의 method 속성 값으로 지정해줘야함

```html
<!-- Spring 설정 -->
<!-- web.xml에 추가 -->
<!--  Enable support for DELETE and PUT request methods with web browser clients -->
<filter>
  <filter-name>hiddenHttpMethodFilter</filter-name>
  <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
</filter>

<filter-mapping>
  <filter-name>hiddenHttpMethodFilter</filter-name>
  <url-pattern>/*</url-pattern>
</filter-mapping>
```

```java
//Spring Boot 설정
// HiddenHttpMethodFilter를 application.java 에 추가
@Bean
public HiddenHttpMethodFilter hiddenHttpMethodFilter(){
    HiddenHttpMethodFilter filter = new HiddenHttpMethodFilter();
    return filter;
}
```

```html
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form"%>

<!-- POST -->
<form action="/board/post/${board.bno}" method="POST">
    <input type="submit" value="삭제">
</form>

<!-- PUT -->
<form action="/board/post/${board.bno}" method="POST">
    <input type="hidden" name="_method" value="PUT"/>
    <input type="submit" value="삭제">
</form>

<!-- DELETE -->
<form action="/board/post/${board.bno}" method="POST">
    <input type="hidden" name="_method" value="DELETE"/>
    <input type="submit" value="삭제">
</form>
```
