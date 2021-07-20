### Sqoop
Sqoop에는 두 가지 동작이 있다.
- import: DB의 데이터를 HDFS로 옮기는 방식
- export: HDFS의 데이터를 DB로 옮기는 방식

![image](https://user-images.githubusercontent.com/30011635/117400962-a110d480-af3e-11eb-900e-a3cb50a19cb1.png)

이런 형태로 스쿱이 하둡과 RDB의 중간에 위치한다.

~~~
스쿱 import 예시
$ sqoop import --connect \"URL\" 
--username \"USERNAME\" 
--password \"PASSWORD\" 
--table \"QUERY\" 
--target-dir \"PATH\" 
--as-parquetfile 
--m 1   // --num-mappers 랑 같음. 맵퍼의 갯수.
~~~


:star: 스쿱으로 데이터를 가져왔으면 가장 먼저 할 일 :star:
1. DB에 있는 데이터 갯수와 하둡에 저장된 데이터 갯수가 같은지 확인 `select count(*)`
2. 샘플 데이터 `show()`로 한글같은게 깨지지 않는지 확인
