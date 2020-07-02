## Spring과 Spring Boot 장/단
Spring -> Spring legacy Project로 현업에서 아직 많이 쓰이고 있다. </br>
Spring Boot -> 개발 환경 세팅이 좀더 간편하고 (최소화 돼 있고) 실행 및 배포가 간단
해짐. </br>

#### Ref.
- [자바 스프링 home.jsp의 동작 원리](https://all-record.tistory.com/165)

- Spring Bean이란?
  - 스프링 빈이란 자바 객체다. 스프링에서 만들어진 자바 객체가 빈이다. 자바 일반 객체와 차이점은 없고.. 그냥 스프링 컨테이너에서 만들어진 자바 객체가 빈이다.
- DI(Dependency Injection) 의존관계 주입
  - 강한 결합: 객체 내부에서 다른 객체를 생성하는 것은 강한 결합도를 가지는 구조다. A클래스 내부에서 B라는 객체를 생성하고 있다면, B 객체를 C객체로 바꾸고 싶은 경우 A클래스도 수정해줘야 한다.
  - 느슨한 결합: 객체를 주입받는 다는 것은 외부에서 생성된 객체를 인터페이스를 통해서 넘겨받는 것이다. 이렇게 하면 결합도를 낮출 수 있고, 런타임시에 의존관계가 결정되기 때문에 유연한 구조를 가진다. 
- JPA Repository
  - [SpringBoot JPA 예제](https://jdm.kr/blog/121)
