# HTTP
-------------
## HTTP란?
- Hyper Text Transfer Protocol의 약자
- 인터넷에서 데이터를 주고받을 수 있는 프로토콜

## HTTP 동작
- Request : client -> server
- Response : server -> client

## HTTP 특징
- HTTP 메시지는 HTTP Server와 HTTP Client에 의해 해석됨
- TCP/IP를 이용하는 응용 프로토콜
- 연결 상태를 유지하지 않는 비연결성 프로토콜
- 연결을 유지하지 않는 프로토콜이기 때문에 Request/Response 방식으로 동작

## Request
#### Request Method
- GET : 정보를 요청할 때 사용
- POST : 정보의 생성을 요청할 때 사용
- PUT : 정보의 수정을 요청할 때 사용
- DELETE : 자료의 삭제를 요청할 떄 사용

#### Request HTTP 메시지 구조
```
GET http://naver.com/ HTTP/1.1 //시작줄
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) ... //헤더
Upgrade-Insecure-Requests: 1 //본문
```

1. 시작줄
  - GET : HTTP Method
  - http://naver.com/ : 사이트 주소
  - HTTP/1.1 : HTTP 버전

2. 헤더

  요청에 대한 정보를 담고 있음

3. 본문

  요청을 할 때 함께 보낼 데이터를 담는 부분

## Response
#### Status code
- 1xx(조건부 응답) : 요청을 받았으며 작업을 계속함
- 2xx(성공) : 클라이언트가 요청한 동작을 수신하여 이해하고 성공적으로 처리함을 가리킴
- 3xx(리다이레션 완료) : 클라이언트는 요청을 마치기 위해 추가 동작을 취해야함
- 4xx(요청 오류) : 클라이언트에 오류가 있음을 나타냄
- 5xx(서버 오류) : 서버가 유효한 요청을 명백하게 수행하지 못함을 나타냄

#### Response HTTP 메시지 구조
```
HTTP/1.1 200 OK // 시작줄
Connection: keep-alive // 헤더 ~
Content-Encoding: gzip												 
Content-Length: 35653
Content-Type: text/html; // ~ 헤더

<!DOCTYPE html><html lang="ko" data-reactroot=""><head><title... //본문
```

1. 시작줄
  - 버전 상태코드 상태메시지로 구성

2. 헤더
  - 응답에 대한 정보를 담고있음

3. 본문
  - 응답 메시지에 담겨있는 HTML을 받아 브라우저가 화면에 렌더링
