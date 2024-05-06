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