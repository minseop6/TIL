# MongoDB-Commands
-----------
- help : `Shell` 도움말 출력
- show dbs : `DB` 목록 출력
- show collections : `Collection` 목록 출력
- use \<database\> : `DB` 전환(DB가 존재하지 않으면 DB 생성)

## Insert
- `Collection `생성 또는 `Collection`에 `document` 삽입 작업
- `Collection`이 존재하지 않을 때 `Collection` 생성
- db.\<collection\>.insertOne() : `Collection`에 한 개의 `doucument` 삽입
- db.\<collection\>.insertMany() : `Collection`에 여러 개의 `document` 삽입
- db.\<collection\>.insert() : `Collection`에 한개 또는 여러 개의 `document` 삽입

#### Insert Behavior
- Collection Creation
  - `insert` 명령어를 실행할 때 `Collection`이 존재하지 않으면 `Collection` 생성
- \_id Field
  - `Collection`에 저장되는 각각의 `document`들은 `primary key` 역할을 하는 고유한 `_id` 필드를 필요로함
  - `document`를 `insert` 할 때 `_id`필드를 생략하면 MongoDB Driver가 자동적으로 `_id`필드에 `ObjectId`를 추가해줌
- Atomicity
  - MongoDB는 각각의 `document`에 대해 원자성을 지님
- Write Acknowledgement
  - `request`에 대한 `response`를 어느 시점에 주느냐에 대한 동작 방식

## Query
- `Collection`에서 `document` 조회
- db.\<collection\>.find() : `document` 조회
  - find().pretty() : `document`를 깔끔하게 조회
  - find({}) : 모든 `document` 조회
  - find({\<field> : \<value>}) : 특정 `document` 조회
  - Embedded
    - find({\<field>.\<Embedded field : \<value>}) : `Embedded Field`를 이용하여 특정 `document` 조회
  - Array
    - find({\<field> : {$all : ["\<value>"]}}) : `Array`에 존재하는 `value`를 포함한 `document` 조회
    - find({\<field> : \<array element>}) : `Array`에 존재하는 `value`를 포함한 `document` 조회
    - find({\<field>.\<index> : \<array element>}) : 특정 `Array`의 \<index> 번째의 `element`가 조건을 만족할 경우에 `document` 조회
    - $elemMatch : 최소 하나의 `Array element`가 조건을 만족할 경우에 `document` 조회
    - find({\<field> : {$size:\<value>}}) : `Array`의 `Length`를 이용하여 `document` 조회
    - find({\<field>.\<Embedded field> : \<array element>}) : `Array`에 내장된 필드가 특정 조건을 만족할경우 조회
  - Projection Field
    - 출력하고자 하는 필드는 1로 제외할 필드는 0으로 지정
    - `_id` 필드는 자동적으로 들어감(출력하지 않으려면 `_id=0`)
    - ex) db.inventory.find( { status: "A" }, { item: 1, status: 1 } ) : SELECT \_id, item, status from inventory WHERE status = "A"

#### Query Operators
- , : AND 조건
- $and : AND 연산자
- $or : OR 연산자

#### Null and Missing Field
- 예제 document : { \_id: 1, item: null }, { \_id: 2 }
- db.inventory.find( { item: null } ) : 두 `document` 모두 조회됨
- db.inventory.find( { item : { $type: 10 } } ) : id가 1인 `document`만 조회
- db.inventory.find( { item : { $exists: false } } ) : id가 2인 `document`만 조회

## Update
- `Collection`에 존재하는 `document` 수정
- db.\<collection\>.updateOne() : 한 개의 `document`의 필드 수정
- db.\<collection\>.updateMany() : 여러개의 `document`의 필드 수정
- db.\<collection\>.replaceOne() : `document`의 `_id`필드를 제외하고 전체 수정

#### Update Operators
- $set : 필드값 수정
- ex)

```sql
--MySQL
UPDATE inventory
SET size.uom='cm', status='P', lastModified=now()
WHERE item='paper'

--MongoDB
db.inventory.updateOne(
   { item: "paper" },
   {
     $set: { "size.uom": "cm", status: "P" },
     $currentDate: { lastModified: true }
   }
)
```

#### Update Behavior
- Atomicity
  - MongoDB는 각각의 `document`에 대해 원자성을 지님
- \_id Field
  - `_id` 필드값을 업데이트 할 수 없음
  - `document`를 `_id` 필드값이 다른 `document`로 `replace` 할 수 없음
- Field Order
  - 아래 두가지 예외를 제외하고 수정된 `document` 필드의 순서를 보존
    - `_id` 필드는 항상 `document`의 첫 번째 필드
    - 필드의 이름이 변경 될 경우 필드 순서가 변경 될 수 있음
- Upsert Option
  - Update 명령어를 실행했을 때 해당되는 `document`가 존재하지 않으면 새 `document` 삽입
  - 해당하는 `document`가 존재하면 업데이트 명령 수행
- Write Acknowledgement
  - `request`에 대한 `response`를 어느 시점에 주느냐에 대한 동작 방식

## Delete
- `Collection`에 존재하는 `document` 삭제
- db.\<collection\>.deleteOne() : 한 개의 `document` 삭제
- db.\<collection\>.deleteMany() : 여러 개의 `document` 삭제
  - deleteMany({}) : 모든 `document` 삭제

#### Delete Behavior
- Indexes
  - Delete 연산은 `Collection`으로부터 모든 `document`를 삭제하더라도 `Indexes`는 삭제하지 않음
- Atomicity
  - MongoDB는 각각의 `document`에 대해 원자성을 지님
- Write Acknowledgement
  - `request`에 대한 `response`를 어느 시점에 주느냐에 대한 동작 방식
