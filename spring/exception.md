- RequestBody의 경우 jsonformat 또는 객체에 맞지 않는 형식을 입력받을 경우 HttpMessageNotReadableException이 발생한다.
- RequestParam의 경우 IllegalArgumentException이 발생한다.
  
- ExceptionHandler :
  - 메소드 단위에서 사용하면 해당 Controller의 예외만 잡는다.
  - 클래스 단위에서 ControllerAdvice와 함께 쓰이면 전체 Controller의 예외를 잡는다.

- HttpMessageNotReadableException 은 json변환 오류를 spring 오류로 변환시켜 던져준다.
    - DateTimeParseException 도 변환된다. 변환될 때 Throwable로 들어간다.
    - 아래 처럼 예외를 바꿀 수 있다.
```java
@ExceptionHandler(HttpMessageNotReadableException.class)
    public ResponseEntity<String> handleHttpMessageNotReadableException(final HttpMessageNotReadableException e) {
        logger.error(e.getMessage(), e);
        final Throwable rootCause = e.getRootCause();
        if (rootCause instanceof DateTimeParseException dateTimeParseException) {
            final String parsedString = dateTimeParseException.getParsedString();
            return ResponseEntity.badRequest().body(parsedString + " 의 형식이 잘못됐습니다.");
        }
        return ResponseEntity.badRequest().body("json의 형식이 잘못됐습니다.");
    }
```
- DateTimeParseException 은 HttpMessageNotReadableException 로 변환되므로 HttpMessageNotReadableException의 부모타입에 의해 advice에서 잡힌다.
    - 하지만 HttpMessageNotReadableException의 부모타입이을 잡지 않는 경우 DateTimeParseException을 잡을 수 있다.(왜 잡을 수 있을까?)

- WebMvcConfigure 에서 addViewController 로 설정한 view는 인터셉터에서 예외가 발생해도 왜 controllerAdvice의 ExceptionHandler에서 잡히지 않을까?
    - 인터셉터에서 발생한 예외는 dispatcherServlet에서 잡아 `processHandlerException()`를 실행한다.
    - `HandlerExceptionResolver` list 중에서 사용할 수 있는 resolver를 선택하여 수행한다.
    - 그 중 controllerAdvice의 ExceptionHandler는 `ExceptionHandlerExceptionResolver`에서 수행된다.
    - `ExceptionHandlerExceptionResolver`의 수행 조건이 Handler가 `HandlerMethod` 일 경우만 실행할 수 있다.
    - 그런데 addViewController로 설정한 controller는 `HandlerMethod` 가 아니라 `ParameterizableViewController`이다.
    - 그래서 ExceptionHandler에서 잡히지 않는다.