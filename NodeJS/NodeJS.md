# Node.js
- 웹 브라우저에 종속적인 JS를 Chrome V8 엔진을 기반으로 외부에서 실행할 수 있는 Runtime 환경을 제공

## 특징
- ### 모듈 시스템
    - 모듈 : 독립적인 하나의 소프트웨어
    - 기능별 모듈화 가능
- ### 싱글 쓰레드(Single Thread)
    - 하나의 `Thread`만을 사용해서 여러 Clinet로부터 오는 `Request`를 처리
    - `Context Switching`으로 인한 오버헤드를 방지
- ### 이벤트 드리븐(Event Driven)
    - 기능별로 등록된 `Event Listener`
- ### Non-Blocking I/O
    - Non-Blocking : 비동기적 처리의 태스크들을 호출 스택에서 태스크 큐로 보내거나 태스크 큐로 부터 이벤트 루프를 통해 다시 스택으로 가져오는 I/O 형태
    - 하나의 `Thread`가 `Request`를 받으면 다음 처리에 요청을 보내놓고 다른 작업을 처리하다가 먼저 요청한 작업이 끝나면 이벤트를 받아서 `Response`
    - 동시에 `Request`가 오더라도 처리가 완료될 때 까지 기다리지 않아도 되기 떄문에 서버 부하가 적음
- ### 내장 객체

## 장점
- `Non-blocking I/O`와 단일 스레드 이벤트 루프를 통한 높은 처리 성능
- 이벤트 기반 비동기 방식이기 때문에 서버에 부하가 적음
- npm(node package manager)을 통한 다양한 모듈 제공
- 높은 생산성
- 실시간 웹 애플리케이션에 적합

## 단점
- 이벤트 기반 비동기방식이라 로직이 복잡한 경우 `Callback Hell`에 빠질 수 있음
- `Single Thread`이기 때문에 CPU 부하가 큰 작업에 적합하지 않음