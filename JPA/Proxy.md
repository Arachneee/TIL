엔티티와 프록시 동등성
- getClass 대신 instanceOf를 써야한다.
- 맴버변수에 직접접근하면 프록시는 null인 상태이므로 getxx 를 사용하여 비교해야한다.