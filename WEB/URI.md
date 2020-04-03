# URI
------------
## URL(Uniform Resource Locator)
- 자원
- 과거에는 URL이 가리키는게 파일소스
- 최근에는 Rewrite 등의 Apache, IIS, Tomcat 등의 핸들러를 자원이라 부름
- 요청하는 주소가 파일이라기 보다는 구분자로 봄
- 서비스를 제공하는 각 서버들에 있는 파일들의 위치를 표시하기 위한 것으로 접속할 서비스의 종류, 도메인명, 파일 위치 등을 포함
- ex) http://example.com/file/index.html <- 웹서버의 실제 파일위치를 나타내는 주소, `URL`이면서 `URI`

## URI(Uniform Resource Identifier)
- 통합 자원 식별자
- 인터넷에 있는 자원을 나타내는 유일한 주소
- `URI`의 존재는 인터넷에서 요구되는 기본조건으로서 인터넷 프로토콜에 항상 붙어다님
- `URI`은 `URL`과 `URN`을 포함
- ex) http://example.com/file/index <- `Rewrite`를 통해 index.html파일을 가리킴, `URI`이지만 `URL`은 아님
