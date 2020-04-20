# Arrow Function
- Arrow Function은 ES6의 문법
- `function` 키워드를 사용 함수를 만든 것보다 간단히 표한 가능
- ex)

```js
//basic function
var ex1 = function(){console.log("ex1")};
//arrow function
var ex2 = () => console.log("ex2");
```

## 기본 문법
```js
//매개변수가 없는 경우
var ex1 = () => console.log("ex1");
ex1(); //result: ex1

//매개변수가 하나인 경우
var ex2 = (x) => x;
ex2("ex2"); //result: ex2

//매개변수가 여러개인 경우
var ex3 = (a, b, c) => a + b + c;
ex3(1, 2, 3); //result: 6

//객체를 반활할 때
var ex4 = () => ( {a: 1, b: 2, c: 3} );
ex4(); //result: {a: 1, b: 2, c: 3}
```