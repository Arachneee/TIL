- `@ID`
	- `@GeneratedValue`
	    - strategy
	        - IDENTITY : 기본키 생성을 데이터베이스에 위임 (Mysql에서 주로 사용)
	            - INSERT를 해야 ID가 생성된다.
	            - persist()로 영속성 상태가 되면 바로 INSERT 쿼리가 나간다. 
	            - 쓰기 지연을 할 수 없다.
	        - SEQUENCE : 데이터베이스 시퀀스를 사용해서 키 생성 (오라클에서 주로 사용), `@SequenceGenerator` 필요
	            - IDENTITY와 다르게 INSERT하기 전에
	            - `
	                CREATE SEQUENCE MEMBER_SEQ START WITH 1 INCREMENT BY 1`
	
	            같은 데이터베이스 시퀀스를 통해 ID값을 찾아 영속성 상태로 만든다.
	            - flush()를 해야 INSERT 쿼리가 나간다. 
	            - 쓰기 지연이 가능하다.
	            - `@SequenceGenerator`는 allocationSize 옵션을 제공한다.
	                - 여러 JVM에서 접근해도 50같은 수로 설정하여 기본값 충돌이 나지 않게 하기 위함이다.
	        - UUID : 중복되지 않는 UUID로 키값을 설정한다.
	            - H2는 `@Column(columnDefinition = "BINARY(16)")` 를 설정해야 들어간다.
	        - TABLE : 별도의 키 생성 테이블 사용 `@TableGenerator` 필요
	        - AUTO : 방언에 따라 자동으로 기본 값 적용
	
- JPA는 같은 트랜잭션일 때 같은 객체면 동일성(`==`)이 보장된다.
    - context에 이미 존재하는 객체를 가져오기 때문이다.