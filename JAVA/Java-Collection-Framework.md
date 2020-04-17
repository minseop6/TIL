# Java Collection Framework
## Java Collection Framework란?
- 다수의 데이터를 쉽고 효과적으로 처리할 수 있는 표준화된 방법을 제공하는 클래스의 집합
- 데이터를 저장하는 자료구조와 데이터를 처리하는 알고리즘을 구조화하여 클래스로 구현한 것

## Java Collection Framework의 인터페이스
### List 인터페이스
- 동일한 데이터의 중복 허용
- 데이터 저장 순서가 유지됨
- 힙 영역내에서 List는 객체를 일렬로 늘어놓은 구조
- 객체를 인덱스로 관리

1. #### ArrayList
- List 인터페이스의 구현 클래스로 객체는 인덱스로 관리됨
- 고정된 배열과 다르게 크기가 동적으로 변경됨
```java
public class Example {

    List<String> list = new ArrayList<String>();
    list.add("A");
    list.add("B");
    list.add("C");

    for(String item : list) {
	    System.out.print(item + " "); //result: A B C
	}

    list.set(1, "Change");
	    
	for(int i=0; i<list.size(); i++) {
	   	System.out.print(list.get(i) + " "); //result: A Change C
	}
}
```

#### 2. Vector
- 고정된 배열과 다르게 크기가 동적으로 변함
- 사용방법 동일

#### 3. LinkedList
- `ArrayList`와 메서드는 동일하지만 내부 구조는 다름
- `ArrayList`는 내부 배열 객체를 저장해서 인덱스를 관리하지만 `LinkedList`는 양방향 포인터 구조로 인접하는 참조를 링크해서 체인처럼 관리
- 사용방법 동일