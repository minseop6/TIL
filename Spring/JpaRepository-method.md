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
