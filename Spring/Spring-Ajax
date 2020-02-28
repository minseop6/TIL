# Spring-AJax
------------------
```html
<form action="loginAjax" method="post">
  <div class="form-group">
    <label for="exampleInputEmail1">ID</label>
    <input type="email" class="form-control" id="id" placeholder="이메일을 입력하세요">
  </div>
  <div class="form-group">
    <label for="exampleInputPassword1">PW</label>
    <input type="password" class="form-control" id="pw" placeholder="암호">
  </div>
  <button type="button" id="login" class="btn btn-default">LOGIN</button>
</form>
...

<script>
//로그인
$('#login').click(function(){
  $.ajax({
    type: "POST",
    url: "/forder/login",
    data:{
      "id": $('#id').val(),
      "pw": $('#pw').val(),
    },
    success: function(){
      alert("LOGIN SUCCESS");
      $('#button').load(window.location.href + "#button");
    },
    error: function(){
      alert("LOGIN FAIL")
    }
  })
})
</script>
```

Service
```java
public boolean login(String id, String pw) {

  User user = userRepo.findById(id);
  if(user.getId().equals(id) && user.getPw().equals(pw)) {
    return true;
  } else {
    return false;
  }
}
```

Controller
```java
//로그인
@PostMapping("/login")
@ResponseBody
public String login(HttpServletRequest request, HttpSession session) {

  String id = request.getParameter("id");
  String pw = request.getParameter("pw");
  if(userService.login(id, pw)) {
    session.setAttribute("name", id);

    return "mypage";
  }else {
    return "fail";
  }
}
```
