# Socket.io
## Socket.io란?
- 클라이언트와 서버의 양방향 통신을 가능하게 해주는 모듈
- `WebSocket`과 다르게 브라우저에 websocket, pooling, straming, flash socket 등 적절한 방법을 찾아 메시지를 보내줌

## 모듈 설치
```powershell
# socket.io 설치
> npm install socket.io

# redis 모듈 설치
> npm install socket.io-redis
```

## 초기 설정
```js
const express = require('express');
const http = require('http');
const socket = require('socket.io');
const bodyParser = require('body-parser');
const fs = require('fs');
const cors = require('cors');

const app = express();
const server = http.createServer(app);
const io = socket(server);
app.use(bodyParser.json())
app.use('/css', express.static('./static/css'));
app.use('/js', express.static('./static/js'));

app.get('/', (req, res) => {
    fs.readFile('./static/index.html', (err, data) => {
        if(err){
            res.send('error');
        }else{
            res.writeHead(200, {'Content-Type':'text/html'});
            res.write(data);
            res.end()
        }
    })
})

server.listen(3001, () => {
    console.log('express is running on 3001');
})
```

#### 디렉토리 생성
1. 루트에 static 생성
2. static 폴더에 index.html 생성
3. static 폴더에 css, js 폴더 생성

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chat</title>
    <link rel="stylesheet" href="/css/index.css">
</head>
<body>
    <div id="main">
        Welcome
    </div>
</body>
</html>
```

```css
/* index.css */
#main{
    margin: auto;
    margin-top: 100px;
    background-color: dimgrey;
    text-align: center;
    width: 200px;
}
```

## Socket.io 사용법
- on()은 해당 소켓에서 이벤트를 받으면 콜백함수를 실행
- `on`은 수신 `emit`은 전송
    - io.sockets.emit() : 모든 유저(본인 포함)
    - socket.broadcast.emit() : 본인을 제외한 모든 유저
- `disconnect`는 `socket.io`의 기본 이벤트로 연결되어 있던 소켓의 접속이 끊기면 자동 실행
```js
// server/server.js 에 추가
io.sockets.on('connect', (socket) => {

    var roomName = 1;

    socket.on('message', (data) => {
        data.name = socket.name;
        console.log(data);
        io.sockets.in(roomName).emit('update', data);
    })

    socket.on('joinRoom', (num, name) => {
        roomName = num;
        console.log(`${name} is join ${num}`);
        socket.join(num);
    });

    socket.on('disconnect', () => {
        console.log(`${socket.name} is disconnected`);
        socket.broadcast.emit('update', {
            type: 'disconnect',
            name: 'SERVER',
            message: `${socket.name} is disconnected`
        });
    })
})
```

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chat</title>
</head>
<body>
    <div id="main">
        <button onclick="ns(1)">Namespace1</button>
        <button onclick="ns(2)">Namespace2</button>
        <input type="text" id="message" />
        <button onclick="send()">SEND</button>
        <textarea id="content" cols="30" rows="10"></textarea>
    </div>
</body>
</html>
<link rel="stylesheet" href="/css/index.css">
<script src="../socket.io/socket.io.js"></script>
<script src="/js/index.js"></script>
```

```js
// index.js
const socket = io()
var name = 'anonymous';
// Connect 이벤트
socket.on('connect', () => {
    name = prompt("What's your name?");
    let room = ['room1', 'room2'];
    let num = 0;
    
    socket.emit('joinRoom', num, name);
})

socket.on('update', (data) => {
    var str = `${data}\n`;
    document.querySelector('#content').value += str;
})


// send 함수
const send = () => {
    var message = document.querySelector('#message').value
    document.querySelector('#message').value = '';
    socket.emit('message', {message: message}) //전송
}

//room 선택 함수
const ns = (num) => {
    document.querySelector('#content').value = '';
    socket.emit('joinRoom', num, name);
}
```