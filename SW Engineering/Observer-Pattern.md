# Observer Pattern
- 어떤 객체에 이벤트가 발생했을 때, 이 객체와 관련된 객체들(옵저버)에게 통지하는 패턴
- 데이터의 변경이 발생했을 경우 상대 클래스나 객체에 의존하지 않으면서 데이터 변경을 통보할 때 사용
- 통보 대상 객체의 관리를 `Subject`클래스와 `Observer`인터페이스로 일반화함
    - 데이터 변경을 통보하는 클래스(ConcreteSubject)는 통보 대상 클래스나 객체(ConcreteObserver)에 대한 의존성을 없앨 수 있음
    - 결과적으로 옵서버 패턴은 통보 대상 클래스나 대상 객체(ConcreteObserver)의 변경에도 `ConcreteSubject` 클래스를 수정 없이 그대로 사용할 수 있음

## 역할이 수행하는 작업
- ### Observer
    - 데이터의 변경을 통보 받는 인터페이스
    - `Subject`에서는 `Observer` 인터페이스의 `update` 메서드를 호출함으로써 `ConcreteSubject`의 데이터 변경을 `ConcreteObserver`에게 통보
- ### Subject
    - `ConcreteObserver` 객체를 관리하는 클래스
    - `Observer` 인터페이스를 참조해서 `ConcreteObserver`를 관리하므로 `ConcreteObserver`의 변화에 독립적임
- ### ConcreteSubject
    - 변경 관리 대상이 되는 데이터가 있는 클래스
    - 데이터 변경을 위한 `setState` 메서드가 있으며 `setState`에서는 자신의 데이터인 `subjectState`를 변경함
    - `Subject`클래스에게서 상속받은 `notifyObservers` 메서드를 호출해서 `ConcreteObserver` 객체에 변경을 통보
- ### ConcreteObserver
    - `ConcreteSubject`의 변경을 통보 받는 클래스
    - `Observer` 인터페이스의 `update` 메서드를 구현함으로써 변경을 통보 받음
    - 변경된 데이터는 `ConcreteSubject`의 `getState` 메서드를 호출함으로써 변경된 데이터를 조회