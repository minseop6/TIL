# Spring Annotation
----------
## 의존 주입
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

## 컨트롤러
- @Controller
- @RestController
- @RequestMapping
- @PathVariable
- @RequestBody
- @RequestParam
- @ResponseBody

## 데이터 접근
- @Service
- @Repository
