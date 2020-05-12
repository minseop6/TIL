# CORS
## CORS란?
- Corss Origin Resource Sharing의 약자로 도메인 또는 포트가 다른 서버의 자원을 요청하는 매커니즘
- 동일 출처 정책(same-origin policy)로 인해 CORS같은 상황이 발생 하면 외부서버에 요청한 데이터를 브라우저에서 보안목적으로 차단함

## CORS가 필요한 이유
1. XSS(Cross Site Scripting)
    - 사용자가 웹 사이트에 접속했을 때 정상적이지 않은 요청이 클라이언트에서 실행됨
    - Cookie의 Session 정보를 탈취 당할 수 있음
2. CSRF(Corss-Site Request Forgeries)
 - 웹 어플리케이션의 사용자가 의도하지 않은 처리를 웹 어플리케이션에서 실행하는 것을 나타냄