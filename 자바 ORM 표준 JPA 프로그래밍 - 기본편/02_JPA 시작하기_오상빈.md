# JPA 시작하기

- H2 Database를 사용해 실습

## 왜 H2 DataBase를 쓰나요?

1. 실습용으로는 최고의 DB
2. 웹용 쿼리툴을 제공함
3. MySQL, Oracle 데이터베이스 시뮬레이션 기능 제공
4. 시퀀스, AUTO INCREMENT 기능 제공
5. 가벼움(1.5M)

## pom.xml 작성

- hibernate(5.3.10.Final)
- H2 DataBase(1.4.199)
- 실무에서 SpringBoot를 적용하기때문에 Spring Docs를 참조하여 버전 설정했음

## persistence.xml

- resources/META-INF 에 작성해야함
- persistence 설정

## 데이터베이스 방언

- JPA는 어느 특정 데이터베이스에 종속X
- 이를 해결하기 위해 persistence.xml 설정에 dialect 속성에서 사용 DB지정해줌

```
  name="hibernate.dialect" value="org.hibernate.dialect.H2Dialect" // H2
  name="hibernate.dialect" value="org.hibernate.dialect.Oracle10gDialect" // Oracle
  name="hibernate.dialect" value="org.hibernate.dialect.MySQL5InnoDBDialect" // MySQL
```

## JPA 구동방식

1. Persistence가 persistence.xml 설정 정보를 조회
2. EntityManagerFactory를 생성
3. Factory에서 EntityManager 생성

### 주의

- 엔티티 매니저 팩토리는 하나만 생성해서 어플리케이션 전체에서 공유
- 엔티티 매니저는 사용 후 버림 (쓰레드간 공유X)
- JPA의 모든 데이터 변경은 트랜잭션 안에서 이루어져야 함
- try catch finally를 통해 try에서 tx.commit() 도중 에러가 발생하면 catch블럭에서 tx.rollback()
  finally에서 사용한 엔티티 매니저를 close()하는 식으로 하는것이 정석임

## JPQL

- JPA는 엔티티 객체를 중심으로 개발함. 이때, 검색쿼리또한 테이블이아닌 엔티티 객체를 중심으로 검색
- 이를위해 JPA는 SQL을 추상화한 JPQL이라는 객체 지향 쿼리 언어를 제공함
- SQL문법과 유사
- JPQL은 엔티티 객체를, SQL은 DB 테이블을 대상으로 쿼리
- 한마디로 JPQL은 객체 지향 SQL임
