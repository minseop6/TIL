# Replica Set
- 데이터를 여러 DB서버에 분산하여 저장 관리하는 기술
- 여러 서버에서 데이터를 동기화하는 프로세스
- 중복성을 제공하여 데이터의 가용성을 높임
- 결함 허용을 제공
- 하드웨어 고장이나 서비스 중단으로인한 장애를 회복할 수 있음

## 구성
- 노드를 최소 3개 이상으로 구성해야함
- 구성 노드들은 2초마다 서로에게 하트비트(ping)을 보냄
- 10초 이내에 하트비트가 반환되지 않으면 다른 멤버는 해당 멤버를 액세스할 수 없음
- ### One Primary node
    - 모든 Write와 Recives 작업 수행
    - 데이터 셋의 모든 변경사항을 `oplog`에 기록
- ### Secondary nodes
    - Primary가 보낸 oplog를 사용하여 비동기적으로 작업을 적용해서 Primary와 같은 데이터 셋을 가짐
- ### An Arviter node(optional)

## Automatic Failover
- Primary node의 대체
- Primary를 사용할 수 없을 때 적합한 Secondary가 선거를 실시해서 스스로 새로운 Primary node가 됨
- Replica set은 선택이 끝날 때까지 write작업을 처리할 수 없음
- Replica set은 Primary를 사용할 수 없을 때 Secondary에서 질의를 수행할 수 있도록 구성했다면 read 질의를 할 수 있음

## Read operation
- 기본적으로 클라이언트는 Primary에 Read 연산을 수행
- 클라이언트는 명시적으로 Secondary에서 Read 연산을 수행할 수 있음
- 비동기식 복제이기 때문에 Secondary에서 Read 연산을 수행하면 Primary의 데이터 상태를 반영하지 않은 데이터가 반환될 수 있음

## Replica Set 구성 예제

```bash
mongod --port 27111 --dbpath c:\data\node1 --replSet exrs
mongod --port 27112 --dbpath c:\data\node2 --replSet exrs
mongod --port 27113 --dbpath c:\data\arbiter --replSet exrs

mongo --port 27111
conf = { _id:"exrs", members:[ { _id:0, host:"localhost:27111" } ] } //Replica Set 환경 설정
rs.initiate(conf) // 복제 세트 초기화

rs.add("localhost:27112") // Secondary node 추가
rs.add("localhsot:27113", {arbiterOnly:true}) // Arbiter node 추가
//rs.addArb("localhost:27113")
db.isMater() // Replicaset 정보 출력 상세정보는 rs.status()
```

### Secondary