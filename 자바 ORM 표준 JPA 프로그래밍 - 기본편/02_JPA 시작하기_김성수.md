# JPA 시작하기

### library 버전

- spring boot - reference 확인
- dependencies
    - h2 driver version 일치

### JPA 설정

- JPA 설정 파일 : persistence.xml
- /META-INF/persistence.xml → 기본 위치 준수
- javax.persistence로 시작 : JPA 표준 속성
- hibernate로 시작 : 하이버네이트 전용 속성

### 데이터베이스 방언

- JPA는 특정 데이터베이스에 종속 X
- 각각의 데이터베이스가 제공하는 SQL 문법과 함수는 조금씩 다름
- 방언 : SQL 표준을 지키지 않는 특정 데이터베이스만의 고유한 기능

### JPA 구동 방식

1. Persistence.Class 설정 정보(META-INF/persistence.xml을 읽어 EntityManagerFactory.class 생성
2. EntityManagerFactory.class 는 필요할 때 마다 EnityManager 생성

### 객체와 테이블 생성/매핑

- @Entity : JPA가 관리할 객체
- @ID : 데이터베이스 PK와 매핑

### EntityManagerFactory

- 딱 한 개만 생성 애플리케이션 전체에서 공유

### EntityManager

- 쓰레드간 공유 x(사용 하고 버려야함)

### JPA 모든 데이터 변경은 Transaction 안에서 실행해야함!!

### JPQL

- 테이블이 아닌 객체를 대상으로 검색하는 객체 지향 쿼리
- SQL을 추상화 해서 특정 데이터베이스 SQL에 의존 X
- JPQL : 객체지향 SQL