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
- [JPA는 도대체 뭘까?](https://velog.io/@adam2/JPA%EB%8A%94-%EB%8F%84%EB%8D%B0%EC%B2%B4-%EB%AD%98%EA%B9%8C-orm-%EC%98%81%EC%86%8D%EC%84%B1-hibernate-spring-data-jpa)
- 참고로 JPA는 스프링에서 제공하는 게 아니고 자바에서 제공하는 persistence api다.
- JPA Repository
  - [SpringBoot JPA 예제](https://jdm.kr/blog/121)
- JPA는 자바 객체와 데이터를 맵핑시켜준다. Entity class 활용.
- Entity class
  - JPA의 Entity class는 데이터베이스에 저장하기 위해 유저가 정의한 class다.
  - DB와 자바객체를 맵핑해준다.
  - Annotation
    - :heavy_check_mark:@Entity: @Entity가 설정된 클래스를 엔티티 클래스라고 하며, @Entity가 붙은 클래스는 테이블과 매핑된다. @Entity 있으면 무조건 "아 이건 jpa가 맵핑한다!"고 생각하면 됨
    - :heavy_check_mark:@Table: 엔티티와 관련된 테이블을 매핑한다. name속성을 사용하여 테이블과 매핑하는데, name을 생략하면 클래스 이름이 테이블 이름과 매핑된다. 다시 설명하자면 `@Table(name = "XXX")` 같은 형식으로 작성하면 이름을 다르게 해서 매핑이 가능하다는 것이다.
    - :heavy_check_mark:@Id: Entity 클래스의 필수 어노테이션이다. <b>이게 없는 엔티티 클래스는 JPA가 처리하지 못한다.</b> 일반적으로 키(primary key)를 가지는 변수에 선언한다. 걍 pk 맵핑해주는 어노테이션
    - :heavy_check_mark:@GeneratedValue: @Id가 선언된 필드에 기본 키를 자동으로 생성하여 할당할 때 사용한다. 다양한 옵션이 있지만 이걸 사용하면 데이터베이스에 따라서 자동으로 결정 된다. H2는 시퀀스를 이용하여 처리한다. `@GeneratedValue(strategy = GenerationType.IDENTITY)` 해주면 디비가 알아서 생성해줌.. id값을 하나씩 ++해서 저장해줌.
    - :heavy_check_mark:@Temporal: 날짜 타입의 변수에 선언하여 날짜 타입을 매핑할 때 사용한다. TemporalType의 DATE, TIME, TIMESTAMP중 하나를 선택할 수 있다.
    - :heavy_check_mark:@Column: @Column선언은 꼭 필요한 것은 아니다. 하지만, @Column에서 지정한 멤버 변수와 데이터베이스의 컬럼명을 다르게 하고 싶다면 `@Column(name="XXX")`같은 형식으로 작성하자. 디폴트는 기본적으로 멤버 변수명과 일치하는 데이터베이스의 컬럼을 매핑한다. 
  - ref. 갓대희님 티스토리: [[스프링부트 (3)] SpringMVC(2) Spring Boot View 설정 및 JSP 연동하기(Thymeleaf 추가)](https://goddaehee.tistory.com/204)
  - ref. JDM's blog: [스프링부트 JPA예제](https://jdm.kr/blog/121)
  - Jpa Repository -> 메소드로 데이터를 이러쿵 
#### <스프링 기본편, JPA> 김영한님
- 2015년 이전 JPA가 한국에 제대로 상륙하지 않은 이유는 국내에 문서가 잘 없었어서..!
- JPA도 스프링만큼 기술적인 넓이와 깊이가 있는 기술이다
- 스프링에서도 JPA를 굉장히 많이 지원하고.. 스프링은 그냥 JPA를 기본으로 깔고 들어간다고 생각하면 된다.
- properties
  - spring.jpa.show=true 추가해주면 jpa가 날리는 sql을 로그로 볼 수 있다.
  - spring.jpa.hibernate.ddl-auto=none 추가해주면 jpa를 보면 회원객체를 보고 테이블을 다 만들어준다.. 만약 테이블이 다 만들어져 있고 만들이진 걸 쓸거면 이건 일단 none으로 설정해주면 된다. none 말고 create 하면 테이블 자동으로 만들어줌!
- JPA를 쓰려면 일단 entity라는 걸로 맵핑을 해줘야 된다.
- jpa는 그냥 인터페이스다. 그냥 표준 진영이랄까.. 그리고 구현체는 여러 업체들이 있지만 보통은 하이버네이트로 한다.
- ORM (Object Relational database table을 Mapping)
    
  
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
  - 주석
    - 기본적인 html 주석: `<!-- 어쩌구 -->`
    - 정적인 페이지에서는 주석 처리지만 타임리프 처리가 되면 브라우저에 노출 되지 않는 주석
      - `<!--/* comments */-->`
      - `<!--/*--><div>정적일 때만 나타나는 화면</div><!--*/-->`
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
  
  ```
  package com.어쩌구.저쩌구;

  import org.springframework.stereotype.Controller;
  import org.springframework.web.bind.annotation.GetMapping;

  @Controller
  public class BoardController {

    @GetMapping("/")
    public String list() {
        return "board/list.html";
    }

    @GetMapping("/post")
    public String post() {
        return "board/post.html";
    }
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
- 스프링 빈은 기본으로 <b>싱글톤</b>으로 등록한다. 따라서 같은 스프링 빈이면 모두 같은 인스턴스다. 특별한 경우가 아닌 이상 대부분 싱글톤을 사용한다.

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
  - <b>setter를 쓰면 안 되는 이유는 엔티티값이 쉽게 변경되면 안 되기 때문이다.</b>
  - JPA Entity class에서 setter를 사용하면 안 되는 이유는 엔티티값이 쉽게 변경되면 안 되기 때문이다.
  - 객체를 생성할 때는 3가지 방법중 하나를 사용합니다. -> 생성자, 정적 팩토리 메서드, builder패턴 -> [관련해서 김영한님 인프런 강의에 질문과 답변](https://www.inflearn.com/questions/16235)
- <font color = "red"> <b>엔티티 클래스는 Domain 영역에 들어간다. </b> </font>
- <b>DTO -> 데이터 전달 객체</b>
- <b>Entity -> DB 저장 객체</b>

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
- Dto에서 필요한 @getter @setter @ToString @NoArgsConstructor를 한꺼번에 해주는 어노테이션 -> @Data

### Test Code (TDD)
테스트코드의 다섯가지 원칙
- F - Fast (테스트 코드를 실행하는 일은 오래 걸리면 안 된다.)
- I - Independent (독립적으로 실행이 되어야 한다.)
- R - Repeatable (반복 가능해야 한다.)
- S - Self Validating (매뉴얼 없이 테스트 코드만 실행해도 성공, 실패 여부를 알 수 있어야 한다.)
- T - Timely (바로 사용 가능해야 한다.) <br>
<font color="red"> Junit, given-when-then 패턴으로 먼저 공부, 각 레이어에 대한 유닛테스트와 전체 api에 대한 인테그레이션 테스트 (http test) 공부 방법으로 </font>
- 테스트는 실행되고 끝날 때 마다 저장소를 지워줘야된다. 테스트 코드를 한꺼번에 실행 시킬 경우, 어떤 테스트가 먼저 실행될지 알 수 없다. 즉, 순서를 보장하지 않는다는 뜻. 테스트는 순서, 의존관계 없이 설계 돼야 한다. 
```
// 테스트코드 실행 후 저장소에 데이터 삭제해주는 코드
@AfterEach
public void afterEach) {
	repository.clearStore();
}
```
- 테스트코드 메소드명은 과감하게 한글로 바꿔도 된다. 
```
// 이런식으로..
@Test
void 회원가입() {
}
```
- given, when, then 패턴
- given -> 
- when -> 뭘 검증할거냐?
- then -> 검증부 -> Assertions로 해주자. assertj 라이브러리의 클래스.  
  

### JPA auditing 
중복 되는 코드를 좀 더 효율적으로 짜도록 도와준다. 특히 게시물 수정 시간 같은 것..!
[JPA auditing 기능이란](https://webcoding-start.tistory.com/53)

```
// 테스트 코드
@Test
    public void BaseTimeEntity_등록 () {
        // given
        LocalDateTime now = LocalDateTime.of(2020, 9, 04, 21, 56, 00);
        postsRepository.save(Posts.builder()
                .title("title")
                .content("content")
                .author("author")
                .build());
```

```
// BaseTimeEntity 코드
package com.deepjin.book.springboot.domain.posts;

import lombok.Getter;
import org.springframework.data.annotation.CreatedDate;
import org.springframework.data.annotation.LastModifiedDate;
import org.springframework.data.jpa.domain.support.AuditingEntityListener;

import javax.persistence.EntityListeners;
import javax.persistence.MappedSuperclass;
import java.time.LocalDateTime;

@Getter
@MappedSuperclass
@EntityListeners(AuditingEntityListener.class)
public abstract class BaseTimeEntity {

    @CreatedDate
    private LocalDateTime createdDate;

    @LastModifiedDate
    private LocalDateTime modifiedDate;
}

```

```
// Application.java에 annotation 추가
package com.deepjin.book.springboot.domain.posts;

import lombok.Getter;
import org.springframework.data.annotation.CreatedDate;
import org.springframework.data.annotation.LastModifiedDate;
import org.springframework.data.jpa.domain.support.AuditingEntityListener;

import javax.persistence.EntityListeners;
import javax.persistence.MappedSuperclass;
import java.time.LocalDateTime;

@Getter
@MappedSuperclass
@EntityListeners(AuditingEntityListener.class)
public abstract class BaseTimeEntity {

    @CreatedDate
    private LocalDateTime createdDate;

    @LastModifiedDate
    private LocalDateTime modifiedDate;
}

```

### 서버 템플릿 엔진 vs. 클라이언트 템플릿 엔진
- 서버 템플릿 엔진
  - 서버에서 DB 혹은 API에서 가져온 데이터를 미리 정의된 Template에 넣어 html을 그려서 클라이언트에 전달해주는 역할을 합니다. 즉, HTML 코드에서 고정적으로 사용되는 부분은 템플릿으로 만들어두고, 동적으로 생성되는 부분만 템플릿에 소스 코드를 끼워넣는 방식으로 동작합니다. 
  - JSP, Freemarker
- 클라이언트 템플릿 엔진
  - 음, 이건. vue.js, React.js 처럼 자바스크립트로 된 프레임워크들로 뷰를 표현할 때. 자바스크립트는 브라우저 위에서 작동한다. 코드가 이미 서버 사이드를 떠나서 브라우저에서 실행된다는 것. 따라서 서버에서 제어할 수 없다.
  
### Spring actuator
- 스프링부트 애플리케이션에서 제공하는 여러가지 정보, 상태를 모니터링 할 수 있는 기능
-> spring actuator admin과 함께 사용하면 UI로 편하게 볼 수 있다.

### Thread pool executor
- 스레드풀을 편하게 관리하게 해주는 클래스

### @ResponseBody
- http에는 header부와 body부가 있는데, body단에 이 데이터를 직접 넣어주겠다는 뜻이다.
```
@GetMapping("hello-string")
@ResponseBody
public String helloString(@RequestParam("name") String name) {
	return "hello"+ name;
}
```
- 자바 객체를 JSON/XML 형식으로 변환해서 Body에 실어 전송할 수 있음

### @RequestBody
- 요청으로 들어온 JSON/XML을 자바 객체로 변환해서 전달 받을 수 있음

### Controller
- `model.addAttribute("key", value)` 컨트롤러에서 return해주는 view에 "key"값을 전달해주는 역할을 한다.

### Service
- 실제 비즈니스 로직을 구현하는 부분

### @Controller와 @RestController 차이
- @Controller 
  - 보통 view를 반환하기 위해 씀
- @RestController
  - JSON 형태로 객체 데이터를 반환하기 위해 씀
  - api 컨트롤러 같은 느낌
  
### HttpStatus.OK and HttpStatus.ACCEPTED
- HttpStatus.OK : 200ok는 리퀘스트가 성공했음을 의미한다. 응답결과는 리퀘스트 메소드에 따라 다르다.
- HttpStatus.ACCEPTED: 202 Accepted는 리퀘스트가 프로세싱되기 위해서 억셉트 되었다는 뜻. 그러나 프로세싱이 완벽하게 끝난 건 아니다. 리퀘스트는 아직 진행중일지도 아닐지도 모른다.
  
### @PostMapping
```
@PostMapping(path = "/members", consumes = "application/json", produces = "application/json")
public void addMember(@RequestBody Member member) {
    //code
}
```  
  
### @JsonProperty
- jackson 라이브러리를 import 해야 사용할 수 있다
- [Jackson라이브러리 이해하기](https://mommoo.tistory.com/83)

### JPA
- [Spring Boot JPA - 시작 및 기본 설정](https://goddaehee.tistory.com/209)

### JPA를 쓸 때 왜 Entity클래스와 Dto클래스를 따로 만들까? builder도 따로 있음.. 이해 안 돼... 에서 시작된 공부
- Entity클래스란 JPA에서 직접 DB에 접근하는 클래스다
- Entity 클래스로 디비에도 접근하고 view단에도 뿌려주려면 약간 문제가 있다..
  - 양방향으로 연결 된 Entity는 순환 참조 문제가 발생한다
  - Entity가 변경 되거나 무거운 양의 데이터를 들고 여러 영역을 넘나들어야 되는 문제점이 있다 -> 성능상 안 좋음
- 실제 DB와 mapping되고 데이터의 저장, 수정, 조회, 삭제에 대해 데이터를 관리하고 보관하는 Persistence Layer까지는 Entity를 사용
- Service 영역에서부터 클라이언트 영역까지는 DTO를 사용합시다!

![image](https://user-images.githubusercontent.com/30011635/96969713-b51a5900-154d-11eb-8b59-13a7b4670909.png)

#### Reference
- [JPA 리파지터리, 데이터 저장하기](https://cloudstudying.kr/lectures/440)
- [스프링과 DAO, DTO, Repository, Entity](https://velog.io/@agugu95/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%8C%A8%ED%84%B4%EA%B3%BC-DAO-DTO-Repository)
- [DAO와 Repository / DTO / VO](https://kkambi.tistory.com/30)
- [Builder 기반으로 객체를 안전하게 생성하는 방법](https://cheese10yun.github.io/spring-builder-pattern/)
- [스프링에서 JPA 사용하기](https://velog.io/@swchoi0329/Spring-Boot%EC%97%90%EC%84%9C-JPA-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)
- [[Spring] Boot와JPA(Mysql)을 이용한 Rest API 간단 예제](https://cjw-awdsd.tistory.com/24)

### After Covid Project
- DAO -> DB에 접근해서 CRUD를 좀 더 편하게 해주는 작업. 만약 JPA를 사용한다면 JpaRepository가 DAO가 된다.
- DTO -> 멤버변수는 private 으로, public getter/setter 필수
- DTO(Data Transfer Object)는 이름과 같이 계층 간 데이터 교환을 위해 사용하는 객체다.
  - :rotating_light: 여기서 말하는 계층이란, View - Controller - Service - DAO와 같은 각 계층을 말한다.
- getter, setter는 데이터를 오브젝트로 변경해주는 메소드다. 그치 맞지.. 메소드로 불러올 수 있게 해주니까..

### application.yml h2-database 부분
```
spring:
  h2:
    console:
      enabled: true
```

#### hibernate.ddl-auto 옵션 정리
- none: 아무 명령도 실행하지 않음 (대부분의 데이터베이스의 기본값)
- create: 어플리케이션 실행시 (Session Factory실행 시) 기존의 테이블을 drop하고 새로 생성
- create-drop: 시작할 때는 create와 동일하고 종료될 때 (SessionFactory종료) drop을 실행한다. in-memory 데이터베이스에서는 이것이 기본값이다. 따라서 해당 옵션을 설정하지 않으면 H2 database는 어플리케이션 재시작시 이전의 데이터는 없어지게 된다.
- <b>update: 변경된 Scheme만 적용하고 데이터는 그대로 유지한다. -> 서비스 운영중에 테이블의 Schema가 종종 변경하게 된다. 이럴 경우 기존에는 직접 ALTER TABLE을 이용하여 변경된 Schema를 변경하지만 이 옵션을 정의하여 주면 @Entity에 추가된 값에 대해 자동으로 Schema를 변경하여 준다.</b>
- validate: Schema validation만 수행

### @Transactinal 어노테이션
- INSERT , UPDATE , DELETE 쿼리를 수행 할 때는 트랜잭션을 필수적으로 명시를 해줘야 합니다.

### 웹, MVC패턴에서 Entity class(DAO)와 Dto
- entity가 있는데 왜 굳이 Dto 클래스를 만들어줘야 되는지??? 
  - 일단 내가 알기론, Entity 클래스는 말 그대로 DB에 접근하는 낮은 단계에서 의미가 있는 클래스고, view에 데이터를 뿌려주기 위해서는 Dto 클래스가 필요하다. 그리고 이것을 ModelMapper가 연결해준다...???
- View에서 표현하는 속성값들은 요청에 따라 계속 달라질 수 있는데, 그 때마다 Entity의 속성값들이 변하게 되면 학생이라는 영속성 모델을 표현한 Students 클래스의 순수성이 모호해지게 된다.

### h2-database 초기화
- 웹개발을 하다가 새로운 프로젝트를 실행시켰는데 h2-console에서 SELECT 해 보니 이 전 프로젝트에서 생성한 컬럼이 그대로 남아있었다. 초기화가 필요하다고 생각했고 찾아 본 결과물 링크 첨부.
  - [h2-database초기화](https://roeldowney.tistory.com/271)

### 웹소켓
[Ref 1. [번역] Spring-WebSocket](https://velog.io/@hanblueblue/%EB%B2%88%EC%97%AD-Spring-4-Spring-WebSocket)
[Ref 2. Spring Boot, PostgreSQL을 이용한 RESTful API, WebSocket 구현](https://nashorn.tistory.com/entry/Spring-Boot-PostgreSQL%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-RESTful-API-%EA%B5%AC%ED%98%84)
