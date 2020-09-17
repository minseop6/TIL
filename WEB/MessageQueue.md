# Message Queue

- 메시지 기반의 미들웨어로 메시지를 이용하여 여러 애플리케이션, 시스템, 서비스들을 연결해줌
- `MOM(Message Oriented Middleware)`를 구현한 시스템으로 비동기 메시지를 사용하는 서비스들 사이에서 데이터를 교환해주는 역할
- `Producer`가 메시지를 큐에 전송하면 `Consumer`가 처리하는 방식
- 대표적인 메시지큐로는 `Apache ActiveMQ`, `Rabbit MQ`, `Kafka` 등이 있음

## 장점

- Asynchronous
- Decoupling : 애플리케이션과 분리 가능
- Resilience : 일부가 실패시 전체에 영향을 받지 않음
- Redundacy : 실패할 경우 재실행 가능
- Guarantees : 작업이 처리된걸 확인할 수 있음
- Scalable : 다수의 프로세스들이 큐에 메시지를 보낼 수 있음

## 사용처

- 다른 곳의 API로부터 데이터 송신
- 다양한 애플리케이션에 비동기 통신
- 이메일 발송 및 문서 업로드
- 많은 양의 프로세스 처리
