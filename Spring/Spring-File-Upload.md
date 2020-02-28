# Spring File Upload
----------

## 환경 설정
```
# MultiPart Upload
spring.http.multipart.enabled=true
spring.http.multipart.max-file-size=1MB
```

## View
```html
<form action="menu" method="POST" enctype="multipart/form-data">
  <div class="form-group">
    <label class="col-sm-2 control-label">상품 이름</label>
    <div class="col-sm-10">
      <input type="text" class="form-control" name="pname">
    </div>
  </div>
  <div class="form-group">
    <label class="col-sm-2 control-label">가격</label>
    <div class="col-sm-10">
      <input type="text" class="form-control" name="price">
    </div>
  </div>
  <div class="form-group">
    <label>이미지 업로드</label>
    <input type="file" name="image">
  </div>
  <button type="submit" class="btn btn-default">등록</button>
</form>
```

## Controller
```java
//Controller
@Controller
public class uploadController {

  @Autowired
	StoreService storeService;

  @GetMapping("/upload")
	public ModelAndView menu(HttpSession session) {

		ModelAndView model = new ModelAndView("upload");

		return model;
	}

  @PostMapping("/upload")
  public String menu(HttpServletRequest request, @RequestParam MultipartFile image) throws IOException {

    //이미지 처리
    System.out.println("save : " + image.getOriginalFilename());
    UUID uid = UUID.randomUUID(); //중복 방지하기 위해 임의로 이름 생성
    String savedName = uid.toString() + "_" + image.getOriginalFilename();
    File target = new File("src/main/resources/static/경로", savedName);
    FileCopyUtils.copy(image.getBytes(), target); //업로드 디렉토리에 저장

    Product product = new Product();
    product.setPname(request.getParameter("pname"));
    product.setPrice(Integer.parseInt(request.getParameter("price")));
    product.setImage(savedName); //파일 경로 저장
    product.setSno(store.getSno());
    product.setStack(0);
    product.setStatus(1);

    productService.addProduct(product);

    return "redirect:/home";
  }
}
```

## Service
```java
//service
@Service
public class ProductService {

	@Autowired
	ProductRepository productRepo;

	public void addProduct(Product product) {
		productRepo.save(product);
	}
}
```
