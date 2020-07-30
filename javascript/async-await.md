# Async/Await
## 동기 / 비동기
### 동기
- 요청을 받으면 요청한 작업의 처리가 끝나고 다음 코드 실행
- 코드가 위에서부터 아래로 순서대로 실행됨을 의미

### 비동기
- 요청에 대한 처리가 끝나기전에 다른 작업을 처리
- 비동기 요청은 응답 시간이 모두 달라 순서대로 실행되지 않고 호출시간과 응답시간에 따라 동작을 수행

## async await
- 비동기 요청의 실행 순서 문제를 해결하기 위해 `ES6`부터 제공됨
```js
let delay = (msg) => {
    let ms = Math.floor(Math.random() * 1000) + 1;
    return new Promise((resolve) => {
        setTimeout(resolve, ms);
    }).then((v) => {
        console.log(v, `${ms} ms`);
    })
}

let asyncFunction = async () => {
    await delay('a');
    await delay('b');
    await delay('c');
}

/* result
a ###ms
b ###ms
c ###ms
*/
```