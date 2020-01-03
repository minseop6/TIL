# Component Life Cycle
---------
###### - 컴포넌트를 생성할 때는 `constructor` -> `componentWillMount` ->
 `render` -> `componentDidMount`순으로 실행
###### - 컴포넌트 업데이트 될때는 `componentWillReceiveProps` -> `shouldComponentUpdate`->
 `componentWIllUpdate` -> `render` -> `componentDidUpdate` 순으로 실행
###### - 컴포넌트가 소멸될 때 `componentWillUnmount` 실행
-------------
### constructor
생성자 메소드로서 컴포넌트가 처음 만들어 질 때 실행됩니다.

### componentWillMount
컴포넌트가 DOM 위에 만들어지기 전에 실행됩니다.

### render
컴포넌트 렌더링을 담당합니다.

### componentDidMount
컴포넌트가 만들어지고 첫 렌더링을 다 마친 후 실행되는 메소드입니다.

------------
### componentWillReceiveProps
컴포넌트가 prop 을 새로 받았을 때 실행됩니다.

### shouldComponentUpdate
prop 혹은 state 가 변경 되었을 때, 리렌더링을 할지 말지 정하는 메소드입니다.

### componentWillUpdate
컴포넌트가 업데이트 되기 전에 실행됩니다.

### componentDidUpdate
컴포넌트가 리렌더링을 마친 후 실행됩니다.

-------------------
### componentWillUnmount
컴포넌트가 DOM 에서 사라진 후 실행되는 메소드입니다.
