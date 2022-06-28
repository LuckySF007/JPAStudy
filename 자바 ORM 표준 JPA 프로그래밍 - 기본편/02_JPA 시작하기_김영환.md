# JPA 기본 2

## JPA 프로젝트 생성

1. DB 스택을 정하고, 올바르게 설치한다.
2. 프로젝트를 생성한다. (Maven or Gradle)
   1. pom.xml을 수정한다.
      1. dependency를 추가한다.
3. JPA 설정을 진행한다.
   1. persistence.xml 파일을 생성한다. (File Path : <u>src/main/resources/META-INF/persistence.xml</u>)
      1. 데이터베이스 정보, hibernate 정보 등을 설정한다.



## hibernate.dialect

- JPA는 특정 데이터베이스에 종속되지 않기에, 각각의 DB가 갖는 고유 기능에 따른 차이를 극복하기 위해 사용한다.



## EntityManagerFactory

- 하나만 생성한다.
- 애플리케이션 전체에서 공유된다.



## EntityManager

- Thread 간 공유를 하면 안된다.
- 사용 후 버린다.



## Transaction

- JPA의 모든 데이터 변경은 트랜잭션 안에서 일어난다.



## JPQL

- 단순 조회는 `EntityManager.find(type, obj)`를 통해 진행할 수 있다.

- 작업이 복잡해지는 경우 SQL 사용이 필요할 수 있는데, 이때 JPQL을 사용할 수 있다.

- 예제 (조회)

  ~~~java
  // JPQL
  List<Member> result = em.createQuery("select m from Member as m", Member.class).getResultList();
  
  for (Member member : result) {
    System.out.println("member name = " + member.getName());
  }
  ~~~

- JPA를 사용하면 엔티티 객체를 중심으로 개발하게 되는데, 쿼리를 사용하면 문제가 되지 않는가?

  - 검색을 할 때, 테이블이 아닌 엔티티 객체를 대상으로 검색하는 로직이 자동으로 구성된다.

- 즉, JPQL은 JPA가 SQL을 추상화한 것으로 객체 지향 쿼리 언어를 제공한다.

### JPQL과 SQL의 차이

- JPQL은 엔티티 객체를 대상으로 쿼리를 날린다.
- SQL은 데이터베이스 테이블을 대상으로 쿼리를 날린다.
