# Component
-------
- `Component`에서는 `props`와 `state`를 사용
- `props`는 부모 컴포넌트가 자식 컴포넌트에게 주는 값으로 자식 컴포넌트에서는 `props`를 받아오기만하고 받아온 `props`를 수정할 수 없습니다.
-`state`는 컴포넌트 내부에서 선언되어 내부에서 값을 변경할 수 있습니다.

## state
### - state 정의

```javascript
import React from 'react';

class App extends React.Component{
  state = {
    count: 0
  };
  render(){
    return(
      <div>
        <h1>Hello React!</h1>
      </div>
    )
  }
}

export default App;

```

### - setState
`this.setState`는 state에 있는 값을 바꾸기 위해사용합니다. 이 함수가 호출되면 리렌더링되도록 설계되어있습니다.
```javascript
this.setState(current => ({count: current.count + 1})) // count값 증가
```

### - 예제 코드

```javascript
import React from 'react';

class App extends React.Component{
  state = {
    count: 0
  };
  add = () =>{
    this.setState(current => ({count: current.count + 1})); //count값 증가
  }
  minus = () =>{
    this.setState(current => ({count: current.count - 1})); //count값 감소
  }
  render(){
    return(
      <div>
        <h1>Count : {this.state.count}</h1>
        <button onClick={this.add}>ADD</button>
        <button onClick={this.minus}>MINUS</button>
      </div>
    )
  }
}

export default App;

```
