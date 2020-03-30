# Overloading and Overriding
------------
## Overloading
- 두 메소드가 같은 이름을 갖고 있지만 인자의 수나 자료형이 다른 경우
- ex)

```java
public void test(int a) {...}
public void test(int a, int b) {...}
public void test(String a) {...}
```

## Overriding
- 상위 클래스의 메소드와 이름이 같은 함수를 하위 클래스에 재정의
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
