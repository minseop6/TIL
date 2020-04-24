# React interlocking
## 1. React app 생성
```powershell
# npm 설치 확인
> npm -v

> npm install -g yarn # yarn 설치
> yarn --version # yarn 설치 확인

# react app을 만들어주는 패키지 설치
> npm install -g create-react-app

# react app 생성
> create-react-app reactapp
```

## 2. express.js 설치
```powershell
# 프로젝트 initialize하고 package.json 생성
> npm init

# express 모듈 설치
> npm install express.js

# body-parser 모듈 설치
> npm install -g body-parser

# nodemon 모듈 설치
> npm install -g nodemon

# cors 모듈 설치
> npm install cors
```

## 3. React app 수정
```js
import React from 'react';
import './App.css';

class App extends React.Component {

  constructor(props){
    super(props);
    this.state = {
      username:null
    }
  }

  componentDidMount(){
    fetch('http://localhost:3001/api')
      .then(res => res.json())
      .then(data => this.setState({username: data.username}))
  }

  render(){
    return (
      <div className="App">
        <header className="App-header">
          {this.state.username ? `Hello ${this.state.username}` : 'Hello World'}
        </header>
      </div>
    );
  }
}

export default App;

```

## 4. Server 실행
```js
// server/server.js
const express = require('express');
const bodyParser = require('body-parser');
const cors = require('cors');
const app = express();
app.use(bodyParser.json())
app.use(cors());

app.get('/api', (req, res) => {
    res.json(
        {
            username: "Kim"
        }
    );
})

app.listen(3001, () => {
    console.log('express is running on 3001');
})
```

```powershell
# 터미널에서 서버 실행
> node server.js
```