> 도메인 객체에 접근하기 위해서 컬렉션과 유사한 인터페이스를 사용해 도메인과 데이터 매핑 계층 사이를 중재하는 역할 feat. 마틴 파울러

- 전제 : 내가 생각하는 Repository의 역할<br>
    - Repository는 데이터베이스가 아닌 객체 중심의 설계가 되어야한다.<br>
    &rarr; Repository는 일급컬렉션 && 도메인 객체다.<br>
    &rarr; Repository는 자신의 데이터만 관리할 수 있어야한다.<br>
    &rarr; `<T>` 객체의 Repository는 `List<T>`로 만들 수 없는 결과를 반환하면 안된다.<br>(예측 불가능한 동작, 과도한 책임, 과도한 역할)<br>
    &rarr; (논외) (이건 좀 더 고민) Repository는 비지니스 로직을 수행해도 된다.<br>

- 질문1 : 인기테마를 ThemeRepository와 ReservationRepository 둘 중 어디서 가져와야하나?
    - 주장 : ReservationRepository에서 가져와야만 한다.
    - 이유 : `List<Theme>`로는 절대 인기테마를 만들 수 없다. 하지만 `List<Reservation>`으로는 인기테마를 만들 수 있다.<br>
    &rarr; ThemeRepository에서 가져오는 것은 제공하면 안되는 기능을 제공하는것이다.<br>
    &rarr; 잘못된 추상화다.<br>
    &rarr; ThemeRepository 객체의 역할이 과도하게 많다.<br>
    &rarr; 인터페이스가 구현체에 의존하는 기능이다.<br>
    &rarr; 데이터베이스에 종속된 설계다.<br>
    &rarr; 확장성이 떨어진다.(메모리 기반, 파일시스템, NoSql 등으로 바꿀 수 없다.)<br>

- 질문2 : 시간의 예약가능 여부를 조회하는 한방쿼리를 보내도 될까요? 보낸다면 어느 레포지토리에 위치해야할까요?
    - 주장 : ReservationRepository와 ReservationTimeRepository 둘 다 전체 시간의 예약가능 여부를 한방 쿼리를 보내면 안된다.
    - 이유: `List<Reservation>`과 `List<ReservationTime>` 둘 다 있어야만 만들 수 있는 결과다. 한가지로는 만들 수 없다.<br>
    &rarr; 한방쿼리로 만든 메소드는 제공하면 안되는 기능을 제공하는 메소드다.<br>
    &rarr; 잘못된 추상화다.<br>
    &rarr; 해당 Repository 객체의 역할이 과도하게 많다.<br>
    &rarr; 인터페이스가 구현체에 의존하는 기능이다.<br>
    &rarr; 데이터베이스에 종속된 설계다.<br>
    &rarr; 확장성이 떨어진다.