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
--m 1
~~~
