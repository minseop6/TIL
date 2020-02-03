# List in a loop
------------------
### 잘못된 코드 예시
```java
public class test{
  public static void main(String[] args){

    List<VO> list = null;

    for(int i=0; i<3; i++){
      Vo vo = new VO();
      list.add(vo); //NullPointerException
    }
  }
}
```
```java
public class test{
  public static void main(String[] args){

    List<VO> list = null;

    Vo vo = new VO();
    for(int i=0; i<3; i++){
      list.add(vo); //에러 발생
    }
  }
}
```

### 올바른 코드 예시
```java
public class test{
  public static void main(String[] args){

    List<VO> list = new List<VO>();

    for(int i=0; i<3; i++){
      Vo vo = new VO();
      list.add(vo); //NullPointerException
    }
  }
}
```
