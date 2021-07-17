### 패러다임 불일치 (객체와 데이터베이스의 차이점, 기존 JDBC API의 불편함)
- 상속
- 연관관계
- 객체그래프 탐색
- 비교
  - 데이터베이스: 기본 키 값으로 각 row 비교
  - 객체: 동등비교(`==`) 즉, 주소값 비교 / `equals()` 메소드를 사용한 객체 내부 값 비교
  
  
### 영속성 컨텍스트
- flush: 트랜잭션을 커밋하는 순간, 영속성 컨텍스트에 새로 저징 된 엔티티를 데이터베이스에 반영한다. 
- `em.find()` 를 호출하면 먼저 1차 캐시에서 엔티티를 찾고, 만약 없으면 DB에서 조회한다.
  - DB에서 데이터를 조회하는 경우, 조회 된 값을 영속성컨테스트(안에 있는 1차 캐시에)에 저장한다.  
```
EntityManager em = emf.createEntityManager();
EntityTransaction transaction = en.getTransaction();
// 엔티티 매니저는 데이터 변경 시 트랜잭션을 시작해야 한다.
transaction.begin(); // [트랜잭션] 시작

em.persist(memberA)
em.persist(memberB)
// 여기까지 INSERT SQL을 데이터베이스에 보내지 않았다.

transaction.commit();
// 커밋하는 순간 데이터베이스에 INSERT SQL을 보낸다.
```
