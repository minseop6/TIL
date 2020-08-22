# Passport.js
- `Node.js`에서 사용하는 인증관련 미들웨어
- 로그인, 접근 권한 등을 인터셉트해서 권한을 체크
- `Express`, `Express-session` 미들웨어와 연동 가능하여 유연한 기능 제공
- 인증을 위한 다양한 `Strategy` 제공(e.g. Facebook. Google ...)

## passport.js 적용
### 1. 모듈 설치
```bash
$ npm i passport passport-local -D
```

### 2. passport 미들웨어 설정
```js
// app.js
import express from 'express';
import bodyParser from 'body-parser';
import session from 'express-session';
import passport from 'passport';
import Passport from './config/passport';
import path from 'path';

class App {
    public app: express.Applicaition = new express();
    public passportConfig: Passport = new Passport();

    constructor(controllers, public port: number) {
        this.initMiddlewares();
        this.initRouters(controllers);
    }

    private initRouters(controllers: any) {
        controllers.map((controller) => {
            this.app.use(controller.url, controller.object.router);
        })
    }

    private initMiddlewares() {
        this.app.use(bodyParser.json());
        this.app.use(bodyParser.urlencoded({ extended : false }));
        this.app.use(session({
            secret:`@#@$MYSIGN#@$#$`,
            resave: false,
            saveUninitialized: true 
        }))
        this.app.use(passport.initialize());
        this.app.use(passport.session());
        this.passportConfig.config();
    }

    public listen(server) {
        server.listen(this.port, () => {
            console.log(`Server is running on ${this.port}`);
        })
    }
}

export default App;
```

### 3. Strategy 정의
```js
// passport.ts
import passport from 'passport';
import passportLocal from 'passport-local';
import User from '../Models/UserModel';

const LocalStrategy = passportLocal.Strategy;

class Passport {
    public config = () => {
        // Local Strategy
        passport.use(new LocalStrategy({
            usernameField: 'id',
            passwordField: 'pw'
        },
        (id, pw, done) => {
            return User.findOne({
                where: {
                    id: id,
                    pw: pw
                }
            })
            .then(user => {
                if(!user) {
                    return done(null, false, { message: 'Incorrect ID or PW' })
                }
    
                return done(null, user, { message: 'Login Success' });
            })
            .catch(err => done(err));
        }))

        passport.serializeUser<any, any>((user, done) => {
            done(null, user);
        });
         
        passport.deserializeUser(function(user, done) {
            done(null, user);
        });
    }
    
    public isAuthenticated = (req, res, next) => {
        if (req.isAuthenticated()) {
            return next();
        }
        res.redirect("/");
    };
}

export default Passport;
```

#### serializeUser
- 로그인에 성공하면 `serializeUser` 메서드를 통해 사용자 정보를 `Session`에 저장

#### deserializeUser
- 요청을 받으면 호출되어 `Session`에 저장된 사용자 정보를 불러옴
- `req.user`에 사용자 정보를 저장

#### isAuthenticated
- 로그인 여부를 확인하는 Function

### 4. 인증 구현
```js
// UserController.ts
import express from 'express';
import passport from 'passport';
import Passport from '../config/passport';

class UserController {
    public router = express.Router();
    public passport: Pssport = new Pasport();
    constructor() {
        this.initRouters();
    }

    private initRouters() {
        this.router.post('/login', passport.authenticate('local', {
            successRedirect: '/rooms',
            failureRedirect: '/'
        }))
        this.router.get('/rooms', this.passport.isAuthenticated, this.renderRooms);
    }

    renderRoom = (req: express.Request, res: express.Response) => {
        console.log(req.user); // Session에 저장된 사용자 정보 출력

        res.render('rooms');
    }
}

export default UserController;
```
