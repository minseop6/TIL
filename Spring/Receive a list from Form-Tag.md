# Receive a list from Form-Tag
---------------
Form 태그를 통해서 파리미터를 리스트로 넘기는 방법
```html
<form action="/forder/purchase" method="get">
  <div class="container">
    <c:set var="count" value="0" />
    <c:set var="add" value="1" />
    <c:forEach var="item" items="${list }">
      <div class="product">
        <img class="food" src="/static/img/product/${item.image}">
        <ul class="information">
          <li>${item.pname}</li>
          <li>${item.price}</li>
        </ul>
        <div class="group">
          <button type="button" class="btn btn-default minus">-</button>
          <input type="text" name="purchase[${count}].amount" value="0">
          <button type="button" class="btn btn-default plus">+</button>
          <input type="hidden" name="purchase[${count}].pno" value="${item.pno}">
        </div>
      </div>
      <c:set var="count" value="${count + add}" />
    </c:forEach>
  </div>

  <div class="bottom">
    <button type="submit" class="btn btn-default order">주문하기</button>
  </div>
</form>
```
```java
// Order.java
@Getter
@Setter
public class Order {

	private int pno;

	@Column(name="amount")
	private int amount;
}
```

```java
// purchase.java
@Getter
@Setter
public class Purchase {

	private List<Order> purchase;
}

```

```java
// MainController.java
@GetMapping("/purchase")
public ModelAndView purchase(@ModelAttribute Purchase purchase) {

 ...

}
```
