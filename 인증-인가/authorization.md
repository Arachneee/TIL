- Authorization 헤더는 기본적으로 비선제인증방식이다.
- 비선제인증방식: Authorization 헤더를 처음에는 전달하지 않는다. 이후 인증이 필요한 서버에만 Authorization은 다시 전달한다.
    - 인증이 필요한 서버에만 인증 요청을 보내기 위함이다.
    - RestAssured에서도 기본이 비선제인증방식이므로 Authorization 헤더에 추가하여 전달하기 위해서는 <br>
    `.auth().preemptive().basic(EMAIL, PASSWORD)`로 preemptive를 선언해야한다.
