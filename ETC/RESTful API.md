# RESTful API
-----------------
## RESTful API란?
- REpresentaional State Transfer
- 분산 시스템 설계를 위한 아키텍처 스타일
- 리소스 중심으로 설계하고 `GET`, `POST`, `PUT`, `DELETE`, `PATCH` 등의 메소드를 정의
  - GET : 지정된 URI에서 리소스의 표현을 조회
  - POST : 지정된 URI에 신규 리소스를 생성
  - PUT : 지정된 URI에 리소스를 수정
  - DELETE : 지정된 URI의 리소스를 제거
  - PATCH : 리소스의 부분 업데이트

## REST의 구성 요소
- Resource
- Method
- Message

## REST API 제약 조건
- Client / Server : 클라이언트와 서버가 서로 분리되어야한다
- Stateless : 각 요청에 클라이언트의 콘텍스트가 서버에 저장되어서는 안된다
- Cacheable : 클라이언트는 응답을 캐싱할 수 있어야 한다
- Layered System : 클라이언트는 서버에 직접 연결되었는지 미들웨어에 연결되었는지 알 필요가 없어야 한다
- Code on demand : 서버에서 코드를 클라이언트에게 보내서 실행하게 할 수 있어야 한다
- Uniform Interface : 아키텍처를 단순화 시키고 작은 단위로 분리함으로써 클라이언트-서버의 각 파트가 독립적으로 개선될 수 있도록 해준다
