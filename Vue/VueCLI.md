# Vue CLI
- 빠른 `Vue.js` 개발을 위해 프로젝트의 구성을 도와주는 모듈

## CLI
- vue create : `Vue.js` 프로젝트를 생성
- vue ui : `UI`를 통해 프로젝트를 관리하는 

## CLI Service
- `webpack`, `webpack-dev-server` 위에 구축이 되며 `CLI Plugin`을 실행하는 핵심 서비스와 `web pack`에 대한 설정을 포함
- `webpack`을 통해 애플리케이션의 개발 서버 실행, 빌드 등을 처리

## CLI Plugin
- `Bable/Typescript`, `ESLint`, `e2e Test` 등과 같은 선택적으로 설치가 필요한 Plugin

## 사용법

### 설치
```bash
$ npm i -g @vue/cli
```

### 프로젝트 생성
```bash
$ vue create <project-name>
```

#### features
- Babel : `ES6` 이상 버전이나 `Typescript`로 코딩한 경우 범용적인 `ES5`로 자동 전환해줌
- Typescript : `JS`에 정적 타입을 도입한 언어
- PWA Support : 웹앱을 만들때 사용
- Router : `Vue`에서 화면 이동을 구현하기 위한 플러그인
- Vuex : `Vue`에서 데이터를 쉽게 공유해서 대규모 `Vue` 개발을 편리하게해줌
- CSS Pre-processors : `SASS`, `LESS` 등 지원
- Linter / Formatter
- Unit Testing : 단위 테스트
- E2E Testing : 통합 테스트

### 프로젝트 실행
```bash
$ npm run serve
```