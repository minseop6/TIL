# Nginx
- 트래픽이 많은 웹사이트의 확장성을 위해 설계된 `Event Driven` 구조의 경량 웹서버
- 클라이언트의 요청을 받았을 때 요청에 맞는 정적 파일을 응답해주는 `HTTP Web Server`로 사용
- `WAS`의 부하를 줄일 수 있는 로드 밸런서로 사용

## Apache와의 차이점
### Apache
- 쓰레드 / 프로세스 구조로 `request` 1개를 쓰레드 1개가 처리하는 구조
- 사용자가 많으면 많은 쓰레드가 생성됨 (메모리, CPU 낭비가 큼)
- 쓰레드 1개 = 클라이언트 1개

### Nginx
- `Event Driven` 구조
- 한 개 또는 고정된 프로세스만 생성해서 사용 (새로운 요청이 들어와도 새로운 프로세스와 쓰레드를 생성하지 않음)
- 비동기 방식으로 `request`를 `Concurrency`하게 처리할 수 있음
- 즉 적은 자원으로 효율적인 운용을 할 수 있음

## Nginx의 구조
- 하나의 Master Process와 다수의 Worker Process로 구성됨
- Master Process는 설정 파일을 읽고 유효성 검사 및 Worker Process를 관리
- 모든 요청은 Worker Process에서 처리함
- Nginx는 이벤트 기반 모델을 사용하고 Worker Process 사이에 요청을 효율적으로 분배하기 위해 OS에 의존적인 메커니즘을 사용함
- Worker Process의 개수는 설정 파일에서 정의되고 정의된 프로세스 개수와 사용 가능한 CPU 코어 개수에 맞게 자동으로 조정됨
