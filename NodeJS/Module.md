# Module
- 모듈은 독립적인 파일 스코프를 갖기 때문에 모듈 안에 선언한 모든 것들은 기본적으로는 해당 모듈 내부에서만 참조 가능
- 모듈 외부에서 사용하려면 모듈을 파일로 작성하고 외부에 공개할 대상을 `export` 해야함

## exports
```js
// test.ts
exports.test1 = () => {
    console.log('exports test1');
}

exports.test2 = () => {
    console.log('exports test2');
}
```

```js
// app.ts
const test = require('./test');

test.test1(); // result : exports test1
test.test2(); // result : exports test2
```

## module.exports
- `exports` 객체는 여러개의 프로퍼티 또는 메서드를 정의할 수 있지만 `module.exports`에는 하나의 값(e.g. 함수, 객체 ...)을 할당

```js
// test.ts
module.exporst = {
    test1() {
        console.log('module.exports test1');
    },
    test2() {
        console.log('module.exports test2');
    }
}
```

```js
// app.ts
const test = require('./test');

test.test1(); // result : module.exports test1
test.test2(); // result : module.exports test2
```

## export default
- `exports` `module.exports`는 `require` 로 모듈을 불러옴
- `export default`는 `import`로 모듈을 불러옴

```js
// test.ts
const test = {
    test1() {
        console.log('export default test1');
    },
    test2() {
        console.log('export default test2');
    }
}

export default test;
```

```js
// app.ts
import test from './test';

test.test1(); // result : export default test1
test.test2(); // result : export default test2
```