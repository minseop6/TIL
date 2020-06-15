# Abstract Factory Pattern
- 관련성 있는 여러 종류의 객체를 일관된 방식으로 생성하는 패턴

## 팩토리 메서드와의 차이점
- ### Factory 클래스에서 객체에 대한 생성을 지원하는 범위
    #### 팩토리 메서드 패턴
        - 한 팩토리당 한 종류의 객체 생성 가능
    #### 추상 팩토리 패턴
        - 한 팩토리에서 서로 연관된 여러 종류의 객체 생성 가능
- ### 팩토리 메서드에서 만드는 객체의 종류
    #### 팩토리 메서드 패턴
        - 인자에 따라 객체의 종류가 결정
    #### 추상 팩토리 패턴
        - 인자에 따라 관련된 객체들을 생성하는 팩토리의 종류가 결정
- ### 결합도를 낮추는 대상
    #### 팩토리 메서드 패턴
        - ConcreteProduct와 Client간의 결합도를 낮춤
    #### 추상 팩토리 패턴
        - ConcreteFactory와 Client간의 결합도를 낮춤

## 역할이 수행하는 작업
- ### AbstractFactory
    - 실제 팩토리 클래스의 공통 인터페이스
    - 각 Product의 객체를 생성하는 기능을 추상 메서드로 정의
- ### ConcreteFactory
    - 구체적인 팩토리 클래스
    - AbstractFactory 클래스의 추상 메서드를 오버라이드함으로써 구체적인 Product 객체 생성
- ### AbstractProduct
    - Product의 공통 인터페이스
- ### ConcreteProduct
    - 구체적인 팩토리 클래스에서 생성되는 구체적인 Product