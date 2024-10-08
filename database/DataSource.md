- DriverManager는 커낵션 풀, 분산 트랜잭션을 지원하지 않는다.
- DataSource는 properties로 디비 연결을 변경할 수 있다.

- Spring Boot는 기본 HikariCP를 사용한다.
	- 성능, 동시성, 안정성, 경량성이 좋다.
- HikariCP 설정
	- maximumPoolSize : 커낵션 풀 최대 사이즈 (기본값 :10)
		- 커낵션의 수가 많아져도 cpu의 코어가 한정적이라 컨텍스트 스위칭 비용이 더 크다.
		- I/O 연산이 많아야 커낵션 수가 컸을 때 의미있다.
	- cachePrepStmts : PreparedStatement(쿼리 파싱 결과)를 캐싱한다.(실행 계획 등) (기본값 : false)
	- prepStmtCacheSize : PreparedStatement의 캐싱 크기 (기본값 : 25)
	- prepStmtCacheSqlLimit : 캐시할 PreparedStatement의 SQL 쿼리의 최대 길이
- Mysql 추천 HikariCP설정
	- https://github.com/brettwooldridge/HikariCP/wiki/MySQL-Configuration