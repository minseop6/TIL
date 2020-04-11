# Dynamically generated tag event
---------------
- `document.ready`는 처음 로드되었을 때의 태그들에 이벤트를 걸어줌
- 동적 태그는 `document.ready` 이벤트가 적용되지 않음

```javascript
/* <button type="button" class="example">EXAMPLE</button>를
  동적으로 만들었을 때  click 이벤트 적용하는 예시 */
$(document).on('click', '.example', function(){
  console.log("Dinamic tag");
})
```
