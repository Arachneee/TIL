> Persistence cascade(영속성 전이)

| Cascade Type | 설명                                                    |
| ------------ | ----------------------------------------------------- |
| PERSIST      | Entity를 영속 객체로 추가할 때 연관된 Entity도 함께 영속 객체로 추가한다.      |
| REMOVE       | Entity를 삭제할 때 연관된 Entity도 함께 삭제한다.                    |
| DETACH       | Entity를 영속성 컨텍스트에서 분리할 때 연관된 Entity도 함께 분리 상태로 만든다.   |
| REFRESH      | Entity를 데이터베이스에서 다시 읽어올 때 연관된 Entity도 함께 다시 읽어온다.     |
| MERGE        | Entity를 준영속 상태에서 다시 영속 상태로 변경할 때 연관된 Entity도 함께 변경한다. |
| ALL          | 모든 상태 변화에 대해 연관된 Entity에 함께 적용한다.                     |
