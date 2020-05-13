# Lambda Expression
## 람다식이란?
- 함수적 프로그래밍을 위해 JAVA8 에서 추가된 기능으로 `익명객체`를 생성하기 위한 표현식
- 쉽게말해 함수인데 함수를 따로 만들지 않고 코드한줄에 함수를 써서 그것을 호출하는 방식

### - 람다식 이전
- 기존 자바에서는 다형성을 제공하기 위해 `interface`를 만들고 그것을 구현한 `class`를 만들어 `interface`참조 변수에 `interface`를 구현한 `class`객체를 생성해 사용함
 
```java
public interface ExampleInterface {
    public void ex();
}

public class Example implements ExampleInterface {
    @Override
    public void ex(){
        System.out.println("Example");
    }
}

public class Main{
    public static void main(String[] args) {
        ExampleInterface example = new Example();
        example.ex(); // result : Example
    }
}
```

### - 람다식 사용
- 람다식을 사용할 경우 좀 더 간결해짐
- `interface`를 생성한 후 `interface`참조 변수에 람다식을 대입해서 사용함
```java
public class Main{
    public static void main(String[] args) {
       ExampleInterface example = () -> System.out.println("Lambda Example"); // result : Lambda Example
       example.ex();
    }
}
```

## 장단점
### 장점
- 코드를 간결하게 만들 수 있음
- 코드가 간결하고 식에 개발자의 의도가 명확히 드러나므로 가독성이 향상
- 함수를 만드는 과정이 없어짐으로 코딩하는 시간이 단축
- 병렬프로그래밍이 용이

### 단점
- 람다를 사용하면서 만드는 익명함수는 재사용 불가
- 디버깅이 까다로움
- 람다를 남발하면 비슷한 함수를 중복생성할 가능성이 높음
- 재귀로 만들기에는 부적합함

## 사용법
- 람다식은 `매개변수 + 실행문` 으로 구성됨
- 즉 `접근자`, `반환형` 모두 생략되는 구조
- `() -> {}` 의 형태
- `()`에 해당 `interface`함수의 매개변수를 입력
- `{}`에 실행할 코드 작성

### 1. 기본 사용법
```java
public interface Calculator {
    public int op(int num1, int num2);
}

public class Main {
	public static void main(String[] args) {
		
		Calculator cal = (int num1, int num2) -> {return num1 + num2;};
		System.out.println(cal.op(1, 2));
	}
}
```

### 2. 매개변수 타입 생략
- 매개변수가 1개이거나 2개 이상의 매개변수의 타입이 모두 같을 때 타입 생략 가능
```java
public interface Calculator {
    public int op(int num1, int num2);
}

public class Main {
	public static void main(String[] args) {
		
		Calculator cal = (num1, num2) -> {return num1 + num2;};
		System.out.println(cal.op(1, 2));
	}
}
```

### 3. 매개변수가 없는 경우
- `interface`의 메소드에 매개변수가 없는 경우에 매개변수 생략 가능
```java
interface Calculator {
    public String op();
}

public class Main {
	public static void main(String[] args) {
		
		Calculator cal = () -> {return "매개변수가 없습니다";};
		System.out.println(cal.op());
	}
}
```

### 4. 중괄호 생략
- 실행할 문장이 1개일 경우에 중괄호 생략 가능
```java
interface Calculator {
    public int op(int num1, int num2);
}

public class Main {
	public static void main(String[] args) {
		
		Calculator cal = (num1, num2) -> num1 + num2;
		System.out.println(cal.op(1, 2));
	}
}
```

### 5. 소괄호, 중괄호 생략
- 매개변수가 1개이고 실행할 문장도 1개일 경우 소괄호와 중괄호 생략 가능
```java
interface Calculator {
    public int op(int num1);
}

public class Main {
	public static void main(String[] args) {
		
		Calculator cal = num1 -> num1;
		System.out.println(cal.op(3));
	}
}
```

## 사용 조건
- 구현해야할 인터페이스에 조건이 있음
- 인터페이스의 추상 메소드가 1개이어야함
- 이를 컴파일 타임에서 에러를 잡기위해 `interface`에 `@FunctionalInterface` 어노테이션을 사용