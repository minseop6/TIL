# NoSQL
-----------
## NoSQL 이란?
- Not Only SQL의 약자로 기존 `RDBMS`와는 다른 형태의 데이터 저장기술을 의미
- `NoSQL`은 `RDBMS`와는 다른 형태의 저장구조를 가짐

## NoSQL의 종류
- Key-Value Store
  - `key`와 `value`로 이루어진 간단한 데이터 구조로 대부분의 `NoSQL`에서 사용
  - 기본적인 형태로 `value`에 String, Integer, List, Hash 등의 기본 자료형이 해당됨
  - 이러한 데이터 구조는 속도가 빠르고 분산저장 환경에 용이하여 `key`에 대한 엑세스 속도는 빠르지만 검색에는 취약한 특징이 있음

- Wide Column Store
  - `key/value` 형태의 데이터 구조에서 하나의 `key`에 하나의 `value`만 저장하는 단점을 극복하기 위해 `value`에 해당하는 값을 여러개의 `Column`형태로 저장
  - 데이터마다 다른 스키마를 가질 수 있음

- Document Store
  - `Document(ex. JSON, XML)` 형태로 데이터가 저장됨
  - 스키마가 유동적임

- Graph DB
- 데이터를 `node`간의 관계로 표현

## NoSQL의 특징
- 정적인 구조의 `RDBMS`보다 융통성있는 형태의 데이터 구조를 사용
- 분산 저장 환경에 용이하여 데이터 저장 및 검색 작업에 있어 뛰어난 성능을 가짐
- 단순한 데이터 검색에 용이한 `key/value`형태는 응답속도나 처리 효율에 큰 장점을 지니고 있어 빅데이터 환경에 특화됨
