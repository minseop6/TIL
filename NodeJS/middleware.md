# Middleware
## Middleware란?
- 클라이언트에게 요청이 오면 요청에 대한 응답하기 전인 중간에 목적에 맞게 처리하는 함수
- 역할
    - 다음 미들웨어 호출(next 함수)
    - `req`, `res` 객체 변경 가능
    - 요청-응답 주기 종료(response method 사용)

## Middleware 유형
### 1. 애플리케이션 레벨 미들웨어
- app.use() or app.method() 함수를 이용해 app 오브젝트의 인스턴스에 바인드
- 미들웨어를 애플리케이션 영역에 지정한 path대로 처리 가능

```js
app.use((req, res, next) => {
    console.log('Middleware example');
    next();
})

// 특정 경로만 적용
app.use('/example', (req, res, next) => {
    console.log('Middleware example');
    next();
})
```

### 2. 라우터 레벨 미들웨어
- express.Router() 인스턴스에 바인드
- 사용 방법은 애플리케이션 레벨 미들웨어와 동일

### 3. 에러 핸들링 미들웨어
- 에러를 다루기 위한 미들웨어
- 미들웨어에 4개의 인자 사용 (err, req, res, next)

### 4. 써드파티 미들웨어
- `Express`에 기능을 추가하기 위한 미들웨어
- [써드파티 미들웨어]](https://expressjs.com/ko/resources/middleware.html)