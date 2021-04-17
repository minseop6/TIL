# JSX
----------
## JSX(Javascript Extension)란?

- `HTML` 문법을 JS 코드 내부에서 사용할 수 있도록 JS를 확장한 문법
- 빌드 시 `Babel`에 의해 JS로 변환됨

```javascript
import React from 'react';

const user = "react user";

function App() {
  return (
    <div>
      <h1>Hello {user}!</h1>
    </div>
  );
}

export default App;
```

## JSX 특징
### 1. class는 className으로 작성
- HTML요소에 class값을 정의할 때, class라는 단어가 ECMAScript6의 클래스 문법과 겹치는 예약어이기 때문에 `className`사용

### 2. for는 htmlFor로 작성
- 1번과 같은 이유

### 3. 이벤트는 camelCase로 작성
 
 ```html
 <button onClick="click">
 ```

### 4. 주석

```html
<!-- html -->
```

```js
{/* jsx */}
```

### 5. JSX 내부에서 JS사용 가능

```js
<div>
{ console.log(this.props) }
</div>
```

