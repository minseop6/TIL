# JpaRepository Method
-----------------

#### `save()` : 새로운 엔티티는 저장, 이미 존재하는 엔티티는 수정(`insert`, `update`)
##### - 특정 칼럼을 제외하고 `Insert`, `Update`하려면
```java
@CreationTimestamp
@Column(name="created_time", updatable=false)
private LocalDateTime created_time;

@UpdateTimestamp
@Column(name="updated_time", insertable=false)
private LocalDateTime updated_time;
```

#### `findOne()` : 엔티티 하나를 조회 (즉시 조회하여 객체를 전달)
#### `getOne()` : 엔티티 하나를 조회 (lazy-loading을 통해 객체를 전달)
#### `findAll()` : 모든 엔티티를 조회
#### `delete` : 엔티티 하나를 삭제

-----------
## 조회 기능 추가
```java
public interface UserRepository extends JpaRepository<User, Integer>{

	User findById(String id); //사용자 한명을 id로 조회
}
```
### 작성 규칙
- findBy### : 쿼리를 요청하는 메서드
- countBy### : 쿼리 결과 레코드 수를 요청하는 메서드

#### 쿼리 메소드에 포함할 수 있는 키워드
- And : 여러필드를 and 로 검색
- Or : 여러필드를 or 로 검색
- Between : 필드의 두 값 사이에 있는 항목 검색
- LessThan : 작은 항목 검색
- GreaterThanEqual : 크거나 같은 항목 검색
- Like : like 검색
- IsNull : null 인 항목 검색
- In : 여러 값중에 하나인 항목 검색
- OrderBy : 검색 결과를 정렬하여 전달
