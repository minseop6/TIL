# Spring-REST API
-------------------------
- 웹 브라우저에는 GET과 POST방식만 지원하고 있어서 PUT,PATCH,DELETE방식의 요청은 전송할 수 없음
-  스프링은 HiddenHttpMethodFilter를 이용해 PUT, PATCH, DELETE방식의 요청을 할 수 있음
- `form`태그의 method 속성 값으로 지정해줘야함

```java
// HiddenHttpMethodFilter를 application.java 에 추가
@Bean
public HiddenHttpMethodFilter hiddenHttpMethodFilter(){
    HiddenHttpMethodFilter filter = new HiddenHttpMethodFilter();
    return filter;
}
```

```html
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form"%>

<form action="/board/post/${board.bno}" method="POST">
    <input type="hidden" name="_method" value="DELETE"/>
    <input type="submit" value="삭제">
</form>
```
