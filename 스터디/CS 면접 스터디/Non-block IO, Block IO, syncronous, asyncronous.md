## I/O 종류
- network(socket)
- file
- pipe : 프로세스간 I/O
- device
## Block I/O
- I/O 작업을 요청한 프로세스/스레드는 요청이 완료될 때까지 대기
## Non-Block I/O
- 프로세스/스레드를 블락시키지 않고 요청에 대한 현재 상태를 즉시 리턴
### Non-Block I/O 작업 완료 확인 방식
1. 반복적인 완료 확인
	- 완료된 시간과 완료 확인 시간 사이의 갭 발생
	- 처리 속도 지연
	- 반복적인 확인으로 CPU 낭비
 2. I/O multiplexing
	- 관심있는 I/O 작업들을 동시에 모니터링하고 그 중에 완료된 I/O 작업들을 한번에 알려줌
	- 여러 이벤트에 대해 한번에 처리한다.
 3. callBack 으로 완료 확인
## Syncronous
- 동기
- 순차적으로 실행
## Asyncronous
- 비동기
- 독립적으로 실행
- multithreading : asyncronous programming의 한 종류

