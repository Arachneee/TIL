- 트랜잭션 : 최소단위의 작업
    - 전파 속성
        - PROPAGATION_REQUIRED(Default) : 진행 중인 트랜잭션이 없으면 새로 시작하고 있으면 참여한다.
        - PROPAGATION_REQUIRED_NEW : 무족건 독립적으로 새로 시작한다.
        - PROPAGATION_NOT_SUPPORTED : 트랜잭션이 없다.
    - 런타임 예외만 복구되고 체크 예외는 복구되지 않는다.

![[Pasted image 20240530203018.png]]