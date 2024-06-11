- `@ID`
	- `@GeneratedValue`
	    - strategy
	        - IDENTITY : 기본키 생성을 데이터베이스에 위임 (Mysql에서 주로 사용)
	            - INSERT를 해야 ID가 생성된다.
	            - persist()로 영속성 상태가 되면 바로 INSERT 쿼리가 나간다. 
	            - 쓰기 지연을 할 수 없다.
	        - SEQUENCE : 데이터베이스 시퀀스를 사용해서 키 생성 (오라클에서 주로 사용), `@SequenceGenerator` 필요
	            - IDENTITY와 다르게 INSERT하기 전에
	            - `CREATE SEQUENCE MEMBER_SEQ START WITH 1 INCREMENT BY 1`
	            같은 데이터베이스 시퀀스를 통해 ID값을 찾아 영속성 상태로 만든다.
	            - flush()를 해야 INSERT 쿼리가 나간다. 
	            - 쓰기 지연이 가능하다.
	            - `@SequenceGenerator`는 allocationSize 옵션을 제공한다.
	                - 여러 JVM에서 접근해도 50같은 수로 설정하여 기본값 충돌이 나지 않게 하기 위함이다.
	        - UUID : 중복되지 않는 UUID로 키값을 설정한다.
	            - H2는 `@Column(columnDefinition = "BINARY(16)")` 를 설정해야 들어간다.
	        - TABLE : 별도의 키 생성 테이블 사용 `@TableGenerator` 필요
	        - AUTO : 방언에 따라 자동으로 기본 값 적용
				MYSQL : IDENTITY
				ORACLE : SEQUENCE
				H2 : SEQUENCE
		- 하나씩 Insert 할 때는 IDENTITY 전략이 좋지만 여러건을 insert 할 때는 쓰기 지연을 활용할 수 없으므로 다른 옵션이 좋다.
	
- JPA는 같은 트랜잭션일 때 같은 객체면 동일성(`==`)이 보장된다.
    - context에 이미 존재하는 객체를 가져오기 때문이다.

- 연관관계
	- N:1 양방향 연관관계
		주인만 등록, 수정, 삭제를 할 수 있다.(객체 그래프 탐색으로 꺼낸 후에는 수정가능하다.)
			- team.getMembers().add(new Member()) 는 변경 안됨.
			- team.getMembers().get(0).setName("변경") 은 변경 됨.
		주인이 아닌 쪽은 읽기만 할 수 있다.
		mappedBy 속성을 지정한 쪽은 주인이 아니다.
		테이블 기준으로는 외래키가 있는 쪽이 주인이다.
		장점 : 객체 그래프 탐색 기능이 추가된다. JPQL 그래프 탐색도 가능하다.
		단점 : 고려해야할 사항이 많아진다.
	- 1:N 단방향관계
		객체가 다른 테이블의 외래키를 관리하게 된다.
		다른 테이블에서 쿼리가 나간다.
		- Cascade.ALL을 하면 INSERT 후에 Update 쿼리가 또 나간다.
		- 양방향으로 바꾸는 것이 좋다.
		권장하지 않는다.
	- 일대일 관계
		지연 로딩을 사용해도 프록시로 하면 즉시 로딩된다.
			프록시의 한계로 bytecode instrumentation을 사용해야 해결할 수 있다. 

- 외래키에는 not null 조건을 명시하는 것이 성능적으로 좋다.
	not null이 없으면 outer join을 하게되고 있으면 inner join을 사용한다.
	inner join이 outer join보다 성능이 좋다.
	`@ManyToOne` : optional = false는 내부조인, true는 외부조인
	`@OneToOne` : optional 외부 조인

- 고아객체
	부모 엔티티와 연관관계가 끊어진 자식
	orphanRemoval = true를 통해 엔티티의 참조만 제거하는 방식으로 엔티티가 자동으로 삭제된다.

- 도메인과 엔티티를 분리하면 영속성과의 타협 없이 풍부한 도메인 모델을 생성할 수 있다.