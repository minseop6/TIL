# Send value on redirect
----------
```java
@PostMapping("/sendRedirect")
public String sendRedirect(RedirectAttributes redirect){
  redirect.addAttribute("value", "value");
  return "redirect:/receiveRedirect";
}

@GetMapping("/receive")
public String receiveRedirect(@RequestParam("value") String value){
  System.out.println(value);

  return value;
}
```
