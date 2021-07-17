# Onion Architecture
- 아키텍쳐 패턴중의 하나로 유지보수와 점직적인 시스템을 만들 수 있도록 해줌
- 좋은 결합도를 가짐
- 비지니스 로직은 객체 지향 컨텍스트 인터페이스를 사용하여 선언됨
- 이해관계가 분리되어 각 계층은 비슷한 변경을 갖는 개념을 제한함

## Layer
<img src="../img/Architecture/onion1.png" width="500" height="500">

### Domain Model
- Domain Model 계층의 의존성은 자기 자신한테만 종속됨
- 비지니스 entity를 나타냄

### Domain Service
- Domain service 계층은 Model Layer에서 정의된 entity들의 behavior를 구현

### Application Service
- Application Service 계층은 외부 infrastructure와 Domain Layer를 연결함