## JAVA
- Encoding & Decoding
  - Encoding: 문자, 기호들을 컴퓨터에 저장하거나 통신에 사용할 목적으로 <b>부호화</b> 하는 것이다. 인코더.
  - Decoding: <b>복호화</b> 인코딩 하기 전으로 되돌리는 처리 방식을 말한다. 디코더.
- JAVA 장점
  - 운영체제에 독립적이다. JVM에 의해 돌아가기 때문이다.
  - 객체지향 언어다.
  - 자동으로 메모리 관리해준다. JVM에서 Garbage Collector가 데몬 쓰레드로 돌아간다. 따라서 별도로 메모리 관리 해 줄 필요x
  - 오픈소스다. Oracle JDK와 OPEN JDK가 있는데, 보통 쓰는 건 후자. 오라클 jdk는 유료다.
  - 멀티스레드 구현에 용이하다. 자바는 스레드 생성과 관련된 라이브러리 API를 제공한다.
  - 동적 로딩(Dynamic Loading)을 지원한다.
- JAVA 단점
  - 속도가 비교적 느리다. 자바는 한 번의 컴파일링으로 실행 가능한 기계어가 만들어지지 않고, JVM에 의해 기계어로 번역되고 실행하는 과정을 거친다. C나 C++은 컴파일링 하면 바로 기계어로 번역되는데, 자바는 JVM 거쳐야돼서 더 느리다는 뜻.
  - 예외처리 불편
- 클래스 vs. 객체
  - 클래스는 '설계도', 객체는 '설계도로 구현한 모든 대상' 의미
- 객체 vs. 인스턴스
  - 클래스 타입으로 선언되었을 때 객체라고 부르고, 그 객체가 메모리에 할당되어 실제 사용될 때 인스턴스라고 부른다.
  - 객체는 현실세계에 가깝고, 인스턴스는 소프트웨어 세계에 가깝다.
  - 객체를 '클래스의 인스턴스' 라고 부르기도 함
  - '방금 인스턴스화하여 레퍼런스를 할당한' 객체를 인스턴스라고 말하지만, 이는 원본(추상적인 개념)으로 부터 생성되었다는 것에 의미를 부여하는 것일 뿐 엄격하게 객체와 인스턴스를 나누긴 어렵다.
- Overloading vs. Overriding
  - overloading(오버로딩): 두 메서드가 같은 이름을 갖고 있으나 인자의 수나 자료형이 다른 경우
  - overriding(오버라이딩):  상위 클래스의 메서드와 이름과 용례(signature)가 같은 함수를 하위 클래스에 재정의하는 것 / 상속 관계에 있는 클래스 간에 같은 이름의 메서드를 정의
- Call by Reference vs. Call by Value
  - Call by Value (값에 의한 호출)
    - 함수가 호출될 때, 메모리 공간 안에서는 함수를 위한 별도의 임시 공간이 생성된다.
    - 함수 호출시 인자로 전달되는 변수의 값을 복사하여 함수의 인자로 전달한다.
    - 복사된 인자는 함수 안에서 지역적으로 사용되는 local value의 특성을 가진다.
    - 따라서 함수 안에서 인자의 값이 변경되어도, 외부의 변수의 값은 변경되지 않는다.
  - Call by Reference (참조에 의한 호출)
    - 함수가 호출될 때, 메모리 공간 안에서는 함수를 위한 별도의 임시 공간이 생성된다.
    - 함수 호출시 인자로 전달되는 변수의 레퍼런스를 전달한다. (해당 변수를 가르킨다.)
    - 따라서 함수 안에서 인자의 값이 변경되면, 인자로 전달된 변수의 값도 함께 변경된다.
    
 ### Jackson 라이브러리
 java object를 JSON으로 변환하거나 JSON을 java object로 변환하는 데 사용하는 java 라이브러리
 
 ### ObjectMapper() 
 JSON파일이나 JSON형식으로 된 string을 파싱하는 역할을 한다.
 ```
 # pom.xml
 <dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.11.0.rc1</version>
 </dependency>
 ```
 
