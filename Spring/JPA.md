# JPA
----------------
## JPA란?
- EJB
  - 과거의 자바 표준(Entity Bean)
  - 과거의 ORM
  - 문제점
    - 코드가 지저분해짐
    - API의 복합성이 높음
    - 속도가 느림
- Hibernate
  - ORM Framework, Open Source SW
  - EJB2 스타일의 Entity Beans를 대체할 목적으로 개발됨
- JPA
  - Java Persistence API
  - 현재 자바의 ORM 기술 표준으로 인터페이스의 모음
    - 즉, 실제로 동작하는 것이 아님
    - JPA 인터페이스를 구현한 대표적인 오픈소스가 Hibernate
  - JPA 2.1 표준 명세를 구현한 3가지 구현체(Hibernate, EclipseLink, DataNucleus)
  - 버전
    - JPA 1.0 : 초기 버전, 복합키와 연관관계 기능이 부족
    - JPA 2.0 : 대부분의 ORM 기능을 포함, JPA Criteria 추가
    - JPA 2.1 : 스토어드 프로시저 접근, 컨버터, 엔티티 그래프 기능 추가

## JPA의 동작 과정
- JPA는 애플리케이션과 JDBC사이에서 동작
  - 개발자가 JPA를 사용하면, JPA 내부에서 JDBC API를 사용하여 SQL을 호출하여 DB와 통신
  - 즉, 개발자가 직접 JDBC API를 쓰는 것이 아님
- 예시
  - 저장 과정
    1. 개발자는 JPA에 저장할 객체를 넘김
    2. JPA가 엔티티를 분석
    3. JPA가 INSERT SQL을 생성
    4. JPA가 JDBC API를 사용하여 SQL을 DB에 적용
  - 조회 과정
    1. 개발자가 조회할 객체의 pk값을 JPA에 넘김
    2. JPA가 엔티티의 매핑 정보를 바탕으로 SELECT SQL을 생성
    3. JPA가 JDBC API를 사용하여 SQL을 DB에 적용
    4. JPA가 DB로부터 결과를 받아옴
    5. JPA가 결과를 객체에 모두 매핑
- 쿼리를 JPA가 만들어 주기 때문에 Object와 RDB간의 패러다임 불일치를 해결 가능

## JPA를 사용해야 하는 이유
- SQL 중심적인 개발에서 객체 중심으로 개발
- 생산성
  - JPA를 사용하는 것은 마치 Java Collection에 데이터를 넣었다 빼는 것처럼 사용할 수 있게 만듬
  - 간단한 CRUD
- 유지보수
  - 기존 : 필드 변경시 모든 SQL을 수정해야함
  - JPA : SQL은 JPA가 처리하기 때문에 필드만 추가하면됨
- Object와 RDB간의 패러다임 불일치 해결
- JPA의 성능 최적화 기능
  1. 1차 캐시와 동일성 보장 - 캐싱 기능
  2. 트랜잭션을 지원하는 쓰기 지연 - 버퍼링 기능
  3. 지연 로딩
    - 지연 로딩 : 객체가 실제로 사용될 때 로딩하는 전략
    - 즉시 로딩 : JOIN SQL로 한 번에 연관된 객체까지 미리 조회하는 전략
- 데이터 접근 추상화와 벤더 독립성
- 표준
