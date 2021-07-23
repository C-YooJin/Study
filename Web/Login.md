### RSA, public key cryptosystem
- 공개키 (puclic key)
- 개인키 (private key)
- 공개키 --> 개인키 (암호화)
- 개인키 --> 공개키 (전자서명)
- 기본적으로 A와 B가 있다고 가정할 때, A->B로 문서를 전달한다고 하면, B의 공개키로 문서를 잠근다. (그럼 B가 본인의 개인키로 열어볼 수 있음)
- 또한, A->B로 문서 전달시, A의 개인키로 문서를 잠그면 B는 A의 공개키로 문서를 열어볼 수 있다.
- 좀 더 응용해서 A->B로 문서 전달시, 1차적으로 B의 공개키로 문서를 잠그고, 그 문서를 A의 개인키로 또 다시 잠글 수 있다. 이런 상황에서 B가 해야 될 일은
  - 첫 번째, A의 공개키로 열어본다 (열리지 않을시 인증되지 않은 문서이기 때문에 버리면 됨) <b> [인증] </b>
  - 두 번째, B의 개인키로 열어본다  <b> [암호화] </b>
    - 이 상황은 인증과 암호화를 모두 거친 RSA다.

### [웹 기준] 로그인, 회원가입 구현할 때 Spring security와 firebase중 어떤 걸 쓰는 게 더 좋을까? 에서 시작 된 스터디
- [Firebase Authentication vs. Spring Security](https://stackshare.io/stackups/firebase-authentication-vs-spring-security)
- Firebase와 Spring Security 둘 다 "User Management and Authentication tool" 임
- Firebase
  - An App Authentication System in a few lines of code
- Spring Security
  - A powerful and Highly customizable authentication and access-control framework
  - It is a framework that focuses on providing both authentication and authorization to Java applications
- JWT -> Json Web Tokens
- 파이어베이스가 BaaS인데.. 스프링으로 백엔드 구현하는데 BaaS 써야되는 이유는? 그냥 Spring Security 쓰면 될듯..?

### Websocket, UDP(received message 구현)

### jwt 토근을 활용한 사용자 인증
- [jwt 토근 기반 인증](https://webcoding-start.tistory.com/50)
- :star: [[SpringBoot] SpringBoot로 SpringSecurity 기반의 JWT 토큰 구현하기](https://mangkyu.tistory.com/57) :star:

### 인증과 인가 (OAuth) (우아한 Tech톡 루피님 강연)
[[10분 테코톡] 루피의 인증과 인가](https://www.youtube.com/watch?v=JZgD8aPkHSc) <br>
회원가입과 로그인 -> 나의 정보를 등록하고 내가 누구인지 인증하는 과정이다. <br>
- 인증(Authentication) : 보호된 리소스에 접근하는 것을 허용하기 이전에 등록된 유저의 신원을 입증(Validating) 하는 과정 
- 인가(Authorization) : 요청된 리소스에 접근할 수 있는 권한이 있는 인증(authenticated) 된 유저인지 입증(validating)하는 과정 <br>
인증이 있은 후에 인가가 있다. 
#### 생각해 볼 만한 것
1. 인증 되었지만 권한이 없다 --> 인가x
2. 인가 되었지만 인증은 되지 않았다 --> 개소리

### 인증과 인가 (OAuth를 제외한 나머지) (우아한 Tech톡 토니님 강연)
[[10분 테코톡] 토니의 인증과 인가](https://www.youtube.com/watch?v=y0xMXlOAfss) <br>
- 인증 하기 : Request Header
  - 유저 ID가 존재 -> Encoding -> 해당 문자열을 Request Header에 삽입 -> 서버가 DB 체킹을 해서 해당 아이디, 비번이 존재하는지 확인 -> OK 사인 전송
- 인증 유지하기 : Browser
- 안전하게 인증하기 : Server
- 효율적으로 인증하기 : Token

### Spring security + Oauth2 + jwt
- [Ref 1. Spring Security 와 OAuth 2.0 와 JWT 의 콜라보](https://velog.io/@tmdgh0221/Spring-Security-%EC%99%80-OAuth-2.0-%EC%99%80-JWT-%EC%9D%98-%EC%BD%9C%EB%9D%BC%EB%B3%B4)

![image](https://user-images.githubusercontent.com/30011635/120022508-768ad680-c027-11eb-8733-b4aab1bfb346.png)

#### OAuth 2.0
- Resource owner: 개인정보 소유자 (유저 A)
- Client: 제 3의 서버로부터 인증받고자 하는 서버. 즉, 직접 개발한 사이트 그 자체! 
- Resource Server: 개인정보를 저장하고 있는 서버. (구글, 카카오, 네이버 등..)
<br>
- Client ID: Resource Server에서 발급해주는 ID. 웹 사이트 X에 구글이 할당한 ID를 알려주는 것이다.
- Client Secret: Resource Server에서 발급해주는 PW. 웹 사이트 X에 구글이 할당한 PW를 알려주는 것이다.
- Authorized Redirect Uri: Client 측에서 등록하는 Url. 만약 이 Uri로부터 인증을 요구하는 것이 아니라면, Resource Server는 해당 요청을 무시한다.

#### jwt에 대하여
- 단점
  - 사용자 인증 정보가 필요한 리소스를 요청 할 때 헤더에 jwt정보를 입력해서 보내야 하는데, 네트워크 부하가 일어날 수 있다.
  - 토큰 자체에 사용자 정보를 담고있기 때문에 jwt 만료전에 탈취당하면 정보가 유출 될 수 있다. (보안)
  - jwt는 한 번 만들어져서 클라이언트에 전달되면 수정할 방법이 없기 때문에 만료기한을 꼭 잘 명시해줘야한다. 
- 장점
  - 서버가 확장되어도 모든 서버가 세션정보를 갖고있지 않아도 된다. 서버 수와 상관 없이 jwt 인증 방법을 알고 있다면 ok
  - 웹과 앱간의 쿠키 세션 처리에도 유용하다.
    - 브라우저와 앱에서의 쿠키 처리 방식이 다르기 때문에, jwt를 쓰면 유용한거지.

#### 전체적인 큰 그림
![IMG_0586](https://user-images.githubusercontent.com/30011635/120057432-ec219180-c07d-11eb-9342-03a9629204b8.jpg)
유저(리소스 오너)가 우리 서비스(client)에서 로그인을 시도한다 = HTTP request를 보낸다 -> 구글이나 카카오같은 Oauth를 제공하는 사이트(즉, 리소스 서버)애 해당 정보가 등록되고 Access 토근이 발급된다.-> 이제부터 client에서 리소스 서버에 로그인을 요청할 떄 마다 즉, 유저A의 인증이 필요할 때 마다 Access Token을 이용하여 접근한다.

#### jwt를 활용한 로그인 프로세스
- jwt는 claim 기반 -> claim이란 사용자 정보
1. 사용자가 Auth server를 통해 로그인을 시도한다.
2. 서버가 사용자 인증을 마치면 jwt 토큰을 사용자에게 전달한다.
3. 이 다음부터는 사용자가 서버에 리소스를 요청할 때 마다 (즉, HTTP request 할 때 마다) 헤더에 jwt값을 넣어서 요청을 보낸다.
4. 이를 전달 받은 서버는 jwt를 통해 사용자를 인증하고, 리소스를 전달한다. 

[Ref 1. JWT & Spring Security](https://brunch.co.kr/@springboot/491)
