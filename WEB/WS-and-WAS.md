# WS and WAS
------------

## WS(Web Server)
- 클라이언트로부터 `HTTP` 요청을 받고 정적인 컨텐츠(html, css ...)를 제공
- 동적 컨텐츠를 제공하기 위해 클라이언트 요청을 `WAS`로 보냄

## WAS(Web Application Server)
- 동적 컨텐츠 제공
- `HTTP`를 통해 어플리케이션을 수행해주는 미들웨어
- Web Application Server = Web Server + Web Container

#### WAS 주요 기능
- 프로그램 실행환경 및 DB 접속 기능
- 여러 트랜잭션 관리 기능
- 업무 처리하는 비지니스 로직 수행

## WS와 WAS를 구분하는 이유
- `WS`는 정적 데이터를 처리하는 기능을 분배하여 서버의 부담을 줄임
- `WAS`는 정적 데이터를 처리를 위해 지연되는 시간이 줄어 동적 컨텐츠의 처리속도가 향상됨
