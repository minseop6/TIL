# Multer
- `Multer`는 `multipart/form-data`를 다루기 위한 `node.js` 미들웨어
- 파일 업로드를 위해 사용되는 모듈

## 사용법

### 모듈 설치
```console
> npm install multer
```

### Client
```html
<body>
    <form action="upload" method="POST" enctype="multipart/form-data">
        <input type="file" name="uploadFile" />
        <button type="submit">UPLOAD</button>
    </form>
</body>
```

### Server
- 사용자가 post로 전송한 데이터가 'upload'폴더로 저장된다면 함수를 실행하여 컨트롤러로 연결
- 미들웨어가 사용자가 전송한 데이터 중에 파일이 포함되어 있으면 파일을 가공해서 `req`객체에 `file`이라는 `property`를 암시적으로 추가해줌
- upload.single()함수의 인자는 form을 통해 전송되는 파일의 `name`속성과 동일해야함

```js
...

app.use('/file', express.static('upload')); // /file 경로를 통해 upload 디렉토리에 저장된 파일을 로드할 수 있음
// ex) http://localhost:3000/file/example.ppt
const multer = require('multer');
const storage = multer.diskStroage({
    destination: (req, file, cb) => {
        cb(null, 'upload/'); // 콜백 함수를 통해 전송된 파일이 저장될 디렉토리 설정
    },
    filename: (req, file, cb) => {
        cb(null, file.originalname) // 콜백 함수를 통해 전송된 파일 이름 설정
    }
})
var upload = multer({storage: storage});

app.post('/upload', upload.single('file'), (req, res) => {
    res.send('upload success');
})

app.get('/download', (req, res) => {

    var file = `파일 경로`;
    var originalName = `원본 파일 이름`;
    
    res.setHeader('Content-disposition', 
                  `attachment; filename=${encodeURI(originalName)}`);
    res.setHeader(`Content-type`, "binary/octet-stream")
    var filestream = fs.createReadStream(file);
    filestream.pipe(res);
})
```

참고

[https://github.com/expressjs/multer](https://github.com/expressjs/multer)