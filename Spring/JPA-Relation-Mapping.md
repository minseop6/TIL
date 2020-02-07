# JPA Relation Mapping
--------------
## 연관관계란?
- 엔티티들을 대부분 서로 관계를 맺고있음
- 객체의 참조와 테이블의 외래키 매핑을 의미
- Mybatis와 달리 참조 테이블의 PK를 변수로 갖지 않고 객체 자체를 참조

## 방향
- 단방향 관계 : 두 엔티티가 관계를 맺을 때 한쪽의 엔티티만 참조
- 양방향 관계 : 두 엔티티가 관계를 맺을 때 양쪽의 엔티티가 서로 참조

## 다중성
#### - OneToOne : 일대일(1:1)
```java
@Entity
@Table(name="student")
public class Student{
  @Id
  @GeneratedValue(strategy=GenerationType.IDENTITY)
  @Column(name="sno")
  private Integer sno;

  @Column(name="name")
  private String name;

  @OneToOne
  @JoinColumn(name="locker_lno")
  private Locker locker;
  ...
}
@Entity
@Table(name="locker")
public class Locker{
  @Id
  @GeneratedValue(strategy=GenerationType.IDENTITY)
  @Column(name="lno")
  private Integer lno;

  @Column(name="title")
  private String title;

  @ManyToOne
  @JoinColumn(name="student_sno")
  private Student student;

  //양방향
  @OneToOne(mappedBy="locker")
  private Student student;
  ...
}
```
#### - ManyToOne : 다대일(N:1)
```java
@Entity
@Table(name="student")
public class Student{
  @Id
  @GeneratedValue(strategy=GenerationType.IDENTITY)
  @Column(name="sno")
  private Integer sno;

  @Column(name="name")
  private String name;
  ...
}
@Entity
@Table(name="book")
public class Student{
  @Id
  @GeneratedValue(strategy=GenerationType.IDENTITY)
  @Column(name="bno")
  private Integer bno;

  @Column(name="title")
  private String title;

  @ManyToOne
  @JoinColumn(name="student_sno")
  private Student student;

  ...
}
```

#### - OneToMany : 일다대(1:N)

```java
//양방향
@Entity
@Table(name="student")
public class Student{
  @Id
  @GeneratedValue(strategy=GenerationType.IDENTITY)
  @Column(name="sno")
  private Integer sno;

  @Column(name="name")
  private String name;

  @OneToMany(mappedBy="student")
	private List<Book> books = new ArrayList<Book>();
  ...
}
@Entity
@Table(name="book")
public class Student{
  @Id
  @GeneratedValue(strategy=GenerationType.IDENTITY)
  @Column(name="bno")
  private Integer bno;

  @Column(name="title")
  private String title;

  @ManyToOne
  @JoinColumn(name="student_sno")
  private Student student;

  ...
}
```

#### - ManyToMany : 다대다(N:N)
