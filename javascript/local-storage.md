# Storage
----------
## Storage란?
- 특정 도메인 `session` 또는 `local storage`에 대한 엑세스를 제공
- `cookie`와 비슷하게 도메인과 관련된 특정 데이터를 서버가 아닌 클라이언트에 저장할 수 있는 기능을 제공
- `Window.sessionStorage` : 데이터가 Reload 했을 때 유지하지만 브라우저를 종료하면 삭제됨
- `Window.localStorage` : 데이터가 Reload 했을 때 뿐만 아니라 브라우저를 종료후 재실행해도 유지됨

## 사용법
- `localStorage`와 `sessionStorage`의 사용법은 동일
- 메소드 & 속성
|Name|Description|
|----|----|
|setItem(key, value)|해당 키 값으로 데이터 저장|
|getItem(key)|해당 키 값에 해당하는 이름을 가진 데이터 조회|
|removeItem(key)|해당 키 값에 해당하는 이름을 가진 데이터 삭제|
|key(index)|해당 인덱스 값을 가진 키의 이름을 조회|
|clear()|모든 데이터 삭제|
|length|저장된 데이터 수 조회|

- 데이터 저장

```javascript
window.localStorage.name = 'Kim';
window.localStorage[name] = 'Kim';
window.localStorage.setItem('name', 'Kim');
```

- 데이터 조회

```javascript
var name = window.localStorage.name;
var name = window.localStorage[name];
var name = window.localStorage.getItem('name');
```

- 데이터 삭제

```javascript
//특정 데이터 삭제
window.localStorage.removeItem('name');

//모든 데이터 삭제
window.localStorage.clear();
```
