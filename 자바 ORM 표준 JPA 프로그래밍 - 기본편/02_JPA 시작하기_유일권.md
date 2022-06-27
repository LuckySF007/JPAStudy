# 02. JPA 시작하기

## J**PA 설정하기**

### pom.xml

- hibernate-entitymanager
- h2database(DB에 따라 변동)

### **persistence.xml**

- JPA 설정 파일
- /resources/META-INF/persistence.xml 위치(위치 준수)
- persistence-unit name 으로 이름 지정
- javax.persistence로 시작 : JPA 표준 속성
- hibernate로 시작 : 하이버네이트 전용 속성

### 데이터 베이스 방언(dialect)

- JPA는 특정 DB에 종속되지 않음
- DB마다 제공하는 문법이 대동소이함
- DB 방언 : SQL 표준을 지키지 않은 특정 DB만의 고유 기능
- persistence.xml의 hibernate.dialect에서 DB를 지정하면 JPA가 알아서 방언에 맞춰 처리

## JPA 구동방식

1. persistence.xml의 설정정보 조회
2. EntitiyManagerFactory 생성
3. EntityManager 생성

### 객체와 테이블 생성하고, 맵핑하기

- @Entity : JPA가 생성하고, 관리할 객채
- @Id : PK선언
- @Table(name=”테이블 명”) : 테이블 명이 다른 경우
- @Column(name=”컬럼 명”) : 컬럼명이 다른 경우
- JPA의 데이터 변경은 Transaction안에서 해줘야함
- **주의점**
    - EntitiyManagerFactory는 하나만 생성
    - EntityManager는 사용후 반환, 쓰레드간 공유 금지

## JPQL이란?

- 특정 조건의 데이터를 검색하는 경우 JPA활용이 복잡함.
- JPQL은 엔티티 객체를 대상으로 쿼리, SQL은 데이터베이스 테이블을 대상으로 쿼리
- Select, From, Where, Group By, Having, Join등 지원