사용법은 아래
#### 1.1 Convert Java object to JSON, writeValue(...)
```
ObjectMapper mapper = new ObjectMapper();
User user = new User();

//Object to JSON in file 
mapper.writeValue(new File("c:\\user.json"), user); 

//Object to JSON in String 
String jsonInString = mapper.writeValueAsString(user);
```

#### 1.2 Convert JSON to Java object, readValue(...)
```
ObjectMapper mapper = new ObjectMapper(); 
String jsonInString = "{'name' : 'mkyong'}"; 

//JSON from file to Object 
User user = mapper.readValue(new File("c:\\user.json"), User.class); 

//JSON from String to Object 
User user = mapper.readValue(jsonInString, User.class);
```
 
 ### HikariCp
 - Database와 Connection Pool을 관리해준다.
 - 실제로 JDBC 커넥션을 맺는 과정은 상당히 복잡하고 자원을 많이 소모한다. 부하도 심하고.. -> hikaricp를 사용하면 미리 정해놓은 만큼에 커넥션을 pool에 담아두고, 요청이 들어오면 Thread가 커넥션을 요청하고, Hikari는 pool내에 있는 커넥션을 연결해준다. 그러면 Thread입장에서는 바로 쿼리를 날릴 수 있게 된다. 
- 일단 뭔가 JDBC 사용할 때 복잡&부하 큰 문제 해결하기 위해 있는 것이라고 알아두기.

### slf4j
- 자바의 로깅 관련 모듈.

