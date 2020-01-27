# Refresh Part of Page by jQuery
------------------
#### html의 특정한 태그만 새로고침하고자 할 때 사용
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <!-- jquery -->
    <script src="https://code.jquery.com/jquery-3.4.1.js"
            integrity="sha256-WpOohJOqMqqyKL9FccASB9O0KwACQJpFTUBLTYOVvVU="
            crossorigin="anonymous"></script>
  </head>
  <body>
    <div class="div1">refresh page</div>
    <button type="button" id="refresh"></button>
  </body>
</html>

<script>
  $('#refresh').click(function(){
    $('.div1').load(window.location.href+".div1");
  })
</script>
```
