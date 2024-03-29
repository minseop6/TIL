# SSR & CSR

## SSR이란?

- Server Side Rendering의 약어
- 서버에서 렌더링함
- 요청시 서버에서 처리하여 새로고침으로 페이지 응답
- MPA(Multi Page Application)

## CSR이란?

- Client Side Rendering의 약어
- 클라이언트에서 `Javascript`를 통해서 렌더링 하는 방식
- SPA(Single Page Application)

## CSR의 장단점

#### 장점

- 트래픽 감소
  - 처음에 렌더링된 후 필요한 데이터만 받아오면 되기 때문에 상대적으로 서버 요청이 적음
- 사용자 경험
  - 새로고침이 발생하지 않아 사용자가 네이티브앱과 비슷한 경험을 할 수 있음

#### 단점

- 초기 렌더링 때 많은 JS 번들을 받아오기 때문에 초기 렌더링 속도가 `SSR`에 비해 느림
- 검색엔진
  - 어플리케이션의 소스를 확인하면 내용이 비어있어 검색엔진 크롤러가 데이터들을 제대로 수집하지 못함
  - 검색을 위해 `SSR`을 따로 구현해야함

## SSR의 장단점

#### 장점

- 검색엔진 최적화(SEO) 가능
- 성능 개선
  - 처음에 렌더링된 html을 클라이언트에 전달해 주기 때문에 초기로딩속도가 `CSR`에 비해 줄어듬

#### 단점

- 페이지 이동시 새로고침 및 중복된 로딩
- 서버 렌더링 부하

## SPA에서 SSR을 적용시켰을 때 문제점

- 프로젝트의 복잡도
- 성능의 악화
