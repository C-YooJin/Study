## Apache Kafka
- 스키마: Json이나 XML보다 Avro를 선호한다. Avro는 원래 하둡을 위해 개발된 직렬화(serialization) 프레임워크다. 데이터를 직렬화하는 형식을 제공하며, 메시지와는 별도>로 스키마를 유지 관리하므로 스키마가 변경되더라도 애플리케이션의 코드를 추가하거나
 변경할 필요가 없다.
- 배치: 카프카는 효율성을 위해 여러 개의 메시지를 모아 batch형태로 파티션에 수록한
다. 이 경우 대기시간(latency)과 처리량(throughput)간의 트레이드오프가 생길 수 있다. 즉, 배치의 크기가 클 수록 단위 시간당 처리될 수 있는 메시지는 많아지지만, 각 메>시지의 전송 시간은 더 길어진다.
- 토픽 == 여러개의 파티션으로 구성 / <b>각 파티션은 서로 다른 서버에 분산될 수 있다.</b> 지금 회사에서도 chriss랑 james에 파티션 분리 돼 있음.
- 파티셔너는 key의 hash값을 생성하고, 그것을 특정 파티션에 대응시킨다.
- 컨슈머 그룹은 하나 이상으 컨슈머로 구성된다. 한 토픽을 소비하기 위해 같은 그룹의 여러 컨슈머가 함께 동작한다. <b>각 컨슈머가 특정 파티션에 대응되는 것을 소유권(ownership)이라고 한다.</b>
- Broker: 시스템 하드웨어 성능에 따라 다르겠지만, 하나의 브로커는 초당 수천 개의 토픽과 수백만 개의 메시지를 처리할 수 있다.
- 디스크 기반의 보존: 토픽별로 보존 옵션을 선택할 수 있다. 보존 기간동안 컨슈머가 동작하지 않더라도 메시지는 카프카에 보존되므로 프로듀서의 메시지 백업이 필요 없다. (카프카 핵심 가이드 11p)
- [Franz Kafka](https://ko.wikipedia.org/wiki/%ED%94%84%EB%9E%80%EC%B8%A0_%EC%B9%B4%ED%94%84%EC%B9%B4) : kafka 이름은 작동방식과 전혀 상관이 없다..?
- Kafka Consumer V0.9 이상부터는 offset 정보를 __consumer_offsets 토픽에 pruduce 한다.
- Burrow
  - [consumer lag monitoring tool](https://blog.voidmainvoid.net/243)
  - Burrow는 __consumer_offsets 토픽을 consume해서 다양한 정보를 가공 및 저장하고 HTTP로 조회가 가능하도록 만든 프로그램
  - Burrow에서 <b>consumer module</b>은 __consumer_offsets 토픽을 consume하면서 fetch한 메시지를 storage module을 이용하여 메모리에 저장한다.
  - <b>storage</b>는 Burrow에서 수집하는 데이터 (Topic/Consumer 정보) 저장/조회 역할을 담당
  - <b>evaluate</b>는 Consumer Offset/Lag을 지켜보면서 Consumer Group의 상태를 판단하는 역할 
    - topic/partition 상태를 판단해서 가장 안 좋은 상태가 Consumer Group의 상태가 된다. [ref](https://dol9.tistory.com/273?category=699081)
- 리밸런싱(Rebalancing): 한 컨슈머로부터 다른 컨슈머로 파티션 소유권을 이전하는 것
  - 컨슈머 그룹의 가용성과 확장성을 높여준다. 
  - 쉽고 편리하게 컨슈머를 추가, 삭제할 수 있다.
  - 단점: 리밸런싱 하는 동안 컨슈머들은 메시지를 읽을 수 없기 때문에 해당 컨슈머 그룹 전체가 잠시나마 사용 불가 상태가 된다. 또한 한 컨슈머로부터 다른 컨슈머로 파이션이 이전될 때는 해당 컨슈머의 이전 파티션에 관한 현재 상태 정보가 없어진다. 즉, 캐시 메모리에 있던 데이터도 지워진다. 

#### Q. 카프카가 왜 분산처리에 좋은가?
- 카프카는 '분산형 스트리밍 플랫폼'이다
- Queue와 Publish - subscribe 모델을 활용해 브로드캐스팅 처리와 개별적 병렬 처리가 가능
- Broker와 Partition 확장이 용이하기 때문에 부하 분산이 손쉽다
#### Q. 카프카가 죽으면 어떻게 되나?
- 더이상 Leader가 될 수 있는 Replica가 없는 경우, Read/Write가 멈추는 것은 당연하다. 다만, 복구될 때 대응 방법이 나눠어 진다.
- 마지막까지 leader였던 broker1번이 up이 되고 다시 leader가 될 때까지 기다린다.(모든 데이터를 가지고 있을 가능성이 높다)
- ISR과 상관없이 누구라도 가장 빨리 up이 되는 topic이 leader가 된다.(데이터 손실이 되더라도 장애 대응이 빠르다)

### 하나의 컨슈머 그룹에 있는 여러개의 컨슈머가 같은 토픽을 구독할 수 있는가?
- 가능하다. 다만 각 컨슈머별로 소유권을 가진 파티션을 구독할 수 있다. 
![image](https://user-images.githubusercontent.com/30011635/127764669-8ec1aedb-a0e2-4918-a37a-92dcc7f79c6f.png)

