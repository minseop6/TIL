# Process와 Thread
## 프로세스
- 메모리에 적재되어 실행되고 있는 프로그램
- 각각 별도의 독립적인 주소공간을 할당
    - Code : 코드 자체를 구성하는 메모리 영역
    - Data : 전역 변수, 정적 변수, 배열 등
    - Heap : 동적 할당시 사용
    - Stack : 지역 변수, 매개 변수, 리턴 값
## 스레드
- 프로세스 안에서 실행되는 여러 흐름 단위
- 프로세스가 할당받은 자원을 이용
- 다른 스레드와 공간, 자원을 공유

## PCB
- Process Controll Block의 약어로 프로세스 제어 블록
- 프로세스에 대한 중요한 정보를 저장하고 있음
- 프로세스 생성시에 만들어지며 주기억장치에 유지됨
- 컨텍스트 전환시에 다른 프로세스를 처리해야할 경우 PCB에 현재 상태를 저장함으로써 나중에 작업 상태를 불러와 작업 재개가 가능
- PID, 상태, Program Counter 등의 정보가 저장됨

## PC
- Program Counter의 약어로 다음에 실행될 명령어의 주소가 들어있는 레지스터
- 명령어가 인출되면 자동으로 다음 명령어를 가리카도록 주소값이 증가됨

## 멀티 프로세스
- 하나의 컴퓨터에 여러 CPU를 장착해서 하나 이상의 프로세스들을 병렬로 동시에 처리
- 장점 : 안정성(메모리 침범 문제를 OS에서 해결)
- 단점 : 각각 독립적인 메모리 영역을 갖고있어 작업량이 많을 수록  `Context Switching` 으로 인한 오버헤드 발생

## 멀티 스레드
- 하나의 응용 프로그램에서 여러 스레드를 구성해 각 스레드가 하나의 작업을 처리
- 스레드들이 공유 메모리를 통해 다수의 작업을 동시에 처리
- 장점
    - 독립적인 프로세스에 비해 공유 메모리만큼의 시간, 자원 손실이 감소
- 단점
    - 힙 영역을 공유때문에 자원을 사용할 때 동기화 해주어야함
    - 동기화를 위해 과도한 락 사용시 병목 현상으로 인해 성능 저하

## 프로세스(스레드) 동기화
- ### 경쟁 상태(Race Condition)
    - 두 개 이상의 프로세스나 스레드가 공유 자원을 동시에 사용할 때 그 순서에 따라 결과가 달라지는 문제
- ### 임계 영역
    - 동기화 방법중 하나로 프로세스간 자원이 공유될 수 있는 코드 블록
    - 조건
        - 상호 배제(Mutual Exclusion) : 프로세스가 임계 영역에 들어가 있다면 다른 프로세스는 임계 영역에 들어갈 수 없음
        - 진행(Progress) : 임계 영역에 들어가 있는 프로세스가 없다면 다른 후보 프로세스가 진입 할 수 있음
        - 한정된 대기(Bounded Waiting) : 프로세스가 진입 가능한 횟수에는 제한이 있음(특정 프로세스만 계속 진입하는 것을 방지)
- ### Lock
    - 하드웨어 기반 처리로 임계 영역에 진입하기 위해서는 Lock이 필요
    - 임계 영역에 진입하는 프로세스는 Lock을 흭득하고 빠져나올 때 Lock을 반납