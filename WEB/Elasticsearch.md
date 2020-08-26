# Elasticsearch
- Apache Lucene 기반의 오픈소스 분산형 검색 및 분석 엔진
- 방대한 양의 데이터를 실시간으로 신속하게 저장, 검색, 분석할 수 있음
- 검색을 위해 단독으로 사용되기도 하고 `ELK(Elasticsearch / Logstash / Kibana)` 스택으로 사용되기도함

## 특징
- ### Scale out
    - `Shard`를 통해 규모가 수평적으로 늘어남
- ### High Availability
    - `Replica`를 통해 데이터의 안전성을 보장
- ### Schema Free
    - JSON 문서를 통해 데이터 검색을 수행하므로 스키마 개념이 없음
- ### RESTful
    - 데이터 `CRUD` 작업은 `HTTP RESTful API`를 통해 수행

## ELK Stack
- ### Logstash
    - 다양한 소스(e.g. DB, csv ...)의 로그 또는 트랜잭션 데이터를 수집, 집계, 파싱하여 `Elasticsearch`로 전달
- ### Elasticsearch
    - `Logstash`로부터 받은 데이터를 검색 및 집계를 하여 필요한 정보 획득
- ### Kibana
    - `Elasticsearch`의 빠른 검색을 통해 데이터 시각화 및 모니터링