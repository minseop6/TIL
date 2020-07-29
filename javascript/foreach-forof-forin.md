# JS 반복문

## forEach
- 모든 요소를 순회
- `break`, `return` 지원 안함
```js
let arr = ['a', 'b', 'c'];

arr.forEach((currentValue, index, array) => {
    console.log(currentValue); // result : 'a' 'b' 'c'
    console.log(index); //result : 0 1 2
    console.log(array); //result : ['a', 'b', 'c'] ['a', 'b', 'c'] ['a', 'b', 'c']
})
```

## for of
- `es6`에서 추가된 문법
- 반복 가능한 객체(Array, Map, Set, String ...)를 반복 하는 기능 수행
- 객체의 요소(Data)를 순회하기 위한 구문
- 단점
    - 인덱스가 문자로 반환됨

```js
let arr = ['a', 'b', 'c'];

for(let i in arr) {
    console.log(i); // result : '0', '1', '2'
}

```

## for in
- 객체의 속성 또는 배열의 요소를 반복하는 기능 수행
- 객체의 속성을 순회하기 위한 구문
- 장점
    - `for in`의 단점을 보완
    - `forEach`에서 지원하지 않는 `break`, `continue`, `return`을 지원

```js
let arr = ['a', 'b', 'c'];

for(let i of arr) {
    console.log(i); // result : 'a', 'b', 'c'
}

```