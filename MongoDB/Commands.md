# MongoDB-Commands
-----------
- help : `Shell` 도움말 출력
- show dbs : `DB` 목록 출력
- show collections : `Collection` 목록 출력
- use \<database\> : `DB` 전환(DB가 존재하지 않으면 DB 생성)

## Create Operations
- `Collection `생성 또는 `Collection`에 `document` 삽입 작업
- `Collection`이 존재하지 않을 때 `Collection` 생성
- db.\<collection\>.insertOne() : `Collection`에 한 개의 `doucument` 삽입
- db.\<collection\>.insertMany() : `Collection`에 여러 개의 `document` 삽입

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
  
## Read Operations
- `Collection`에서 `document` 조회
- db.\<collection\>.find() : `document` 조회
  - .pretty() : `document`를 깔끔하게 조회

## Update Operations
- `Collection`에 존재하는 `document` 수정
- db.\<collection\>.updateOne() : 한 개의 `document`의 필드 수정
- db.\<collection\>.updateMany() : 여러개의 `document`의 필드 수정
- db.\<collection\>.replaceOne() : `document` 전체 수정


## Delete Operations
- `Collection`에 존재하는 `document` 삭제
- db.\<collection\>.deleteOne() : 한 개의 `document` 삭제
- db.\<collection\>.deleteMany() : 여러 개의 `document` 삭제
