# Forward and Redirect
## Forward
- `Web Continter` 차원에서 페이지의 이동
- 실제로 웹 브라우저는 다른 페이지로 이동했는지 알 수 없음
- 웹 브라우저는 최초 호출한 URL만 표시하고 이동한 페이지의 URL 정보는 볼 수 없음
- 동일한 `Web Container`에 있는 페이지로만 이동 가능
- 현재 실행중인 페이지와 Forawd에 의해 호출될 페이지는 `request`, `response` 객체를 공유

## Redirect
- `Web Containter`는 `redirect`명령이 들어오면 웹 브라우저에게 다른 페이지로 이동하라는 명령을 내림
- 웹 브라우저는 URL을 지시된 주소로 변경하고 그 주소로 이동
- 다른 `Web Container`에 있는 주소로 이동 가능
- 새로운 페이지에서는 `request`, `response` 객체가 새로 생성됨