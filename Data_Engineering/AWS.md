# AWS (Amazon Web Service) 클라우드

## AWS VPC 관련 IAM 정책
- IAM (Identity and Access Management)
- VPC (Virtual Private Cloud)
- EC2 (Elastic Compute Cloud)

![image](https://user-images.githubusercontent.com/30011635/135569483-077dd616-7d5c-461f-9b5b-5904cdd7b102.png)

Ref) [AWS IAM: IAM Policy 알아보기 (이론편)](https://musma.github.io/2019/11/05/about-aws-iam-policy.html)




## AWS Aurora
#### AWS가 MySQL 및 Postgresql을 호환해서 만든 RDBMS
- [RDS MySQL과 AWS Aurora의 큰 차이점](https://notemusic.tistory.com/69)


## Amazon Athena
- 서버리스
- 쿼리당 비용을 지불한다 (데이터 압축, 파티셔닝을 통해 스캔하는 데이터 양을 제한해 비용 절감 가능)
- Facebook에서 개발한 오픈소스 인메모리 분산 쿼리 엔진인 <b>presto</b>를 랩핑해서 AWS cloud에서 구현한 것
- 따라서 아테나는 프레스토의 대부분의 기능들을 지원한다.
- 빠름.. 그러나 큰 데이터는 안정적이지 않음 (RedShift와 고민하는 지점)
#### 데이터 파티셔닝
- S3에 쌓인 많은 로그를 조회할 때 성능을 향상시키고 비용을 절감하는 방법
- 보통 날짜 기준으로 파티셔닝 한다
- Ref) [번개장터 AWS Athena 사용기][https://www.theteams.kr/teams/7937/post/70685]

## Presto
- 단일 query로 여러 개의 data source로부터 데이터를 질의 할 수 있는 빅데이터 처리 언어
- spark 역할.. spark에서 presto로 많이 넘어가기도 하는듯?
- 
