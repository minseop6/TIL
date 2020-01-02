# JSX
----------
## JSX(Javascript XML)란?

- `React`에서 사용하는 문법
- `javascript`안에서 `html`처럼 사용
- `React`에서는 `{}`로 `component`에서 쓰이는 `html`의 속성 값이나 `content`에 사용

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
