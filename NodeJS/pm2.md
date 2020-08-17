# pm2
## pm2란?
- Process Manager의 약어
- Node.js의 프로세스를 관리해주는 역할
- 생산 프로세스 관리자로 서버 인스턴스들에 대한 로드 밸런싱과 Node.js의 `Scale Up` 또는 `Scale Down`을 도움
- 프로세스들이 계속 실행할 수 있는 환경을 제공
- 처리하지 못한 예외에 의해 스레드가 죽음으로 인해 애플리케이션이 죽는 현상을 방지

## 사용법
1. pm2 -version
    - Version 확인 명령어
2. pm2 start example.js
    - pm2를 실행하는 명령어로 서버 소스코드가 작성되어 있는 js파일을 실행
    - options
        - --watch : pm2가 실행된 프로젝트의 변경사항을 감지하여 서버를 자동 리로드 해줌
        - -i max(코어 개수) : Node.js의 싱글 스레드를 보완하기 위한 `Cluster` 모드
3. pm2 kill
    - 실행 중인 pm2 Daemon을 종료시킴
4. pm2 list
    - pm2에 등록된 관리 리스트 조회
5. pm2 log
    - 실행 중인 pm2 Daemon의 log를 확인
6. pm2 monit
    - pm2로 실행한 서버의 상황을 모니터링