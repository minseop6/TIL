# Stack and Queue
## 스택(Stack)이란?
- 한 쪽 끝에서 데이터를 넣고 뺄 수 있는 `LIFO(Last In Fisrt Out)` 형식의 선형 자료구조
- 스택은 가장 최근에 스택에 추가한 데이터가 가장 먼저 제거됨
    - push() : 스택에 데이터를 저장
    - pop() : 스택에서 데이터를 꺼냄
    - peek() : 스택에서 가장 최근에 추가한 데이터를 반환
    - isEmpty() : 스택이 비어 있을 때 `true` 반환

## 활용 방안
- 재귀 알고리즘
    - 재귀적으로 함수를 호출해야 하는 경우에 임시 데이터를 스택에 넣어줌
    - 재귀함수를 빠져 나와 `backtracking`을 할 때는 스택에 넣어 두었던 임시 데이터를 가져옴
- 웹 브라우저 방문 기록
- 실행 취소
- 역순 문자열 만들기
- 수식의 괄호 검사
- 후위 표기법 계산

## 큐(Queue)란?
- 먼저 넣은 데이터가 먼저 나오는 `FIFO(First In First Out)` 형식의 선형 자료구조
- 큐는 가장 늦게 큐에 추가한 데이터가 가장 먼저 제거됨
    - add() : 큐의 가장 끝에 데이터를 추가
    - remove() : 큐의 첫 번째 항목을 제거
    - peek() : 큐의 첫 번째 항목을 반환
    - isEmpty() : 큐가 비어있을 때 `true` 반환

## 활용 방안
- 데이터가 입력된 시간 순서대로 처리해야할 때 사용
- `BFS(Breadth First Search)`
    - 노드를 처리할 때 마다 해당 노드와 인접한 노드들을 큐에 저장
- 캐시(Cache) 구현
- 우선순위가 같은 작업 예약
- 선입선출이 필요한 대기열
- 윈도우 시스템의 메시지 처리기
- 프로세스 관리