# Partition
- 대용량의 테이블이나 인덱스를 작은 논리적 단위인 파티션으로 나누는 것
- 대용량 DB의 경우 중요한 몇 개의 테이블에만 집중되어 데이터가 증가되므로, 이런 테이블들을 작은 단위로 나눠 분산시키면 성능 저하를 방지할 뿐만 아니라 데이터 관리도 쉬워짐
- 테이블이나 인덱스를 파티셔닝 하면 파티션키 또는 인덱스키에 따라 물리적으로 별도의 공간에 데이터가 저장됨
- 데이터 처리는 테이블 단위로 이루어지고 데이터 저장은 파티션별로 수행됨

## 장점
- 데이터 접근 시 액세스 범위를 줄여 쿼리 성능 향상
- 파티션별로 데이터가 분산되어 저장되므로 디스크의 성능이 향상
- 파티션별로 백업 및 복구를 수행하므로 속도가 빠름
- 시스템 장애 시 데이터 손상을 최소화
- 파티션 단위로 입, 출력을 분산시킴

## 단점
- 하나의 테이블을 세분화하여 관리하므로 세심한 관리가 요구됨
- 테이블간 조인에 대한 비용 증가
- 용량이 작은 테이블에 파티셔닝을 수행하면 오히려 성능 저하

## 파티션의 종류
- ### 범위 분할(Range Partitioning)
    - 지정한 열의 값을 기준으로 분할
- ### 해시 분할(Hash Partitioniong)
    - 해시 함수를 적용한 결과 값에 따라 데이터를 분할
    - 특정 파티션에 데이터가 집중되는 범위 분할의 단점을 보완한 것으로 데이터를 고르게 분산시킴
    - 특정 데이터가 어디에 있는지 판단할 수 없음
    - 데이터가 고른 컬럼에 효과적
- ### 조합 분할(Composite Partitioning)
    - 범위 분할로 분할한 다음 해시 함수를 적용하여 다시 분할하는 방식
    - 범위 분할한 파티션이 너무 커서 관리가 어려울 때 사용

## 인덱스 파티션
- 파티션된 테이블의 데이터를 관리하기 위해 인덱스를 나눈 것
- Local Partitioned Index가 Global Partitioned Index에 비해 데이터 관리가 쉬움
- ### Local Partitioned Index
    - 테이블 파티션과 인덱스 파티션이 1:1 대응되도록 파티셔닝
- ### Global Partitioned Index
    - 테이블 파티션과 인덱스 파티션이 독립적으로 구성되도록 파티셔닝