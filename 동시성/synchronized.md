- synchronized
Spring AOP인 @Transactional를 사용하면 프록시 객체를 생성한다.
synchronized는 상속이 되지 않아 동시성 보장이 되지 않는다.
또한 다른 예약과도 순차 실행이 되어 성능상으로 좋지 않다.

- AtomicBoolean, ConcurrentHashMap
특정 예약에 대해 요청을 큐에 담아 첫번째 요청만 승인 시킨다.

서버가 여러대일 경우 대응 할 수 없다.

- 락(PESSIMISTIC_WRITE) + 격리 수준 READ_COMMITTED
예약 슬롯에 비관락을 걸어 읽을 수 없게하고 격리 수준을 READ_COMMITTED으로 설정하여 다른 트랙젝션이 쓰기를 한 데이터를 읽을 수 있게 한다.

예약완료후 예약 대기들은 비관락이 필요하지 않다. 또한 읽기도 불가능하여 예약 중에 예약 슬롯을 읽을 수 없다. 비관락으로 인한 성능 저하가 발생했다.

- 네임드 락
레코드에 락을 거는 방식이 아닌 예약 슬롯 문자에 락을 걸어 다른 곳에서 예약 슬롯을 읽을 수 있도록 할 수 있다.

- 메시지 큐


### 1. 비관락 (Pessimistic Locking)

#### 장점:

- **데이터 일관성:** 비관락은 데이터베이스 레벨에서 직접 잠금을 걸어, 동시에 여러 트랜잭션이 동일한 데이터를 수정하지 못하도록 합니다.
- **즉각적인 충돌 방지:** 잠금이 활성화되면 다른 트랜잭션은 해당 데이터를 수정하거나 읽을 수 없으므로, 즉각적으로 데이터 충돌을 방지합니다.

#### 단점:

- **성능 저하:** 트랜잭션이 오랜 시간 동안 잠금을 유지하면 다른 트랜잭션이 대기하게 되어 성능이 저하될 수 있습니다.
- **데드락 위험:** 여러 트랜잭션이 서로의 잠금을 기다리는 상황이 발생할 수 있습니다.
- **스케일 문제:** 많은 사용자나 요청이 있을 경우, 데이터베이스의 성능이 저하될 수 있습니다.

### 2. 메시지 큐 (Queueing)

#### 장점:

- **비동기 처리:** 예약 요청을 큐에 넣고 순차적으로 처리할 수 있어, 동시에 들어오는 요청을 효율적으로 관리할 수 있습니다.
- **확장성:** 메시지 큐를 사용하면 시스템의 부하를 분산시키고 수평적으로 확장하기가 용이합니다.
- **과부하 방지:** 요청을 큐에 쌓아두고, 시스템이 처리할 수 있는 만큼만 진행하므로 과부하를 방지할 수 있습니다.

#### 단점:

- **복잡성 증가:** 메시지 큐를 도입하면 시스템 구조가 복잡해질 수 있으며, 추가적인 컴포넌트가 필요합니다.
- **지연 시간:** 큐에 쌓인 요청이 처리되기까지 시간이 걸릴 수 있으므로, 실시간성이 중요한 경우에는 적합하지 않을 수 있습니다.
- **장애 처리:** 큐에 쌓인 메시지의 상태를 관리해야 하며, 처리 중 문제가 발생할 경우 복구 로직을 구현해야 합니다.

### 결론

- **비관락**은 데이터의 즉각적인 일관성을 보장해야 할 때 유용하며, 상대적으로 단순한 시스템에 적합합니다. 그러나 대규모 트랜잭션을 처리하는 경우 성능 문제가 발생할 수 있습니다.
- **메시지 큐**는 대량의 요청을 비동기적으로 처리하고 시스템의 부하를 분산시키는 데 유리합니다. 그러나 시스템의 복잡성이 증가하고, 처리 지연이 발생할 수 있습니다.

- 메시지 큐
	- 메시지 브로커
		- Producer가 생산한 메시지를 큐에 저장한다.
		- Consumer가 메시지를 가져간다.
		- Consumer가 가져간 메시지는 짧은 시간안에 삭제된다.
	- 이벤트 브로커
		- 메시지 브로커의 역할도 한다.
		- Consumer가 가져간 메시지는 삭제되지 않고 다시 소비할 수 있다.

