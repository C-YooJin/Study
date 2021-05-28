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
스프링 ㄱ시큐리티 존나어렵다..욕나온다 ㅅㅂ 탈모각

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
