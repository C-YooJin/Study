# Apache Spark
### `Repartition`과 `coalesce`의 차이
- 두 메서드는 모두 파티션의 크기를 나타내는 정수를 인자로 받아서 파티션의 수를 조정한다는 점에서 공통점
- But, `repartition()`이 파티션 수 늘리기/줄이기 모두 할 수 있다면 `coalesce()`는 줄이기만 가능
