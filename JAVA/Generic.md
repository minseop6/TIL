# Generic
--------------
## Generic 이란?
- 클래스 내부에서 사용하는 데이터의 타입을 클래스의 인스턴스를 생성할 때 결정하는 것을 의미
- 객체의 타입을 컴파일 시점에 체크하기 때문에 안정성이 높고 형변환의 번거러움을 줄일 수 있음

## 제네릭 특징

#### 객체 생성이 가능한 타입에 대해서만 제네릭 사용 가능
- 기본 데이터 타입(int, long ...)에 대해서는 지정이 불가능
- 기본 타입을 객체 타입으로 사용하는 `Wrapper`클래스(Integer, Boolean...)는 제네릭 사용 가능

#### 제네릭 파라미터

```java
public class SmapleGeneric<T> {

  public T sample;

  ...
}

public class Main{
  public static void main(String[] args){

    SampleGeneric<String> strSample = new SampleGeneric<String>();
    SampleGeneric<Integer> intSample = new SampleGeneric<Integer>();

    strSample.sample = "Sample";
    intSample.sample = 123;

    System.out.println(strSample.sample.getClass()); //java.lang.String
    System.out.println(intSample.sample.getClass()); //java.lang.Integer
  }
}
```

#### 멀티 타입 파라미터

```java
public class SampleGeneric<T, K> {

  public T sample1;
  public K sample2;

  ...
}

public class Main{
  public static void main(String[] args){

    SampleGeneric<String, Integer> genericSample = new SampleGeneric<String, Integer>();

    genericSample.sample1 = "Sample";
    genericSample.sample2 = 123;

    System.out.println(genericSample.sample1.getClass()); //java.lang.String
    System.out.println(genericSample.sample2.getClass()); //java.lang.Integer
  }
}
```
#### 제네릭 생략

```java
public class SmapleGeneric<T> {

  public T sample;

  ...
}

public class Main{
  public static void main(String[] args){

    SampleGeneric genericSample = new SampleGeneric();
    genericSample.sample = "Sample";

    System.out.println(genericSample.sample1.getClass()); //java.lang.String
  }
}
```


#### 제네릭 메소드

```java
public <T> Sample<T> methodSample(T t){
  ...
}

Sample<Integer> <Integer>methodSample(10); //명시적으로 Integer 지정
Sample<Integer> methodSample(10); // 컴파일러가 매개 값을 보고 타입 결정
```

#### 타입 매개변수 제한

```java
public class SmapleGeneric<T extends String> {

  public T sample;

  ...
}

public class Main{
  public static void main(String[] args){

    SampleGeneric<String> genericSample = new SampleGeneric<String>();
    SampleGeneric<Integer> genericSample = new SampleGeneric<Integer>(); //컴파일 오류
  }
}
```
