# Serverless
## Serverless 란?
- 서버가 없다는 의미가 아닌 `BaaS(Backend as a Service)` 또는 `FaaS(Function as a Service)`에 의존해 작업을 처리한다는 의미

## BaaS (Backend as a Service)
- 어플리케이션 개발에 필요한 기능들을 `API`로 제공해줌
- 장점
    - 개발 시간의 단축
    - 서버 확장 작업의 불필요함
- 단점
    - 클라이언트 위주의 코드
    - 가격
    - 복잡한 쿼리가 불가능

## FaaS(Function as a Service)
- 함수를 서비스로 제공함으로써 어플리케이션 개발에서 함수를 실행하기 위해 서버를 올리고 런타임을 구성해 코드를 배포해야하는 일련의 과정을 생략
- 서버가 계속 대기하면서 사용자의 요청을 처리하는 것이 아니라 이벤트가 있을 때만 서버가 실행됨
- 장점
    - 비용
    - 인프라 관리, 보안
    - 확장성
- 단점
    - 자원의 제한
    - 강한 의존
    - local storage 사용 불가능
