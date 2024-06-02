- #### Http Client
	- RestClient
		- synchronous
		- fluent API
		- ExceptionHandler factory 중 Simple 을 사용하면 401에서 다른 예외를 발생시킨다. Jdk를 사용하면 해결 할 수 있다.
	- RestTemplate
		- synchronous
		- template method API
	- WebClient
		- non-blocking
		- reactive client
		- fluent API

- Time Out
	- Connection TimeOut : TCP 3 way handshake 를 하는 시간
	- Read TimeOut : 3 way handshake 이후 데이터를 주고 받는 시간
		- Connection은 3번의 통신을 하지만 Read의 경우 1번의 통신만 필요하다. 
			그래서 Read TimeOut을 짧게 가져가는 것이 좋다.
			1번의 유실정도만 허용한다면 Connection TimeOut을 3초, Read TimeOut을 1초 정도로 설정할 수 있다.

- RTO : 패킷 유일을 판단하는 시간(리눅스 기준 InitRTO = 1초)

- TimeOut 이후 API가 진행 될 수 있다.
- 트랜젝션 내부로 들어가면 DB lock을 오래 점유하게 되어 문제가 생길 수 있다.

##### Test
`@RestClientTest` 와 `MockRestServiceServer` 

RestClient.Builder 가 빈에 등록되어있다.
builder에 바로 errorHandler를 세팅하면 Mocking이 되지 않는다.
RestClientCustomizer 를 사용하여 빈으로 등록하면 Mocking을 사용할 수 있다.

```java
@Bean  
public RestClient restClient(RestClient.Builder restClientBuilder) {  
    return restClientBuilder.build();  
}  
  
@Bean  
public RestClientCustomizer restClientCustomizer() {  
    return (restClientBuilder) -> restClientBuilder  
            .requestFactory(clientHttpRequestFactory())  
            .baseUrl("https://api.tosspayments.com")  
            .defaultHeader("Authorization", createAuthorizationHeader())  
            .defaultStatusHandler(responseErrorHandler());  
}
```

MockRestServiceServer가 RestClient 의 요청에 응답할 수 있다.

```java
@RestClientTest(value = PaymentClient.class)  
@Import(PaymentConfig.class)  
class TossPaymentClientTest {  
  
    @Autowired  
    private PaymentClient paymentClient;  
  
    @Autowired  
    private MockRestServiceServer mockRestServiceServer;  
  
    @DisplayName("결제 승인이 정상 처리된다.")  
    @Test  
    void success() {  
        // given  
        PaymentRequest paymentRequest = new PaymentRequest(1000, "orderId", "paymentKey");  
  
        mockRestServiceServer.expect(requestTo("https://api.tosspayments.com/v1/payments/confirm"))  
                .andRespond(withSuccess());  
  
        // when // then  
        assertThatCode(() -> paymentClient.requestApproval(paymentRequest))  
                .doesNotThrowAnyException();  
    }
```

mockRestServiceServer가 외부 서버의 역할을 모킹하여 테스트 할 수 있다.


`@Configuration`
메소드로 빈을 주입받을 수 있다.
```java
@Bean  
public RestClient restClient(RestClient.Builder restClientBuilder) {  
    return restClientBuilder.build();  
}
```
Config로 빈 설정을 직접하는 것이 서로 다른 모듈로 독립되어 설정을 할 수 있다. 
스캔 방식은 어플리케이션 규모가 커지면 어떤 빈이 등록되었는지 파악하기 어려워진다.