### `private volatile string test = test;`
- Ref. [Java volatile이란?](https://nesoy.github.io/articles/2018-06/Java-volatile)
- java volatile 키워드는 java 변수를 Main Memory에 저장하겠다고 명시하는 것이다.
- 변수를 read 할 때, CPU cache에 저장 된 값이 아닌 Main Memory에서 읽는 것이다.
- write 할 때도 마찬가지로 Main Memory에 작성한다. 
#### 어떨 때 쓸까?
- Multi Thread환경에서 Thread가 변수 값을 읽어올 때 각각의 CPU cache에 저장된 값이 다르기 때문에 <b>변수 값 불일치</b>가 일어난다. 예를 들어, a라는 변수에 대해 한 쓰레드에서는 값을 읽고 더하고, 한 쓰레드에 대해서는 a를 읽기만 할 때 문제가 발생한다. 앞 쓰레드에서는 a값의 변형이 일어나지만(cache메모리로 가져와서 작업한다), 뒷 쓰레드는 변형되기 전(Main Memory에 있는) a값을 가져오기 때문이다. 이런 경우 변수 a에 대해 Main Memory에서 직접 read & write 한다면 문제 없다. 
- `volatile`이 가장 적합한 상황: 멀티쓰레드 환경에서 한 쓰레드는 read & write 하고, 나머지는 read만 하는 경우
- 여러 쓰레드에서 write를 하는 경우에는 적합하지 않다. 연산 후 main memory에 반영되기 전 다른 쓰레드에서 read 하고 write 해버린다면 값의 오차가 생긴다. 자세한 건 위 ref 블로그 참고.

### enum 열거형 (JDK 1.5 up)
- 클래스처럼 보이게 하는 상수
- 서로 관련 있는 상수들을 모아 심볼릭한 명칭의 집합
- Enum클래스형을 기반으로 한 클래스형 선언
```
<EnumExample.java>
public emun Example {
  WALKING, RUNNING, TAEKONDO
}
```
- 값들은 대문자로 적어준다.

### extends (상속)
- 사실 extends가 상속의 대표적인 형태다.
- 부모의 메소드를 그대로 사용할 수 있으며 오버라이딩 할 필요 없이 부모에 구현되있는 것을 직접 사용 가능하다.
```
class Vehicle {
  protected int speed = 3;
  
  public int getSpeed(){
    return speed;
  }
  public void setSpeed(int speed){
    this.speed = speed;
  }
}

class Car extends Vehicle{
  public void printspd(){
    System.out.println(speed);
  }
}

public class ExtendsSample {
  public static main (String[] args){
    Car A = new Car();
    System.out.println(A.getSpeed());
    A.printspd();
  }
}
```
car 클래스는 Vehicle을 상속 받았다.

### implements (상속)
- 자바는 다중 상속을 지원하지 않는다. `public class Son extends Father, Mother{...}` 이것이 불가능 하다는 것이다.
- 근데 implements는 다중 상속을 가능하게 해 줌. 일단 아래부터 보자.
```
interface TestInterface{
  public static int num = 8;
  public void fun1();
  public void fun2();
}

class InterfaceExam implements TestInterface{
  @Override
  public void fun1(){
    System.out.println(num);
  }
  
  @Override
  public void fun2() {
    
  }
}

public class InterfaceSample{
  public static void main(String args[]){
    InterfaceExam exam = new InterfaceExam();
    exam.fun1();
  }
}
```
#### implements의 가장 큰 특징은 이렇게 부모의 메소드를 반드시 오버라이딩(재정의)해야 한다.
- 그리고 `public class Son implements Father, Mother{...}`를 가능하게 해준다. extends에서는 다중 상속이 안 돼서 요게 안 됨.

### Thread
- 동시성과 병렬성을 구분하자
  - 동시성: 하나의 코어(single core)에서 여러개의 쓰레드가 동작하는 것
  - 병렬성: 여러개의 코어(multi core)가 돌아가는 것
- `Runnable 인터페이스` : 별도의 thread 객체 생성 후 start() 메소드를 호출한다.
```
// 보통 이런식으로 많이 사용한다. 
Thread thread = new thread(new Runnable() {
              public void run() {
                작업 내용;
               }
});
```
#### :sparkles: 정독 합시다 :sparkles:
Q. 쓰레드 인스턴스를 생성하고 나서, start 메소드를 호출하면 run 메소드가 실행되는데, run 메소드를 직접 호출하면 안 되나? <br>
A. run 메소드를 직접 호출하는게 "불가능" 한 건 아니지만 의미가 없달까. <b>run을 바로 호출해봤자 쓰레드의 생성으로 이어지진 않음.</b><br>
쓰레드는 자신만의 메모리 공간을 할당 받아서 별도의 흐름을 형성하는데, 그래서 start()를 호출해 주는 거거든. start()를 호출하면 쓰레드를 실행하기 위한 '기반'이 마련되고, 그 다음에 run()메소드를 대신 호출해주는 역할을 한다. <br>
<br>
Q. CPU가 하나인데 어떻게 둘 이상의 쓰레드가 동시에 실행 가능한가요? <br>
A. 모든 쓰레드는 CPU를 공유한다. 쓰레드를 동시에 실행하려면 멀티쓰레딩을 하는 거고.. <br>
참고로 CPU 코어가 여러개인 경우 쓰레드 각각에 코어가 하나씩 할당되어 실행되기도 한다. <br>
<br>
Q. main 메소드가 종료되어도 쓰레드는 실행을 계속 하나요? 그리고 쓰레드는 run 메소드의 실행이 완료되면 종료 되나요?<br>
A. 쓰레드의 main메소드가 run메소드다. start 메소드를 호출한다고 해서 main메소드가 종료되는 건 아니다. main메소드도 하나의 쓰레드처럼 스스로 나름대로 실행 흐름을 이어간다. main메소드가 종료되어도 실행 중에 있는 쓰레드가 있다면, 프로그램은 종료되지 않는다. 즉, 남은 쓰레드까지 실행을 완료해야 프로그램은 종료 된다. <br>
<br>
Q. 정확히 무얼 가르켜 쓰레드라 하는가?<br>
A. 별도의 실행흐름(쓰레드)를 형성하기 위해서 자바 가상머신에 의해 만들어지는 (또는 준비되는) 모든 리소스와 각종 정보들을 총칭해서 쓰레드라 한다. 
  - 참고로, 쓰레드를 생성하기 위해서는 '메모리 할당', 'CPU를 나눠쓰기 위한 각종 정보 등록' 등의 작업들이 필요하다. 이것들 또한 쓰레드라는 것..
  
  
### ArrayBlockingQueue
- Array로 구현 된 Blocking Queue다. 추가되는 아이템은 순서가 있으며, FIFO를 따른다.
- queue에 담을 수 있는 아이템의 갯수가 한정 된다.
- Queue에서 아이템을 가져올 때 비어있으면 null을 리턴하지 않고, Queue에 아이템이 채워질 때 까지 기다린다.
- 아이템을 추가할 때 Queue가 꽉 차 있으면 공간이 생길 때 까지 기다린다.
- Exception이 발생하거나 일정 시간 기다릴 수 있음
- 멀티 쓰레드 환경에서 사용하기 위해 구현 됐다.
- 사용방법
```
int capacity = 10;
ArrayBlockingQueue<Integer> queue = new ArrayBlockingQueue<Integer>(capacity);
```

### Generic
- 자바 7 이전 버전에서는 `Map<String, String> map = new HashMap<String, String>();`
- 자바 7부터는 `Map<String, String> map = new HashMap<>();`

### List와 ArrayList의 차이가 뭔지 모르겠어서 검색해 본 결과물
- 인터페이스 List 대신에 구현 클래스 ArrayList의 형타입을 알 수 있다면 더 편리하게 사용할 수 있습니다. (낮게 나는 새가 더 자세히 본다)
- 구현 클래스 ArrayList 대신에 인터페이스 List를 사용하면 더 많은 형타입을 받아 들일 수 있습니다. (높게 나는 새가 더 멀리 본다.)
- 예를들어, 목록의 모든 원소를 출력하는 메서드 `public void printAll(List items)`는 `public void printAll(ArrayList items)` 보다 더 많은 종류의 형타입을 받아 들일 수 있습니다. (Vector, Set, etc)

### POI
엑셀 파일 다루는 라이브러리

### Launch4j
exe파일 만드는 라이브러리

### ? 연산자
- `a ? b : c`: a가 True면 b 실행, False면 c실헹

### 접근 제한자
- 객체의 멤버에 대한 접근을 제한할 때 사용하는 것

### HashMap
![image](https://user-images.githubusercontent.com/30011635/105696777-17b53380-5f47-11eb-93b0-f950f84a2e11.png)
```
HashMap<String,String> map1 = new HashMap<String,String>();//HashMap생성
HashMap<String,String> map2 = new HashMap<>();//new에서 타입 파라미터 생략가능
HashMap<String,String> map3 = new HashMap<>(map1);//map1의 모든 값을 가진 HashMap생성
HashMap<String,String> map4 = new HashMap<>(10);//초기 용량(capacity)지정
HashMap<String,String> map5 = new HashMap<>(10, 0.7f);//초기 capacity,load factor지정
HashMap<String,String> map6 = new HashMap<String,String>(){{//초기값 지정
    put("a","b");
}};
```

### What is difference between Selenium and Jsoup in JAVA
- 일단 알아둘 것 -> 백그라운드에서 HTTP Request/Response가 이루어지며, Request를 던졌을 때 웹 서버에서 응답한 결과를 받아온다. 따라서 서버사이드 렌더링(SSR)을 사용하는 웹 사이트는 서버에서 렌더링을 한 후 화면을 그리기 때문에 크롤링이 가능하지만, 클라이언트 사이드 렌더링(CSR)을 사용하는 웹 사이트는 최소한의 페이지만 서버에서 렌더링하고 클라이언트(브라우저)에서 화면을 그리기 때문에 HTTP Request로 실제 브라우저에서 보여지는 화면을 스크랩 할 수 없다. 
- Selenium
  - 웹 어플리케이션 자동화 툴, 현재 브라우저에 출력된 페이지 소스를 파싱할 수 있다
  - xPath 지원
  - CRS 사용한 웹사이트 크롤링 가능
  - 속도 느림 (브라우저가 렌더링 된 후 페이지를 파싱하기 때문에)
- Jsoup
  - 서버사이드 렌더링 웹사이트만 크롤링 가능함. CRS 불가. 뭐, 불가는 아니지만 한계가 있음.
  - xPath 지원 안 함
  - 속도 빠름 
#### 결론: Selenium은 Jsoup의 몇 가지 단점을 커버하지만, 동적 웹페이지가 아니라면 Jsoup을 이용하는 것이 낫다. 셀레니움 느리니까. (실무에서도 경험한 부분)
