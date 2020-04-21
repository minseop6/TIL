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

### Set 인터페이스
- 데이터의 저장 순서를 유지하지 않음
- 같은 데이터의 중복저장을 허용하지 않음(null도 하나만 허용)
- 인덱스로 객체에 접근할 수 없음
- 반복자(Iterator)를 이용해서 객체에 접근

#### 1. HashSet
- 순서가 필요없는 데이터를 hash table에 저장
- Set중에 가장 성능이 좋음
```java
public class Example {
    	HashSet<String> ex = new HashSet<String>();
	    ex.add("a");
	    ex.add("b");
	    ex.add("c");
	    ex.add("a");
	    
	    Iterator it = ex.iterator();
	    while(it.hasNext()) {
	    	System.out.print(it.next() + " "); // result: a b c
	    }
}
```
#### 2. TreeSet
- 저장된 데이터의 값에 따라 정렬됨
- HashSet보다 성능이 느림

#### 3. LinkedHashSet
- 연결된 목록 타입으로 구현된 hash table에 데이터 저장
- 저장된 순서에 따라 값이 정렬되나 가장 느림

### Map 인터페이스
- `key`와 `value`로 구성된 `Entity` 객체를 저장하는 구조
- `value`는 중복저장이 가능하지만 `key`는 중복저장이 불가능
- 중복된 `key` 로 저장 시 기존 `value`는 새로운 `value`로 대체됨

#### 1. HashMap
- 해시테이블을 사용한 클래스
- 중복을 허용하지 않고 순서를 보장하지 않음
- `key`와 `value`로 null을 허용

```java
public class example{
	Map<String, Integer> hashMap = new HashMap<String, Integer>();

    hashMap.put("Key1", 1);
	hashMap.put("Key2", 2);
    hashMap.put("Key3", 3);
    hashMap.put("Key4", 4);
    hashMap.put("Key5", 5);

    // 방법1
    Iterator<String> keys = hashMap.keySet().iterator();
    while (keys.hasNext()){
        String key = keys.next();
        System.out.println("KEY : " + key); // Key2 , Key1, Key4, Key3, Key5
    }

    // 방법2
    Set set = hashMap.keySet();
    Iterator iterator = set.iterator();
    while(iterator.hasNext()){
        String key = (String) iterator.next();
        System.out.println("KEY : " + key); // Key2 , Key1, Key5, Key4, Key3
    }

    // 방법3
    Set set2 = hashMap.entrySet();
    Iterator iterator2 = set2.iterator();
    while(iterator2.hasNext()){
        Entry<String,Integer> entry = (Entry)iterator2.next();
        String key = (String)entry.getKey();
        int value = (Integer)entry.getValue();
        System.out.println("hashMap Key : " + key);
        System.out.println("hashMap Value : " + value);
    }
}