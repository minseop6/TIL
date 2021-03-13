# GraphQL
## GraphQL이란?
- facebook에서 만든 `Graph Query Language`로 API를 위한 쿼리 언어
- 타입 시스템을 이용해서 실행하는 서버사이드 런타임

## REST API의 단점을 극복하기 위해 만들어짐
- `REST API`는 API를 호출했을 때 상황에 따라 필요하지 않은 데이터도 받는 `Over Fetching`이 발생
- `REST API`는 원하는 데이터를 얻기 위해 여러 API를 호출하는 `Under Fetching`이 발생
- API를 만들 때 도메인 별로 엔드포인트를 갖기 때문에 각 도메인에 비슷한 API가 존재할 수 있음

## GraphQL의 장점
- 하나의 엔드포인트만 가지고 있음
- 클라이언트에서 쿼리를 작성하여 필요한 데이터를 받아옴
    - 요청 횟수와 응답 사이즈를 줄일 수 있음
    - `Over Fetching`, `Under Fetching` 문제 해결

## GraphQL의 단점
- 요청이 text로 전달되서 파일 전송 등의 구현이 복잡
- 캐싱 사용 불가 (Applo를 사용하여 해결 가능)
- 재귀적인 쿼리를 사용할 수 없음 (Applo를 사용하여 해결 가능)