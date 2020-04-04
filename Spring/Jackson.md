# Jackson
-----------
## Jackson 이란?
- Java 표준 라이브러리로 `JSON` 뿐만 아니라 `XML`/`YAML`/`CSV` 등 다양한 형식의 데이터를 지원하는 `데이터 처리 툴`
- `스트림 방식`이므로 속도가 빠르고 유연하며 `POJO`기반의 자바 객체들을 `JSON`으로 변환 가능

## 사용법
#### 설정
```xml
<!-- pom.xml -->
...

<!-- jackson -->
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-databind</artifactId>
  <version>2.9.7</version>
</dependency>
```

#### Java객체를 Json문자열로 변환
```java
//java 객체 생성
BoardVo posts = new BoardVo();
posts.setBno(1);
posts.setTitle("test");
posts.setContent("contents");

//json 문자열로 변환
ObjectMapper mapper = new ObjectMapper();
String testJson = mapper.writeValueAsString(posts);
```

#### Json문자열을 Java객체로 변환
```java
String testJson = "{\"title\" : \"test title\", \"content\" : \"test content\"}"; //json 문자열

//java 객체로 변환
ObjectMapper mapper = new ObjectMapper();
BoardVo convertJson = new BoardVo();
convertJson = mapper.readValue(testJson, BoardVo.class);
```
