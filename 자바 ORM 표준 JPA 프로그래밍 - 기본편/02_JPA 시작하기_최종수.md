# JPA 시작하기

## Hello JPA - 프로젝트 생성

### H2 데이터베이스 설치와 실행

- 가볍다.
- 웹용 쿼리툴 제공
- MySQl, Oracle 데이터베이스 시뮬레이션 기능
- 시퀀스, AUTO INCREMENT 기능 지원
- error : [Database "C:/Users/joung/test" not found, either pre-create it or allow remote database creation (not recommended in secure environments)](http://39.115.231.15:8082/login.do?jsessionid=b6cd2aabcb4aadce5916ea3467bfdc35#)
    - 해결 방법 : 실행되었던 h2 데이터베이스를 강제 종료후 재실행, 최초 접속 때만 생성 가능한 것으로 보인다. 한 번 오류가 났다면 껐다 켜야 할 것.

### 메이븐 소개

- 자바 라이브러리, 빌드 관리
- 라이브러리 자동 다운로드 및 의존성 관리
- 최근에는 Gradle이 점점 유명

### 프로젝트 생성

- 자바 8 이상
- 메이븐 설정
- 프로젝트 생성시 Maven archetype 이 아닌 new project에서 maven select
    - Maven archetype : 메이븐에서 미리 만들어놓은 프로젝트 트리(구조)

### 라이브러리 추가 - pom.xml

- 나중에 스프링 부트에서 사용할 때 → 스프링 부트 버전 체크 → Reference Doc. → org.hibernate 검색 → 버전확인
- h2데이터베이스 다운로드 받은 것과 버전 체크(현재 버전 : 2.1.214)

### JPA 설정하기 - persistence.xml

- JPA 설정 파일
- /resources/META-INF/persistence.xml 위치
- persistence-unit name 으로 이름 지정
- javax.persistence로 시작 : JPA 표준 속성
- hibernate로 시작 : 하이버네이트 전용 속성

### 데이터베이스 방언

- JPA는 특정 데이터베이스에 종속 X
- 각각의 데이터베이스가 제공하는 SQL문법과 함수는 조금씩 다름
    - 가변 문자 : MySQL은 VARCHAR, Oracle은 VARCHAR2
    - 문자열을 자르는 함수 : SQL 표주는 SUBSTRING(), Oracle은 SUBSTR()
    - 페이징 : MySQL은 LIMIT, Oracle은 ROWNUM
- 방언 : SQL 표준을 지키지 않는 특정 데이터베이스만의 고유 기능
- 결과적으로 hibernate.dialect 속성에 지정 → 알아서 데이터베이스에 맞춰서 방언 지원
- 40가지 이상의 데이터베이스 방언 지원
- hibernate.show_sql : DB에 넘어가는 SQL구문을 볼것인가 말것인가, true or false

## Hello JPA - 애플리케이션 개발

### JPA 구동 방식

1. persistence 설정 정보 조회
2. EntityManagerFactory 생성
3. EntityManager들 생성

### 객체와 테이블을 생성하고 매핑하기

- 에러 : hibernate.properties not found → 자바 11 에서 발생하는 에러
    - 해결 방법 :  pom.xml에 추가
    
    ```
    <dependency>
        <groupId>javax.xml.bind</groupId>
         <artifactId>jaxb-api</artifactId>
        <version>2.3.0</version>
     </dependency>
    ```
    
- @Entity: JPA가 관리할 객체
- @ID: 데이터베이스 PK와 매핑
- JPA에서 데이터를 변경하는 단위는 transaction에서 해줘야 한다.
- transaction try catch 문 안에서 → 나중에 spring boot에서 다 해준다.
- @Table(name = “user”) : 테이블 명이 다를 경우
- @Column(name = “~~~”) : 컬럼 명이 다를 경우
- 수정은 따로 저장을 하지 않아도 된다. JAVA Collection에 저장 생각

### 주의

- 엔티티 매니저 팩토리는 하나만 생성
- 엔티티 매니저는 쓰레드간에 공유 X(사용하고 버려라)
- **JPA의 모든 데이터 변경은 트랜잭션 안에서 실행**

### JPQL 소개

- 가장 단순한 조회 방법
    - EntityManager.find()
    - 객체 그래프 탐색(a.getB().getC())
- 나이가 18살 이상인 회원을 모두 검색하고 싶다면?
- JPQL로 전체 회원 검색
    - createQuery(”select m from Member as m”, Member.class).getResultList();
    - setFirstResult().setMaxResults() : 페이징 처리 간단, 방언 처리 가능
- 검색 쿼리가 문제
- 검색 할 때도 테이블이 아닌 엔티티 객체를 대상으로 검색
- 결국 검색 조건이 포함된 SQL이 필요
- SQL을 추상화한 객체 지향 쿼리 언어 제공
- SELECT, FROM, WHERE, GROUP BY, HAVING, JOIN 지원
- JPQL은 엔티티 객체를 대상으로 쿼리, SQL은 데이터베이스 테이블을 대상으로 쿼리
- 한마디로 객체 지향 SQL