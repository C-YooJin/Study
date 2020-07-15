### Docker Swarm 
#### 서버 오케스트레이션(server orchestration): 여러 대의 서버와 여러 개의 서비스를 편리하게 관리해주는 작업
![server orchestration tool](https://user-images.githubusercontent.com/30011635/87406241-6af31480-c5fb-11ea-9281-ae9351607890.png)
- 스케줄링: 컨테이너를 적당한 서버에 배포해주는 작업이다. 여러 대의 서버 중 가장 할 일 없는 서버에 배포하거나 그냥 차례대로 배포 또는 아예 랜덤하게 배포할 수도 있다. 컨테이너 개수를 여러 개로 늘리면 적당히 나눠서 배포 하고, 서버가 죽으면 실행 중이던 컨테이너를 다른 서버에 띄워주기도 한다.
- 클러스터링: 여러 개의 서버를 하나의 서버처럼 사용하는 것이다. 여기저기 흩어져 있는 컨테이너도 가상 네트워크를 이용하여 마치 같은 서버에 있는 것 처럼 사용할 수 있다.
- 서비스 디스커버리: 서비스를 찾아주는 기능. ⭐️클러스터 환경에서 컨테이너는 어느 서버에 생성될 지 알 수 없다.⭐️ 따라서 컨테이너와 통신하기 위해서 어느 서버에서 실행중인지 알아야 하고, 컨테이너가 생성되고 중지될 때 어딘가에 IP와 Port같은 정보를 업데이트 해줘야 한다. key-value 스토리지에 정보를 저장할 수도 있고, 내부 DNS서버를 이용할 수도 있다.
- 로깅, 모니터링: 여러 대의 서버를 관리하는 경우 로그와 서버 상태를 한 곳에서 관리하는게 편하다. 툴 or 프로그램 사용. ELK, prometheus등 다양한 툴 활용 가능 <br>

--> 서버 오케스트레이션의 단점: 비용 어마어마, 설치와 관리가 어렵다, 대형 회사에서 보통 사용하는 편, 에러가 생기면 서버 전체에 영향을 줄 수 있어 조심스러움
--> 이런 서버 오케스트레이션의 단점을 도커 스웜이 바꿔 놓음. -> 구축 비용이 거의 들지 않고 관리가 쉬우며 다양한 기능 제공.

ref. [Docker Swarm을 이용한 쉽고 빠른 분산 서버 관리](https://subicura.com/2017/02/25/container-orchestration-with-docker-swarm.html)