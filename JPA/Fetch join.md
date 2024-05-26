- 무분별하게 fetch join을 사용하면 안된다.
	- View에서 필요한 데이터만 로딩하기 위한 메소드가 많아 질 수 있다.
	- Repository가 VIew에 의존하는 형태가 된다.
	- 데이터를 조금 더 조회해 오는 것의 성능 차이가 크지 않다면 적정 수준을 유지하는 것이 좋다.

- jpql에서 엔티티 그래프를 사용하면 항상 Sql에서 outer join을 한다.
	- fetch join을 명시해주면 inner join을 한다.
