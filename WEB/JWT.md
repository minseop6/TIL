# JWT
- `JSON Web Token`의 약어
- `JSON` 포맷을 이용하여 사용자에 대한 속성을 저장하는 `Claim`기반의 `Web Token`으로 `RFC-7519` 표준
- 토큰 자체를 정보로 사용하는 `Self-Contained` 방식으로 정보를 전달

## 구조
1. ### Header
    - `typ`와 `alg` 두 가지 정보로 구성됨
    - typ : 토큰의 타입 지정
    - alg : `Signature`를 만드는 해시 암호화 알고리즘 지정
2. ### Payload
    - 토큰에 담을 `Claim` 정보를 포함(`key-value` 쌍으로 이루어짐)
    - `Registered`, `Public`, `Private`의 3가지 유형으로 나뉨
    - 만료일시, 발급일시, 발급자, 권한정보 등이 포함
3. ### Signature
    - `Payload`가 위변조되지 않았다는 사실을 증명하는 문자열
    - `Header`, `Payload`, `Secret Key`를 포함하여 암호화되어 있음

## Client-Server 인증 과정
1. Clinet에서 로그인
2. Server에서 로그인 확인 후 `Scret Key`를 통해 `Access Token`을 발급하여 Client에 `JWT` 반환
3. Client에서 `JWT`를 보관하다가 Server에 요청을 할 때 마다 `JWT`를 `Request Header`에 포함하여 전달
4. Server는 Client가 전달한 `JWT`의 `Signature`를 확인하고 `JWT`에서 사용자 정보를 확인
5. 사용자 정보가 올바르다면 Client의 `Request`에 대한 `Response`

## 장점
- 사용자 인증에 필요한 정보가 토큰 자체에 포함되어 있기 때문에 별도의 인증 저장소가 필요없음
- 서버를 확장하거나 유지, 보수하는데 유리
- 토큰 기반으로하는 다른 인증 시스템에 접근 가능

## 단점
- 한번 발급된 토큰은 값을 수정하거나 폐기가 불가능
    - 세션/쿠키 방식의 경우 `SessionID`가 변질되었다고 판단되면 세션을 지우면 되지만 `JWT`는 한 번 발급되면 유효기간이 종료될 때 까지 사용가능하므로 유효기간이 종료되기 전까지 정보들을 탈취할 수 있음
- 세션/쿠키 방식에 비해 `JWT`의 길이가 길어 인증이 필요한 요청이 많아질수록 서버의 자원낭비가 커짐