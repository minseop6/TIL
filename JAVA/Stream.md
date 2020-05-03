# Stream
## Stream이란?
- Java8에서 추가된 것으로 람다를 활용할 수 있는 기술 중 하나
- 배열 또는 컬렉션등의 저장요소를 하나씩 참조해 람다식을 적용하여 반복적으로 처리할 수 있음
- 즉, 배열과 컬렉션을 함수형으로 처리할 수 있음

## 스트림 구조
1. 스트림 생성 : 스트림 인스턴스 생성
2. 중간 연산 : 필터링 및 매핑 등 원하는 결과를 만드는 중간 작업
3. 최종 연산 : 최종적으로 결과를 만들어내는 작업

## Create Operations
#### - Arrays.stream()
```java
String[] arr = new String[] {"A", "B", "C"};
Stream<String> stream = Arrays.stream(arr);
Stream<String> streamOfArrayPart = Arrays.stream(arr, 1, 3);
```

#### - Collections.stream()
```java
String[] list = Arrays.asList("A", "B", "C");
Stream<String> stream = list.stream();
Stream<String> parallelStream = list.parallelStream();
```

#### - build()
```java
Stream<String> stream = Stream.<String>builder()
    .add("A")
    .add("B")
    .build();
```
#### - generate()
- 특정 크기를 지정하지 않으면 무한한 크기를 갖기 때문에 `limit`으로 최대 크기를 제한해야함
```java
Stream<String> stream = Stream.generate(() -> "gen").limit(5);
```

#### - iterate()
- 특정 크기를 지정하지 않으면 무한한 크기를 갖기 때문에 `limit`으로 최대 크기를 제한해야함
```java
Stream<Integer> stream = Stream.iterate(30, n -> n + 2).limit(5);
```

## Intermediate Operations
- 각각의 중간 연산자들은 `lazy`하게 실행되고 결과로 `stream`을 반환
- `method chainning`형태로 연결하여 처리할 수 있음

#### Lazy 한 처리
- 결과가 필요하기 전까지 실행되지 않음
- 연산의 시점을 최대한 늦춤

#### 함수형 인터페이스
- Java8에서 제공되는 것으로 추상 메소드를 단 하나만 가지는 인터페이스를 지칭
- Function : input을 받아 output을 출력하는 함수형 인터페이스
- Predicate : boolean을 리턴하는 함수형 인터페이스
- Comparator : 두 값을 비교하기 위한 함수형 인터페이스

#### - filter()
- 원하는 요소만 추출하기 위한 메소드
- 인자로 `Predicate`를 받고 `boolean`을 반환하는 람다식이 들어감
```java
Stream<T> filter(Predicate<? super T> predicate);

//문자열 리스트에서 특정 문자가 포함된 문자열 추출
List<String> list = Arrays.asList("LIST", "STREAM", "TEST");
    .stream()
    .fliter(item -> item.contains("T"))
    .collect(Collectors.toList());
```

#### - map()
- `T`를 인자로 받아 변환한 값 `R`을 반환하는 함수
```java
<R> Stream<R> map(Function<? super T, ? extends R> mapper);

//문자열 리스트를 소문자로 변환
List<String> list = Arrays.asList("LIST", "STREAM", "TEST");
    .stream()
    .map(String::toLowerCase)
    .forEach(System.out::println);
```

#### - filterMap()
- `map`과의 차이점은 함수의 반환 값이 `stream`형태
- 중첩 구조를 한 단계 제거하고 단일 컬렉션으로 만들어줌
```java
<R> Stream<R> flatMap(Function<? super T, ? extends Stream<? extends R>> mapper);

// ex
String arr[][] = {
    {"A", "B", "C"},
    {"D", "E", "F"},
    {"G", "H", "i"}
};
Stream.of(arr)
    .flatMap(Stream::of)
    .forEach(System.out::println);
```

#### - sorted()
- stream 요소를 정렬함
- `Comparator`를 인자로 넣으면 `Comparator`의 기준에 따라 정렬 (default는 오름차순)
```java
Stream<T> sorted();
Stream<T> sorted(Comparator<? super T> comparator);

// 내림차순 정렬
List<String> list = Arrays.asList("LIST", "STREAM", "TEST");
    .stream()
    .sorted(Comparator.reverseOrder())
    .forEach(System.out::println);
```

#### - distinct()
- 중복 제거

#### - peek()
- 결과에 영향을 주지 않고 중간에 값을 출력할 때 사용
```java
Stream<T> peek(Consumer<? super T> action);

// ex
List<String> list = Arrays.asList("LIST", "STREAM", "TEST");
    .stream()
    .peek(System.out::println)
    .sorted(Comparator.reverseOrder())
    .forEach(System.out::println);
```

#### - limit()
- 앞에서부터 n개의 요소만 취함

#### - skip()
- 앞에서부터 n개의 요소를 건너뜀

#### - concat()
- 두 `stream`을 연결
```java
List<String> stream1 = Arrays.asList("A", "B", "C");
List<String> stream2 = Arrays.asList("D", "E", "F");
Stream.concat(stream1, stream2)
    .forEach(System.out::println);
```

## Terminal Operations
### - Calculating
- count()
- sum()
- min()
- max()
- average()

### - accumulator
- reduce
    - 세가지의 인자를 받아 처리할 수 있음
    - accumulator
        - 각 요소를 처리하는 계산 로직
        - 각 요소가 올 때마다 중간 결과를 생성
    - identity
        - 계산을 위한 초기값
        - `stream`이 비어서 계산할 값이 없어도 반환됨
    - combiner
        - 병렬 `stream`에서 나눠 계산한 결과를 하나로 합쳐 반환

### - Collecting
- 스트림 값을 모아 `Map`, `Set`, `List와` 같은 컬렉션 형태로 변환해줌
- 가장 많이 쓰이는 최종 연산자
- Collectors.toList()
    - 리스트 형태로 결과 반환
- Collectors.joining()
    - 스트림 작업 결과를 하나의 스트링으로 연결
    - delimiter : 각 요소의 중간에 들어가는 구분자
    - prefix : 이어붙인 결과 맨 앞에 붙는 문자
    - sufix : 이어붙인 결과 맨 끝에 붙는 문자
- Collectors.groupingBy()
    - 특정 조건으로 요소들을 그룹화하여 `Map` 타입으로 반환
- Collectors.partitioningBy()
    - Predicate로 특정 조건을 받아 해당 조건을 만족하면 `true` 아니면 `false`그룹으로 구분하여 `Map`타입으로 반환
- Collectors.averageingInt()
    - 요소들의 평균을 `Integer`로 반환
- Collectors.summingInt()
    - 요소들의 합을 `Integer`로 반환
- Collectors.summarizingInt()
    - 다양한 연산 결과를 `IntSummaryStatistics`로 반환

### - Match
- anyMatch : 하나라도 조건을 만족하는 요소가 있는지 확인
- allMatch : 모두 조건을 만족하는지 확인
- noneMatch : 모두 조건을 만족하지 않는지 확인

### - forEach()
- 요소를 순회하면서 실행되는 작업
- 인자로 넘긴 메소드에 요소를 대입하여 호출
