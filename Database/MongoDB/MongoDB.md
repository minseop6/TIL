# MongoDB
## Document Database
- `key-value` 쌍으로 구성된 `document`를 저장
- MongoDB의 `document`는 `JSON` 객체와 유사
- `key`의 `value`에는 `document`, `array`, `array of document`도 사용할 수 있음
- `Document`는 많은 프로그래밍 언어의 데이터 타입과 일치
- `Embedded document`와 `array`는 `join`의 필요성을 줄여줌
- 동적 스키마는 다형성을 지원
- MongoDB는 `collection`에 `document`를 저장
- `collection`은 RDB의 테이블과 유사

## Key Features
- ### High Perfomance
    - MongoDB는 고성능 데이터 지속성을 제공
        - 내장된 데이터 모델은 데이터베이스 시스템의 I/O 활동을 줄여줌
        - 인덱스는 빠른 쿼리를 지원하고 Embedded document와 array를 키에 포함할 수 있음
- ### Rich Query Language
    - MongoDB는 CRUD를 위한 풍부한 질의어를 지원함

- ### High Availability
    - MongoDB의 `replica set`이라고 불리는 복제 기능은 자동 장애 복구와 데이터 중복 저장을 제공
    - `replica set`은 MongoDB 서버들의 그룹으로 같은 데이터 집합을 유지하여 데이터의 가용성을 높임

- ### Horizontal Scalability
    - `Sharding`은 장치들의 클러스터에 데이터를 분산시킴

- ### Support for Multiple Storage Engines