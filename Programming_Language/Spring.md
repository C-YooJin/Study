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

### JPA
- JPA Repository
  - [SpringBoot JPA 예제](https://jdm.kr/blog/121)
- JPA는 자바 객체와 데이터를 맵핑시켜준다. Entity class 활용.
- Entity class
  - JPA의 Entity class는 데이터베이스에 저장하기 위해 유저가 정의한 class다.
  - DB와 자바객체를 맵핑해준다.
  - Annotation
    - :heavy_check_mark:@Entity: @Entity가 설정된 클래스를 엔티티 클래스라고 하며, @Entity가 붙은 클래스는 테이블과 매핑된다.
    - :heavy_check_mark:@Table: 엔티티와 관련된 테이블을 매핑한다. name속성을 사용하여 테이블과 매핑하는데, name을 생략하면 클래스 이름이 테이블 이름과 매핑된다. 다시 설명하자면 `@Table(name = "XXX")` 같은 형식으로 작성하면 이름을 다르게 해서 매핑이 가능하다는 것이다.
    - :heavy_check_mark:@Id: Entity 클래스의 필수 어노테이션이다. <b>이게 없는 엔티티 클래스는 JPA가 처리하지 못한다.</b> 일반적으로 키(primary key)를 가지는 변수에 선언한다.
    - :heavy_check_mark:@GeneratedValue: @Id가 선언된 필드에 기본 키를 자동으로 생성하여 할당할 때 사용한다. 다양한 옵션이 있지만 이걸 사용하면 데이터베이스에 따라서 자동으로 결정 된다. H2는 시퀀스를 이용하여 처리한다.
    - :heavy_check_mark:@Temporal: 날짜 타입의 변수에 선언하여 날짜 타입을 매핑할 때 사용한다. TemporalType의 DATE, TIME, TIMESTAMP중 하나를 선택할 수 있다.
    - :heavy_check_mark:@Column: @Column선언은 꼭 필요한 것은 아니다. 하지만, @Column에서 지정한 멤버 변수와 데이터베이스의 컬럼명을 다르게 하고 싶다면 `@Column(name="XXX")`같은 형식으로 작성하자. 디폴트는 기본적으로 멤버 변수명과 일치하는 데이터베이스의 컬럼을 매핑한다. 
  - ref. 갓대희님 티스토리: [[스프링부트 (3)] SpringMVC(2) Spring Boot View 설정 및 JSP 연동하기(Thymeleaf 추가)](https://goddaehee.tistory.com/204)
  - ref. JDM's blog: [스프링부트 JPA예제](https://jdm.kr/blog/121)
    
  
### POJO
- POJO (Plain Old Java Object)
  - pojo란 평범하고 오래 된 자바 객체라는 뜻이다. 왜 이런 이름이 붙었냐면, 사람들이 EJB(Enterprise Java Bean)만 사용하는 걸 보게 된 마틴 파울러라는 사람이 "평범한 자바 객체를 로직에 넣는 게 더 도움 될 때도 있는데, 사람들은 왜 EJB만 쓸까?"에 대한 생각을 하다가, 평범한 자바 객체는 EJB와 같은 이름이 없어서 라는 생각을 하게 됐다. 그래서 POJO라는 이름을 붙여줬다. 
  - 스프링도 pojo 프레임워크중 하나라고 볼 수 있다.
  - 특정 규약에 종속되지 않는 자바 객체
  - 스프링 애플리케이션 = POJO를 이용해서 만든 애플리케이션 로직 + POJO가 어떻게 관계를 맺고 동작하는지 정의해놓은 설계정보
  - ![spring](https://user-images.githubusercontent.com/30011635/87107102-df475400-c299-11ea-850e-4a767b3fac6d.png)
  - EJB 등에서 사용되는 Java Bean 이 아닌 Getter 와 Setter 로 구성된 가장 순수한 형태의 기본 클래스를 POJO라 하며, 이는 Spring에서 고안된 철학의 핵심적인 부분을 구성하는 요소로 사용된다

### Templates
- thymeleaf
  - 템플릿 엔진이다.
  - HTML, XML, JavaScript, CSS 및 일반 텍스트를 처리 할 수 있는 웹 및 독립형 환경에서 사용할 수 있는 Java 템플릿 엔진
  - 스프링 MVC패턴에서 V(view)를 담당 (꼭 뷰를 만들 때만 쓰는 건 아니다)
  - html 파일을 가져와서 파싱, 분석 후 정해진 위치에 데이터를 치환해서 보여준다.
  - jsp에 비해 속도가 느림
- `mvn package` : 패키징. jar를 만들어준다. 컴파일 된 결과물을 패키지 파일로 생성. 컴파일, 테스트, 빌드를 수행하여 패키지 파일을 생성. 
- MVC 패턴 (Model, View, Controller)
  - controller: Model과 View를 연결해주는 역할. springframework.ui.Model 라이브러리로 Model 설정해줌
### IoC (Inversion of Control)
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

#### 등록 된 bean을 어떻게 꺼내 쓰지?
<b> :heavy_check_mark: 1. Application Context 사용해서 꺼내기</b> <br>
<b> :heavy_check_mark: 2. @Autowired 어노테이션으로 꺼내기</b> <br>
  - 생성자를 통해서 직접 주입받는 것이 아니라, autowired라는 어노테이션으로 IoC 컨테이너에 등록된 bean을 주입 받아 사용할 수 있다.
  - Application Context로 직접 꺼내는 것 보다는 스프링이 제공하는 Dependency Injection 하는 방법. 즉, Autowired를 활용하는 경우가 많다. 
  - spring version 4.3부터 Autowired 생략 가능
  - Autowired는 생성자, 메소드, 멤버변수 위에 사용할 수 있다. 대부분은 멤버변수 위에 선언하여 사용한다.
  - 스프링 컨테이너는 멤버변수 위에 붙은 Autowired를 확인하는 순간 해당 변수의 타입을 체크한다. 그리고 그 타입의 객체가 메모리에 존재하는지를 확인한 후에, 그 객체를 변수에 주입한다.
  - 그런데 만약 @Autowired가 붙은 객체가 메모리에 없다면 컨테이너가 `NoSuchBeanDefinitionException`을 발생시킨다. 
  ![image](https://user-images.githubusercontent.com/30011635/89385247-47267880-d73a-11ea-9ce1-2f3dfaf45461.png)

### AOP (Aspect Oriented Programming) 
- 똑같은 코드인데 흩어져있는 코드들. 이걸 바꾸려면 일일이 찾아가서 바꿔줘야 되는 문제가 있음. 
- @Transactional 어노테이션
- AOP 구현 방법 <br>
:heavy_check_mark: 컴파일<br>
:heavy_check_mark: 바이트코드 조작<br>
:heavy_check_mark: 프록시 패턴<br>
프록시 패턴과 관련된 건 다음 시간에 ...

### DTO와 VO를 구분할 수 있는 아주 좋은 형태
:boom:get/set = DTO<br>
:boom:get = VO

### getter와 setter의 차이
ref. [getter와 setter 비유 굿](https://m.blog.naver.com/PostView.nhn?blogId=mdown&logNo=221315912263&proxyReferer=https:%2F%2Fwww.google.com%2F)
- getter: 데이터에 접근해서 가져오는 거
- setter: 데이터를 수정하는 것!
객체에 접근할 때, 원하는 데이터를 변수에 가지고 있는 클래스에 접근하고 싶을 때, 패키지가 다르면 접근이 불가능하다. 변수를 class.method()로 가져올 수 없다. 이런 경우 get메소드를 만들어서 해당 변수를 return 해주면 된다. B클래스가 A클래스에 있는 변수 title을 사용하고 싶다면 A클래스에 아래와 같이 getTitle 메소드를 만든다.
```
public String getTitle(){
	return title;
}
```
- Entity 클래스에는 setter를 절대 쓰면 안 된다. builder로 데이터를 생성해주자.
```
// 객체의 생성자 설정 (필드가 많을경우 롬복의 @Builder 사용하면 좋다)
@Builder
public Member(String username, String password, String name, String tel, Address address) {
        this.username = username;
        this.password = password;
        this.name = name;
        this.tel = tel;
        this.address = address;
    }
```

```
// 객체 생성 시 값 세팅(빌더패턴 사용)
Member member = Member.Builder()
      .username("name")
      .password("1234")
      .name("name);
      .tel("01012345677")
      .address(address)
      .build();
```

### Test Code (TDD)
테스트코드의 다섯가지 원칙
- F - Fast (테스트 코드를 실행하는 일은 오래 걸리면 안 된다.)
- I - Independent (독립적으로 실행이 되어야 한다.)
- R - Repeatable (반복 가능해야 한다.)
- S - Self Validating (매뉴얼 없이 테스트 코드만 실행해도 성공, 실패 여부를 알 수 있어야 한다.)
- T - Timely (바로 사용 가능해야 한다.)