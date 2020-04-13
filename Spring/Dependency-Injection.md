# Dependency-Injection
------------
## DI란?
- 객체 자체가 아니라 Framework에 의해 겍체의 의존성이 주입되는 설계 패턴
- Framework에 의해 동적을 주입되므로 여러 객체 간의 결합이 줄어듬
- `DI`는 `Spring Framework`에서 지원하는 `IoC(Inversion of Control)`의 형태
- 설정에 명시된대로 Container가 bean 객체를 생성하고 종속성 주입을 수행
- `DI`와 `IoC`는 같은 의미로 사용됨
- `IoC` : 프로그램 제어권을 Framework가 가져가는 것
  - 개발자가 모든 제어의 중심이지만 코드 전체에 대한 제어는 framework가 한다
  - 개발자가 설정(xml, annotation 등)만 하면 Container가 알아서 처리

#### 의존성 주입 방법
1. Constructor Injection
  - `생성자`를 통한 주입
  - `<constructor-arg ref="object"></constructor-arg>`
  - ex)

```java
@Controller
public class exampleController{

  private ExampleVo = exampleVo;

  public ExampleVo(ExampleVo exampleVo){
    this.exampleVo = exampleVo;
  }
}
```

2. Method(Setter) Injection
  - `setter()`를 통한 주입
  - `<property name="objectName" value="object1"></property>`
  - ex)

  ```java
  @Controller
  public class exampleController{

    private ExampleVo = exampleVo;

    public void setExampleVo(ExampleVo exampleVo){
      this.exampleVo = exampleVo;
    }
  }
  ```

3. Field Injection
  - 멤버 변수를 통한 주입
  - ex)

  ```java
  @Controller
  public class exampleController{

    @Autowired
    private ExampleVo = exampleVo;
  }
  ```

#### DI의 장점
- Reduced Dependencies
  - 종속성의 감소
  - components의 종속성이 감소하면 변경에 민감하지 않음
- More Reusable Code
  - 재사용성의 증가
  - 일부 인터페이스의 다른 구현이 필요한 경우 코드를 변경할 필요없이 해당 구현을 사용하도록 components를 구성할 수 있음
- More Testable Code
  - 더 많은 테스트 코드 작성 가능
- More Readable Code
  - 코드의 가독성 증가
  - components의 종속성을 보다 쉽게 파악할 수 있으므로 코드의 가독성이 증가

#### Spring Container
- Spring Framework의 핵심 컴포넌트
- Container는 DI를 사용하여 응용 프로그램을 구성하는 bean 객체를 관리
- 역할
  - bean을 포함하고 관리하는 책임이 있음
  1. 객체(bean)를 생성
  2. 객체 묶기
  3. 객체 구성
  4. 객체들의 라이프 사이클을 관리
- 설정 방법
  - Spring Container metadata 설정 방법
  1. XML
    1. 빈 객체 정의(Bean Definition)
    2. 의존성 주입(Dependency Injection)
  2. Java Annotation
  3. Java Code
- 유형
  - BeanFactory
    - 주로 단순한 DI에서 사용
    - `XMLBeanFactory`
  - ApplicationContext
    - Resources가 제한되어 있지 않은 모든 곳에 사용
    - `ClassPathXmlApplicationContext`
