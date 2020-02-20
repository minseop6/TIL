# JSTL
--------
- JPS파일에서 JSTL을 사용하기 위한 선언 방법
```java
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
```

## JSTL Tag
#### - <c:set>
```html
<c:set var="변수이름" value="값" />
```
  - 변수 선언 태그
  - ${변수이름} 으로 사용

#### - <c:if>
```html
<c:if test="true">
	참
</c:if>
```
- eq : 비교하고자 하는 값이 동일한지를 확인할때 사용
- ne : 비교하는 값이 동일하지 않은지 확인할때 사용
- empty : 비교하는 값이 null 인지 확인할때 사용
- and : 모두 참일경우에 참
- or : 하나라도 참이면 참
- not : 논리 부정

#### - <c:forEach>
```html
<c:forEach
  var="변수" items="항목들"
  begin="시작값" end="종료값"
  step="증가값"
  varStatus="변수명">
...
<c:forEach>
```
  - varStatus
    - ${변수명.currnet} : 현재 for문의 값
    - ${변수명.index} : 0부터의 순서
    - ${변수명.count} : 1부터의 순서
    - ${변수명.first} : 첫 번째인지 여부
    - ${변수명.last} : 마지막인지 여부
    - ${변수명.begin} : for문의 시작 번호
    - ${변수명.end} : for문의 끝 번호
    - ${변수명.step} : for문의 증가 값
