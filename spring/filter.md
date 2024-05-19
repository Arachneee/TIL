
- dispatcherServlet 에 전달되기 전에 실행된다.
- 예외 발생시 Spring MVC 외부이므로 controllerAdvice에서 잡지 못한다.
- response, request 객체를 바꿀 수 있다.