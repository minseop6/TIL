# Apollo

## Apollo란?

- `GraphQL`의 클라이언트 라이브러리 중 하나로 상태 관리 플랫폼
- `Vue`, `Angular`, `React`를 모두 지원함

## 특징

- ### Query와 Mutation을 직접 전송
  - API를 호출하기 위해 `HTTP` 요청을 신경 쓸 필요 없음(`Fetch`, `Axios` 필요 없음)
- ### 전송받은 데이터 캐싱
  - `Query`를 통해 전송받은 데이터를 자동으로 캐싱해 서버의 부하를 줄일 수 있음
  - 크롬 브라우저 `Apollo Client Develop Tools` 익스텐션을 설치하면 캐시 상태와 정보를 확인 가능
- ### Local State 관리
  - 클라이언트의 `Local State`를 만들어 `Query`, `Mutation`, `Resolver` 사용 가능
    - `GraphQL` 서버에 지정되어 있는 `type` 중에서 필드를 생성해야함
    - 클라이언트에서 생성한 `Local State`는 서버에 전송되지 않아야 하므로 `@Client` 키워드를 사용
