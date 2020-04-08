# Overloading and Overriding
------------
## Overloading
- 두 메소드가 같은 이름을 갖고 있지만 인자의 수나 자료형이 다른 경우
- 조건
 - 메소드 이름이 같아야함
 - 리턴형이 같아도 되고 달라도됨
 - 파라미터 개수가 달라야함
 - 파라미터 개수가 같을 경우 데이터 타입이 달라야함
- ex)

```java
public void test(int a) {...}
public void test(int a, int b) {...}
public void test(String a) {...}
```

## Overriding
- 상위 클래스의 메소드와 이름이 같은 함수를 하위 클래스에 재정의
- 조건
 - 오버라이드 하고자 하는 메소드가 상위 클래스에 존재해야함
 - 메소드 이름이 같아야함
 - 메소드 파라미터 개수, 파라미터 자료형이 같아야함
 - 메소드 리턴형이 같아야함
 - 상위 메소드와 동일하거나 내용이 추가되어야함
 - `static` 메소드는 상속되지 않음
    - `static` 메소드는 클래스 단위로 만들어지기 때문에 객체 단위로 형성되는 `Override`는 성립될 수 없음
    - `static` 메소드는 클래스가 컴파일 되는 시점에 결정
    - `Override` 메소드는 런타임 시점에 사용될 메소드가 결정
- ex)

```java
public abstract class Parent{
  public void test1() {
    System.out.println("Parent Class test1");
  }

  public static void test2() {
    System.out.println("Parent Class test2");
  }
}

public class Child extends Parent {
  @Override
  public void test1(){
    System.out.println("Child Class test1");
  }

  public static void test2() {
    System.out.println("Child Class test2");
  }
}

public class Main{
  public static void main(String[] args) {
    Parent parent = new Parent();
    Parent child = new Child();

    parent.test1(); //result : Parent Class test1
    child.test1(); //result : Child Class test1
    parent.test2(); //result : Parent Class test1
    child.test2(); //result : Parent Class test1
  }
}
```
