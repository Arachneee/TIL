- 묵시적 조인과 명시적 조인
	- `select m.t from Member m join m.team t` : 명시적 조인
	- `select m.t from Member m` 묵시적 조인
	- 묵시적 조인으로 join을 명시하지 않아도 inner join을 수행한다.
	- 명시적 조인을 사용하는 것이 성능을 분석하기 좋다.
- 타입 표현
	- 문자는 작은 따옴표로 표현 ''
	- Enum은 패키지명을 포함한 전체 이름
	- 엔티티 타입 TYPE(m) = Member 타입 비교도 가능
- TREAT 
		상속 구조에서 타입 캐스팅 가능
- Named 쿼리를 사용하면 애플리케이션 로딩 시점에 JPQL 문법을 체크하고 미리 파싱해두어 성능 최적화에 도움이 된다.
- 데이터를 조회할 때 영속성 컨텍스트에서 엔티티를 먼저 찾지 않고 데이터베이스를 바로 조회한다.
	- 조회후에 영속성 컨텍스트에 존재하면 조회한 값을 버린다.
- 실행 전에 flush를 하고 데이터를 조회한다.