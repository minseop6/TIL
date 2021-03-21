# Javascript This
- `this`는 크게 4가지 정도의 방법으로 사용됨
- `this`가 쓰이는 함수를 어떤 방식으로 실행하느냐에 따라서 그 역할이 구별됨

## 1. 기본 바인딩 (전역 객체)
- javascript 실행 환경의 전역 객체 (브라우저는 window 객체)
- `this`가 전역 객체를 context 객체로 갖음
- 전역 스코프에서 정의한 변수는 전역 객체에 등록됨

```js
console.log(this); // Window {0: global, window: Window, self: Window, document: document, name: "", location: Location, …}
```

```js
this.test1 = 'Test1';

console.log(this.test1) // 'Test1'

const doSomething = () => {
    this.test2 = 'Test2';
}

console.log(this.test1); // 'Test1'
console.log(this.test2); // undefined

doSomething();

console.log(this.test1); // 'Test1'
console.log(this.test2); // 'Test2'
```

## 2. 암시적 바인딩
- 객체를 통해 함수가 호출된다면 그 객체가 `this`의 `context` 객체

```js
function foo() {
    console.log(this.bar);
}

const obj = {
    bar: 'Test',
    func1: foo,
    func2: function() {
        console.log(this.bar);
    }
}

obj.func1();
obj.func2();
```

## 3. 명시적 바인딩
- 함수 객체는 call, apply, bind 메소드를 갖고 있는데 첫번째 인자로 넘겨주는 것이 `this`의 `context` 객체

```js
function foo() {
    console.log(this);
}

const obj = { bar: 'Bar' };
foo.call(obj); // { bar: 'Bar' }
foo.call('Test'); // String {"Test"}
```

## 4. new 바인딩
- 동작 순서
    1. 객체 생성
    2. 생성된 객체의 Prototype 체인이 호출 함수의 프로토타입과 연결됨
    3. 1에서 생성된 객체를 `this`의 `context` 객체로 사용하여 함수가 실행됨
    4. 함수가 객체를 반환하지 않는 한 1에서 생성된 객체가 반환됨

```js
function foo(val) {
    this.val = val;
}

const bar = new foo('test');
console.log(bar.val);
```