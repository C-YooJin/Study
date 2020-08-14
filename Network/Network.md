## 네트워크
url이 들어오고 osi 7 계층을 거쳐 서버 전달 -> 유저에게 화면을 띄워주는 것 까지 </br>
- [Computer Network & Web(FE) 면접 정리](https://kadamon.tistory.com/22) </br>
- [기술면접 정리 서버 / 네트워크](https://j2hworld.tistory.com/53) </br>
- [네트워크통신 면접](https://hyeonu1258.github.io/2018/03/10/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC%ED%86%B5%EC%8B%A0%20%EB%A9%B4%EC%A0%91/)


### 모바일 환경에서 대용량 traffic이 발생하면 어떻게 처리할까?에 대한 궁금증 해소
- 로드밸런싱 (Load Balancing)
  - 서비스가 커지고 사업 규모가 확장되면 클라이언트 수 up / 증가한 트래픽 처리하려면 로드밸런싱 필요
  - 둘 혹은 셋 이상의 중앙처리장치 혹은 저장장치와 같은 컴퓨터 자원들에게 작업을 나누는 것
  ![load balancing](https://user-images.githubusercontent.com/30011635/86857858-6231a880-c0fa-11ea-96e1-7738dd3defea.png)
  - Client와 Server pool(서버가 모여있는 풀) 사이에 Load balancer가 client를 자원에 효율적으로 분배해준다.
  - 부하(=로드)를 분산(=밸런싱)
- 로드밸런서 (Load Balancer)
  - 여러대의 서버에 로드밸런싱 해주는 장치
  - L2 load balancer: Mac주소를 바탕으로 Load Balancing 
  - L3 load balancer: IP주소를 바탕으로 Load Balancing
  - L4 load balancer: Transport Layer(IP, port)level에서 Load Balancing
- Scale-up: 서버 자체의 성능을 확장하는 것
  -  cpu i3 -> i7 
- Scale-out
  - 기존 서버와 동일하거나 낮은 성능의 서버를 두 대 이상 증설하는 것
  - 이 경우 반드시 로드밸런싱이 필요해진다
- VIP (Virtual IP)
  - 회사 사정상 Scale-out이 불가능한 경우 하나의 중앙처리장치(cpu+ram+hdd)에 가상 IP를 여러개 만들어 사용한다.
- NETFLEX -> Spring boot + Ribbon + Eureka
  - 로드밸런서를 따로 두지 않고, client단에서 load balancing을 제어하는 것 (스프링부트에 톰캣이 붙어있기 때문에..)
  ![netflex load balancing](https://user-images.githubusercontent.com/30011635/86858894-81c9d080-c0fc-11ea-86d9-074a44befa36.png)
  - 추가 공부 필요
  
### 고가용성 (HA, High Availability)
- 서버와 네트워크, 프로그램 등이 상당히 오랜 기간 동안 정상 운영이 가능한 성질
- 고가용성 = '가용성이 높다' = '절대 고장나지 않음'
### 결함허용 (Fault Tolerant) 
- 하드웨어 또는 소프트웨어의 결함, 오동작, 오류 등이 발생하더라도 설계상 명시된 기능을 지속적으로 수행할 수 있는 시스템
- 시스템의 가용성, 신뢰성, 안정성 보장 

비교항목| HA | FT 
---- | ---- | ----
Failover Time | 0초 | 30 - 300초
동시성 유지보수 | 필요 | 불필요
시스템 비용 | 10 - 20배 | 2배 이상
어플리케이션 | 제한적 | 대부분 범용제품
운영체제 | 전용OS | 범용OS
하드웨어 | 전용 하드웨어 | 범용 

### Netty
- Netty는 TCP, UDP소켓 서버 개발과 같은 네트워크 프로그래밍을 지원한다. (간단하고 쉽게)
- 모든 방식이 Channel, ChannelPipeline, ChannelHandler 인터페이스를 기준의로 정의된다.
- 네티가 제공하는 전송
  - NIO: 논블로킹 입출력. selector기반 방식.
  - Epoll: 논블로킹 입출력. 리눅스에서만 이용한다. NIO 전송보다 빠르고 안전한 논블로킹.
  - OIO: 블로킹 스트림 이용
  - 로컬(Local): VM에서 파이프를 통해 통신하는 데 이용
  - 임베디드(Embedded): 실제 네트워크 기반 전송 없이 ChannelHandler를 이용할 수 있게 해줌. ChannelHandler 구현을 테스트 하는 데 유용.
