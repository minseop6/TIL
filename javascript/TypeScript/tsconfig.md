# tsconfig
- 타입스크립트를 자바스크립트로 변환할 때의 설정을 정의해놓는 파일
- `tsc` 명령어를 사용하면 현재 폴더부터 상위 폴더로 순차적으로 `tsconfig.json` 파일을 탐색

## 타입스크립트 설정 파일 속성
### files
- 컴파일할 파일들을 지정하는 옵션

```js
{
    "files": ["app.ts", "./practice/test.ts"]
}
```

### include
- `files`와 달리 컴파일할 파일을 지정하는 것이 아닌 디렉토리를 지정
- 타입스크립트는 기본적으로 `node_modules`를 제외하지만 써드 파티 라이브러리의 타입을 정의해놓는 `@types` 디렉토리는 컴파일에 포함함
- 와일드 카드 패턴
    - `*` : 해당 디렉토리의 모든 파일을 검색
    - `**`: 하위 디렉토리를 재귀적으로 접근
    - `?` : 해당 디렉토리안에 파일의 이름 중 키워드를 포함하는 파일 검색

```js
{
    "include": ["src/**/*"]
}
```

### exclude
- `include`와 반대로 컴파일 제외할 디렉토리를 지정

```js
{
    "exclude": ["node_modules"]
}
```

### extends
- 특정 타입스크립트 설정 파일에서 다른 타입스크립트 설정을 가져와 추가할 수 있는 옵션
- 오버라이드 가능

```js
// config/bash.json
{
    "compilerOptions": {
        "noImplicitAny": true
    }
}

// tsconfig.json
{
    "extends": "./config/base.json"
}
```

### target
- 타입스크립트 파일을 컴파일 했을 때 빌드 디렉토리에 생성되는 자바스크립트의 버전 명시

```json
{
    "target": "esnext" // es3, es5, es6
}
```

### lib
- 타입스크립트 파일을 자바스크립트 파일로 컴파일 할 때 포함될 라이브러리 목록
- 대표적으로 `Promise` 객체, `dom` 관련 속성을 인식할 수 있는 `esnext`, `dom`, `dom.iterable` 사용

```js
{
    "lib": ["es2015", "dom", "dom.iterable"]
}
```

### allowJs
- 타입스크립트 컴파일 작업을 진행할 때 자바스크립트 파일의 포함 여부를 설정하는 옵션