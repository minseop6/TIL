# Kafka

- 메시지 큐의 일종으로 분산형 스트리밍 플랫폼
- 메시지를 메모리에 저장하는 다른 메시지 큐와 달리 메시지를 파일 시스템에 저장하여 메시지 유실을 줄일 수 있음
- 다른 메시지 큐는 `broker`가 `consumer`에게 메시지를 `push`하는 방식이지만 `Kafka`는 `consumer`가 `broker`로부터 직접 메시지를 가지고 가는 `pull` 방식으로 동작하기 때문에 `consumer`는 성능 최적화 가능

## 주요 개념

- ### Topic
  - 메시지는 `topic`으로 분류됨
- ### Partition
  - `topic`이 나눠지는 단위
  - 메시지를 병렬로 처리하기위해 `topic`을 여러개의 `partition`으로 나눔
- ### Log
  - `partition` 내의 하나의 메시지
- ### Offset
  - `partition`의 각 메시지를 식별할 수 있는 유니크한 값
  - 일종의 인덱스
- ### Producer
  - 메시지 생산하는 주체
  - `consumer`의 존재는 알지 못함
- ### Consumer
  - 메시지 소비자
  - `producer`의 존재를 알지 못함
  - 특정 `topic`을 구독함으로써 메시지를 가져옴
- ### Consumer Group
  - 특정 `topic`은 `consumer group`과 `1:N` 매칭을 해야함
- ### Broker
  - 카프카 서버를 지칭
  - 동일한 노드에서 여러개의 `broker` 서버를 띄울 수 있음
- ### Zookeeper
  - 분산 메시지 큐의 정보를 관리해 주는 역할
- ### Replication
  - `Scale Out`
