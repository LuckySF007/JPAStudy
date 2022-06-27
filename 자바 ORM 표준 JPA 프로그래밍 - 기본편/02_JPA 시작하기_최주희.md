# 02.JPA 시작하기

## JPA 설정하기 - persistence.xml

- jpa 설정 파일 (/META-INF/persistence.xml)
- persistence-unit name으로 이름 지정
- javax.persistence로 시작 : JPA 표준 속성
- hibernate로 시작 : 하이버네이트 전용 속성

<br>

## 데이터베이스 방언 (dialect 속성)

- jpa는 특정 디비에 종속적이지 않음
- 방언 : sql 표준을 지키지 않는 특정 db만의 고유 기능

<br>

## JPA 구동방식

설정 정보 조회(persistence.xml) → EntityManagerFactory 생성 → EntityManager 여러개 생성

<br>

## 객체와 테이블을 생성하고 매핑

- @Entity : JPA가 관리할 객체
- @Id : 데이터베이스 pk와 매핑
- 엔티티 매니저 쓰레드간에 공유 x
- **JPA의 모든 데이터 변경은 트랜잭션 안에서 실행**

<br>

## JPQL

- JPA를 사용하면 엔티티 개체를 중심으로 개발하는데, 검색쿼리가 문제가됨
- 모든 데이터를 객체로 변환해서 검색하는 것은 불가능 → 애플리케이션이 필요한 데이터만 db에서 불러오려면 결국 검색조건이 포함된 sql이 필요
- JPQL은 엔티티 객체를 대상으로 쿼리 (객체지향 SQL)