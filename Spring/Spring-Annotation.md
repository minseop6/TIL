# Spring Annotation
----------
#### @Required
- 필수 속성들을 정의

#### @Autowired
- 의존관계를 자동설정할 때 사용
- 타입을 이용하여 의존 객체를 주입

#### @Qualifier
- 같은 타입의 빈이 두 개 이상 존재하는 경우에 사용
- @Autowired와 함께 사용해서 어떤 bean을 사용할지 지정하여 객체 주입

#### @Resource
- 이름을 이용하여 의존 객체를 주입

#### @Inject
- @Autowired와 동일하게 타입을 이용하여 의존 객체를 주입
- @Autowired와는 달리 Spring Framework에서 지원하는게 아니라 Java에서 지원

#### @Controller
- Spring MVC에서 Controller클래스임을 명시

#### @RestController
- @Controller + @ResponseBody

#### @RequestMapping
- URI를 정의
- value : 해당 url로 요청이 들어오면 해당 메소드가 수행
- method(GET, POST, PATCH, PUT, DELETE) : 요청 method를 명시

#### @PathVariable
- 요청 URI의 패스 변수 값을 매핑

#### @RequestBody
- HTTP 요청시 넘어온 body값을 매핑

#### @RequestParam
- HTTP 요청시 파라미터를 매핑

#### @ResponseBody
- 자바 객체를 HTTP 요청의 body값으로 매핑

#### @Service
- Spring MVC에서 비즈니스 로직을 수행하는 클래스임을 명시

#### @Repository
- Spring MVC에서 DB에 접근하는 클래스임을 명시
