# JPA-Hibernate-DB-Reset
-------------
## DDL generation
- `Spring`은 EntityScan을 통해 `@Entity` 어노테이션이 명시한 클래스를 찾음
- `spring.jpa.generate-ddl=true` 옵션은 해당 데이터를 서버 시작시점에 DDL문을 생성해서 DB에 적용
- `spring.jpa.hibernate.ddl-auto` 옵션을 통해서 보다 상세한 데이터베이스 초기화를 설정할 수 있음
  - `none` : 아무것도 실행하지 않음(default)
  - `create` : 기존에 있던 테이블을 삭제하고 새로 생성
  - `create-drop` : 기존에 있던 테이블을 삭제하고 새로 생성한뒤 종료시점에 테이블 삭제
  - `update` : 테이블의 변경을 적용
  - `validate` : 엔티티와 테이블이 정상 매핑되었는지 검증
