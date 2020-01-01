# var, let, const의 차이점

1. 유효 범위
2. 값의 변환
---
## 1. 유효 범위
`var` : `function-scoped`<br>
`let`, `const` : `block-scoped`

## var(function-scoped)
```javascript

var str = "Test String";
if(str == "Test String"){
  var result = true;
} else {
  var result = false;
}

console.log(result);    // output : true
```

## let & const(block-scoped)
```javascript
var str = "Test String";
if(str == "Test String"){
  const result = true;
} else {
  const result = false;
}

console.log(result);    // ReferenceError: result is not defined
```

------

## 2. 값의 변환
## var
```javascript
var str = "First String";
console.log(str); // output : Frist String

var str = "Second String";
console.log(str); // output : Second String
```
## let & const
```javascript
const str = "First String";
console.log(str);

const str = "Second String";
console.log(str);

// SyntaxError: Identifier 'str' has already been declared
```
