# Apache Spark
### `Repartition`과 `coalesce`의 차이 (작성중)
- 두 메서드는 모두 파티션의 크기를 나타내는 정수를 인자로 받아서 파티션의 수를 조정한다는 점에서 공통점
- But, `repartition()`이 파티션 수 늘리기/줄이기 모두 할 수 있다면 `coalesce()`는 줄이기만 가능


### `dynamic.partition.mode` 옵션 값
- `hive.exec.dynamic.partition = true`: This will set the dynamic partitioning for hive application
- `hive.exec.dynamic.partition.mode = nonstrict`: This will set the mode to non-strict. The non-strict mode means it will allow all the partition to be dynamic.
- 아무래도 동적 파티션(dynamic partition)과 정적 파티션(static partition)의 차이를 명확하게 하는게 좋을듯함

#### (1) 동적 파티션(dynamic partition)
컬럼 정보로 파티션이 생성되기 떄문에 쿼리 시점에는 파티션을 알 수 없다. 
```
INSERT INTO TABLE tbl(yymmdd)
SELECT name,
       yymmdd
FROM   temp;
```
위와 같이 입력할 때 temp 테이블의 yymmdd 컬럼에 20210101, 20210102 두 개의 데이터가 있으면 다음과 같이 생성한다.
```
hdfs://[tbl 위치]/yymmdd=20210101/
hdfs://[tbl 위치]/yymmdd=20210102/
```
hive는 기본적으로 동적 파티션만 이용하는 것을 권장하지 않는다. 따라서 동적 파티션만 이용하기 위해서는 `hive.exec.dynamic.partiton.mode`설정을 `nonstrict`로 변경해야 한다. <br>
동적 파티션을 사용하면 속도가 느려지기 때문에 동적 파티션의 생성 개수에 제한이 있다. 기본 설정보다 많은 파티션을 생성할 때는 다음 설정을 해주어야한다.
```
// 동적 파티션 개수
set hive.exec.max.dynamic.partitions=1000;

// 노드별 동적 파티션 생성 개수
set hive.exec.max.dynamic.partitions.pernode=100;
```

#### (2) 정적 파티션(static partition)
테이블에 데이터를 입력하는 시점에 파티션 정보를 전달하기 때문에 입력되는 파티션을 알 수 있다.

### Spark dataframe `cache()` `persist()`
- 한 번 로드 된 데이터를 저장공간에 올려놓는다.
- `cache()` 말고 `persist()`를 사용하면 스토리지 레벨 파라미터(storage level parameter)를 직접 특정해줄 수 있나보다.
  - `MEMORY_AND_DISK, MEMORY_ONLY, DISK_ONLY` 같은게 있다. 디폴트는 <b>MEMORY_AND_DISK</b>다.        
