## Spring
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
- POJO (Plain Old Java Object)
  - pojo란 평범하고 오래 된 자바 객체라는 뜻이다. 왜 이런 이름이 붙었냐면, 사람들이 EJB(Enterprise Java Bean)만 사용하는 걸 보게 된 마틴 파울러라는 사람이 "평범한 자바 객체를 로직에 넣는 게 더 도움 될 때도 있는데, 사람들은 왜 EJB만 쓸까?"에 대한 생각을 하다가, 평범한 자바 객체는 EJB와 같은 이름이 없어서 라는 생각을 하게 됐다. 그래서 POJO라는 이름을 붙여줬다. 
  - 스프링도 pojo 프레임워크중 하나라고 볼 수 있다.
  - 특정 규약에 종속되지 않는 자바 객체
  - 스프링 애플리케이션 = POJO를 이용해서 만든 애플리케이션 로직 + POJO가 어떻게 관계를 맺고 동작하는지 정의해놓은 설계정보
  - ![spring](https://user-images.githubusercontent.com/30011635/87107102-df475400-c299-11ea-850e-4a767b3fac6d.png)
  - EJB 등에서 사용되는 Java Bean 이 아닌 Getter 와 Setter 로 구성된 가장 순수한 형태의 기본 클래스를 POJO라 하며, 이는 Spring에서 고안된 철학의 핵심적인 부분을 구성하는 요소로 사용된다
- thymeleaf
  - 템플릿 엔진이다.
  - HTML, XML, JavaScript, CSS 및 일반 텍스트를 처리 할 수 있는 웹 및 독립형 환경에서 사용할 수 있는 Java 템플릿 엔진
  - 스프링 MVC패턴에서 V(view)를 담당 (꼭 뷰를 만들 때만 쓰는 건 아니다)
  - html 파일을 가져와서 파싱, 분석 후 정해진 위치에 데이터를 치환해서 보여준다.
  - jsp에 비해 속도가 느림
- `mvn package` : 패키징. jar를 만들어준다. 컴파일 된 결과물을 패키지 파일로 생성. 컴파일, 테스트, 빌드를 수행하여 패키지 파일을 생성. 
- MVC 패턴 (Model, View, Controller)
  - controller: Model과 View를 연결해주는 역할. springframework.ui.Model 라이브러리로 Model 설정해줌
- IoC (Inversion of Control)
  - "내가 사용할 의존성 누군가 알아서 주겠지" -백기선님 유튜브 스프링 부트 입문
  - IoC 컨테이너는 Application Context나 Bean Factory 같은 걸 사용하면 되는데 Application Context를 사용하면 된다. 그 이유는 Application Context가 Bean factory를 상속받고 있고, 다른 것들도 상속받고 있기 때문에 다양한 구현이 가능하기 때문이다.
- 일반 객체와 Bean
  - Bean: 객체인데 IoC 컨테이너가 관리하는 객체
  ```
  // 둘 다 같은 OwnerController
  
  // 일반 객체
  OwnerController ownerController = new OwnerController();
  // bean으로 주입 받은 객체. new로 해서 인스턴스를 생성해줄 필요가 없음. bean에 있는 걸 가져다 쓴다.
  OwnerController bean = applicationContext.getBean(OwnerController.class);
  ```
#### 어떻게 스프링 컨테이너 안에다가 bean을 만들어줄까?
#### 어떻게 어떤 특정한 instance를 bean으로 만들 수 있을까?
크게 두 가지 방법 있음 <br>
<b> :heavy_check_mark: 1. Component Scan</b> <br>

어노테이션 프로세서 중 스프링 ioc 컨테이너가 사용하는 여러가지 인터페이스가 있는데, 그런 인터페이스를 life cycle call back라고 부름. 여러가지 life cycle call back 중에, component 어노테이션을 찾아서, 즉 @Component가 붙어 있는 모든 class를 찾아서, 그 class에 있는 인스턴스를 bean으로 등록함.
```
@Component Scanning
	@Repository
	@Service
	@Controller
	@Configuration
```
등등 더 있음.. 직접 정의할 수도 있고. 이런 어노테이션들을 찾아서 bean으로 등록 해주는게 component scanning이다.

예를 더 들어보자면

```
@Controller
class OwnerController {

	...
}
```
이렇게 Controller 어노테이션을 붙여주면 <b>자동으로 bean으로 등록</b> 되는 것이다.

repository는 spring data jpa가 제공해주는 기능에 의해서 자동으로 bean으로 등록된다. 따라서 특정한 어노테이션을 붙이지 않아도 된다.<br>
<br>
<b> :heavy_check_mark: 2. 직접 xml이나 '자바설정파일'에 bean으로 등록하는 방법. 요즘 추세는 자바설정파일을 많이 씀.</b> <br>
VizConfig.java 파일 만들어서, 어떤 class위에 @Configuration이라는 어노테이션을 붙여주고, 그 안에 @Bean이라는 어노테이션을 붙여줌

```
@Configuration
public class VizConfig {
    
    @Bean
    public VizController vizController() {
        return new VizController();
    }
}
```
이런식으로. 그러니까 이게 뭐냐면. Configuration 파일에서 지금 Controller를 bean에 등록해줬기 때문에, VizController 클래스 위에 @Controller 붙여주지 않아도 된다는 말이다. 이 코드로인해 이미 Controller로 bean에 등록 됐기 때문에.

### Test Code (TDD)
테스트코드의 다섯가지 원칙
- F - Fast (테스트 코드를 실행하는 일은 오래 걸리면 안 된다.)
- I - Independent (독립적으로 실행이 되어야 한다.)
- R - Repeatable (반복 가능해야 한다.)
- S - Self Validating (매뉴얼 없이 테스트 코드만 실행해도 성공, 실패 여부를 알 수 있어야 한다.)
- T - Timely (바로 사용 가능해야 한다.)
