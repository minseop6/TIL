# JPA-Entity
----------
#### @Entity
- `@Entity`가 붙은 클래스는 JPA가 관리하는 클래스로 해당클래스를 엔티티라고함
- `@Entity` 속성
 - name : JPA에서 사용할 엔티티 이름을 지정

#### @table
- 엔티티와 매핑할 테이블을 지정
- `@Table` 속성
 - name : 매핑할 테이블 이름을 지정
 - catalog : 데이터베이스 catalog 매핑
 - schema : 데이터베이스 schema 매핑
 - uniqueConstraints(DDL) : DDL 생성 시에 유니크 제약 조건 생성


 --------------
 ## 데이터베이스 스키마 자동 생성
- DDL을 애플리케이션 실행 시점에 자동으로 생성
- `hibernate.hbm2ddl.auto` 옵션의 속성값
  - `none` : 아무것도 실행하지 않음(default)
  - `create` : 기존에 있던 테이블을 삭제하고 새로 생성
  - `create-drop` : 기존에 있던 테이블을 삭제하고 새로 생성한뒤 종료시점에 테이블 삭제
  - `update` : 테이블의 변경을 적용
  - `validate` : 엔티티와 테이블이 정상 매핑되었는지 검증

------------
## 필드와 컬럼 매핑

### @Id
- Primary Key 매핑

### @Column
- `name` : 객체명과 DB 컬럼명을 다르게 하고 싶은 경우에 DB 컬럼명으로 설정할 이름을 name 속성으로 지정
- `insertable`
- `updatable` : 컬럼을 수정했을 때 DB에 추가할 것인지 여부
- `nullable` : null 가능 여부
- `unique`
- `columnDefinition` : 직접 컬럼 정보를 지정
- `length` : 문자 길이 제약 조건 지정
- `precision`

### @Enumerated
- Enum Type 매핑
- `EnumType.ORDINAL` : enum 순서를 DB에 저장
- `EnumType.String` : enum 이름을 DB에 저장
