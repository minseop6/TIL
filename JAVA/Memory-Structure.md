# Memory Structure
----------
## JVM 구조
- 실행될 클래스 파일을 메모리에 로드 후 초기화 작업 수행
- 메소드와 클래스 변수들을 해당 메모리 영역에 배치
- 클래스 로드가 끝난 후 JVM은 main메소드를 찾아 지역변수, 객체변수, 참조변수를 스택에 쌓음
- JVM은 4가지로 나뉘어짐
  - Class Loader : 클래스 파일들을 묶어서 운영체제로부터 할당받은 메모리 영역인 Runtime Data Area로 적재하는 역할
  - Execution Engine : Class Loader에 의해 메모리에 적재된 클래스들을 기계어로 변경해 명령어 단위로 실행하는 역할
  - Garbage Collector : Heap 메모리 영역에 적재된 객체들 중에 참조되지 않는 객체들을 탐색 후 제거하는 역할
  - Runtime Data Area : JVM의 메모리 영역으로 자바 어플리케이션을 실행할 때 사용되는 데이터들을 적재하는 영역
    1. Method adrea
      - 필드 정보, 메소드 정보, 상수 풀, static 변수 등이 생성되는 영역
    2. Heap area
      - new 키워드로 생성된 객체와 배열이 생성되는 영역
      - 메소드 영역에 로드된 클래스만 생성이 가능하고 Garbage Collector가 참조되지 않는 메모리를 확인하고 제거하는 영역
    3. Stack area
      - 지역 변수, 파라미터, 리턴 값, 연산에 사용되는 임시 값 등이 생성되는 영역
      - 메소드를 호출할 때마다 개별적으로 스택이 생성됨
    4. PC Register
      - Thread가 생성될 때마다 생성되는 영역
      - Program Counter 즉, 현재 쓰레드가 실행되는 부분의 주소와 명령을 저장하고 있는 영역
      - 이것을 이용하여 Thread를 돌아가면수 수행할 수 있게함

    5. Native method stack
      - 자바 외 언어로 작성된 네이티브 코드를 위한 메모리 영역
      
