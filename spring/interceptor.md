- 왜 인터셉터 preHandle을 했는데 왜 2번 실행될까?
    - 기본으로 예외가 발생하면 WAS까지 예외가 전파되고 다시 `/error`로 BasicErrorController로 전달된다.
    - 그래서 BasicErrorController를 위한 인터셉터가 실행되고 이때 예외가 또 발생하면 Error page가 렌더링되지 않고 오류 http만 전달한다.
    - 인터셉터 추가시 `/error` 를 제외 시켜야한다.
    - 또는 인터셉터에서 예외를 던지지 않고 리다이렉트를 하거나 http status를 변경하여 false를 반환한다.

- 인터셉터에서 토큰으로 인증을 검증하는데 argumentResolver에서 또 토큰으로 검증 후 Member를 반환해야할까? 토큰 해석을 2번씩 중복할 필요가 있나?
    - 없다. request에 setAttribute로 해당 스레드에서만 사용할 수 있는 객체를 넣을 수 있다.