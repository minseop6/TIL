# WebSocket
------
## WebSocket이란?
- 서버와 클라이언트가 실시간으로 양방향 통신을 할 수 있게 해주는 기술

## 사용 이유
- 웹은 `Request`/`Response`로 데이터를 주고 받아 네트워크의 연결을 유지하지 않음
- `WebSocket`개념으로 연결을 유지하며 실시간으로 데이터를 주고 받을 수 있음
- `header`가 상당히 작아 `overhead`가 적음

## WebSocket이 필요한 경우
1. 실시간 양방향 데이터 통신이 필요한 경우
2. 많은 수의 동시 접속자를 수용해야 하는 경우
3. 브라우저에서 TCP 기반의 통신으로 확장해야 하는 경우
4. 개발자에게 사용하기 쉬운 API가 필요할 경우
5. 클라우드 환경이나 웹을 넘어 SOA(Service Oriented Architecture) 로 확장해야 하는 경우