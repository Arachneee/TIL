### Map 
- 정의 : key-value pair들을 저장하는 ADT(추상 자료형)
- 구현체 : hash table, tree-based
### HashTable
- 정의 : 배열과 해시함수를 사용하여 map을 구현한 자료구조
- 특징 : 상수 시간으로 데이터에 빠르게 접근한다.
### HashFuction
- 정의 : 임의의 크기를 가지는 type의 데이터를 고정된 크기를 가지는 type의 데이터로 변환하는 함수
### Hash table 기본 동작
- put("010-3313-9533", "백호") -> hash fuction ->  202 -> % capacity(16) -> 10(인덱스)


| index | key             | value | hash |
| ----- | --------------- | ----- | ---- |
| 0     |                 |       |      |
| 1     |                 |       |      |
| 2     | "010-3313-9533" | "백호"  | 202  |
| 3     |                 |       |      |
| 4     |                 |       |      |
| 5     |                 |       |      |
| 6     |                 |       |      |
| 7     |                 |       |      |

### Hash collision
- 발생 가능 상황
	- key는 다른데 hash가 같은 경우
	- key, hash 둘다 다른데 hash % capacity 결과가 같은 경우
- 해결 방법
	- open addressing(CPython)
		- 종류
			- Linear Probing : 순차적으로 탐색하며 비어있는 버킷을 찾을 때까지 계속 진행된다.
			- Quadratic probing : 2차 함수를 이용해 탐색할 위치를 찾는다.
			- Double hashing probing : 하나의 해쉬 함수에서 충돌이 발생하면 2차 해쉬 함수를 이용해 새로운 주소를 할당한다. 위 두 가지 방법에 비해 많은 연산량을 요구하게 된다.
		- 특징
			- 충돌이 난 경우 다른 빈 버킷에 저장한다.
			- 다른 빈 버킷을 찾지 못하고 돌아올 수 있다.
			- 찾을 때 다른 버킷도 탐색해야한다.
			- 삭제할 때 다음 버킷의 위치를 변경하거나 더미를 추가한다.
		
	- separate chaining(Java)
		- 종류
			- Linked List
				- 각각의 버킷(bucket)들을 연결리스트(Linked List)로 만들어 Collision 이 발생하면 해당 bucket 의 list 에 추가하는 방식. 
				- 삭제 또는 삽입이 간단하다. 
				- 작은 데이터들을 저장할 때 연결 리스트 자체의 오버헤드가 부담.
				- 버킷을 계속해서 사용하는 Open Address 방식에 비해 테이블의 확장이 늦음.
		    - Red-Black Tree
			    - 연결 리스트 대신 트리를 사용하는 방식.
			    - 트리는 기본적으로 메모리 사용량이 많다.
			
			- 선택 기준 : 하나의 해시 버킷에 할당된 key-value 쌍의 개수이다. 
				- 데이터의 개수가 적다 -> 링크드 리스트. 
					- 데이터 개수가 적을 때 Worst Case 를 살펴보면 트리와 링크드 리스트의 성능 상 차이가 거의 없다. 
					- 메모리 측면을 봤을 때 데이터 개수가 적을 때는 링크드 리스트를 사용한다.
### Hash table resizing
- java 기준으로 버킷이 75% 찬 경우 사이즈를 2배 늘린다. (CPyhon 기준으로 버킷이 66% 찬 경우 사이즈를 2 or 4배 늘린다.)
- resizing 후 hash % capacity를 다시 해야하므로 빠른 동작을 위해 hash도 저장해둔다.
- 사이즈는 2의 지수이다.

### 단점
- Hash를 저장해야하므로 List보다 메모리를 더 많이 모소한다.