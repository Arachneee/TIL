- OS에 종속받지 않고 CPU가 Java 인식, 실행할 수 있게 하는 가상 컴퓨터이다.
- .class(바이트 코드)를 JIT 컴파일러가 바이너리 코드로 변환한다.
	- 바이트 코드 : JVM이 이해할 수 있는 코드
	- 바이너리 코드 : CPU가 이해할 수 있는 코드
![[Pasted image 20240924002729.png]]

## 메모리 영역
- Heap
	- new 로 생성된 인스턴스 객체
	- 배열
![[Pasted image 20240924003721.png]]
	- Permanent
		- 영구 세대
		- Meta 정보가 저장되는 영역
		- Reflection으로 동적으로 로딩되는 경우 사용
		- GC의 대상이지만 빈도가 적다.
	- New/Young
		- Minor GC
	- Old
		- Major GC
- Stack
		- 할당된 변수
- Method (= Class area = Static area)
	- 클래스 정보를 처음 메모리 공간에 올릴 때 초기화되는 대상을 저장하기 위한 메모리 공간
	- 전역 변수
	- 참조 변수

- JDK
	- JRE를 포함하여 javac, javadoc 등이 있다.
- JRE
	- JVM + 자바 라이브러리