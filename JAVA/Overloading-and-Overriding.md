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
- ex)

```java
public abstract class Parent{
  public void test() {
    System.out.println("Parent Class");
  }
}

public class Child extends Parent {
  @Override
  public void test(){
    System.out.println("Child Class");
  }
}

public class Main{
  public static void main(String[] args) {
    Parent parent = new Parent();
    Child child = new Child();

    parent.test(); //result : Parent Class
    child.test(); //result : Child Class
  }
}
```
