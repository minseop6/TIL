# Jest
- `JS Test Framework`
- `Test Runner`, `Test Matcher`, `Test Mock` 모두 제공

## 사용법
1. ### npm install
```bash
$ npm install -D jest
```

2. ### package.json에 명령어 추가
```js
// package.json
{
    ...
    "scripts": {
        "test": "jest"
    }
    "jest": {
        "transform": {
            ".(ts|tsx)": "<rootDir>/node_modules/ts-jest/preprocessor.js"
        },
        "testRegex": "(/__tests__/.*|\\.(test|spec))\\.(ts|tsx|js)$",
        "moduleFileExtensions": ["ts", "tsx", "js"]
    }
    ...
}
```

3. ### Matchers
```js
// src/util/operator.ts
const operator = {
    sum(a: number, b: number): number {
        return a + b;
    }
}

export default operator;
```

```js
// test/operator.spec.ts
import operator from '../src/util/operator';

describe('Test', () => {
    // toBe test case
    test('toBe Example', () => {
        expect(operator.sum(1, 2)).toBe(3);
        expect(operator.sum(3, 2)).toBe(5);
        expect(operator.sum(5, 200)).toBe(205);
    })
    // not test case
    test('toBe Example', () => {
        expect(operator.sum(1, 2)).toBe(3);
        expect(operator.sum(3, 2)).not.toBe(0);
        expect(operator.sum(5, 200)).toBe(205);
    })
    // toEqual test case
    test('toEqual Example', () => {
        const data = {
            field1: 1,
            field2: 2
        };
        expect(data).toEqual({ field1: 1, field2: 2 });

    })
})
```

#### Truthiuness
- toBeNull : `null` 값을 매칭
- toBeUndefined : `undefined` 값을 매칭
- toBeDefined : `undefined` 가 아닐 때 매칭
- toBeTruthy : `true` `statement`일 때 매칭
- toBeFalsy : `false` `statement`일 때 매칭

#### Numbers
- toBeGreaterThan : 초과
- toBeGreaterThanOrEqual : 이상
- toBeLessThan : 미만
- toBeLessThanOrEqual : 이하

#### Strings
- toMatch : `string` 비교(정규식 사용 가능)

#### Arrays and iterables
- toContain : 배열 요소에 포함 여부 확인
