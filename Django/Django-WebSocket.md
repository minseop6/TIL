# Django-WebSocket
------
## WebSocket이란?
https://github.com/sksdk34/TIL/blob/master/ETC/WebSocket.md

## ASGI 란?
- `ASGI(Asynchronous Server Gateway Interface)`
- `WSGI(Web Server Gateway Interface)`를 계승하여 비동기 방식으로 실행
- `HTTP`, `HTTP/2` 및 `WebSocket`과 같은 프로토콜을 지원
- 비동기 요청인 웹 소켓을 처리하는 이벤트로서 `connect`, `send`, `receive`, `disconnect`가 있음

## Channels 란?
- `Django`에서 HTTP 프로토콜이 아닌 다른 프로토콜을 사용할 수 있게해줌
- `Channels`를 이용해서 `WebSocket`을 사용할 수 있음
- 연괄과 소켓을 비동기 처리
- `Channels`를 사용하면 `Channel layer`가 생겨 `HTTP message`뿐만 아니라 `WebSocket message`를 처리 가능

## Channel layer 란?
- 의사소통 시스템
- `channel`과 `group`이라는 두가지 개념이 존재
  - channel : 각 `channel`은 고유한 이름이 있어 누구든지 message를 보낼 수 있음
  - group : `group`에는 여러개의 `channel`들을 추가 또는 삭제 할 수 있음
