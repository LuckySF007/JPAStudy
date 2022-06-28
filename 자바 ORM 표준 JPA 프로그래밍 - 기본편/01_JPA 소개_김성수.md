# JPA 소개

## 목표 : 객체와 테이블을 제대로 설계하고 Mapping

- 객체를 관계형 데이터베이스에 저장

### SQL중심적인 개발의 문제점

- CRUD의 반복
- SQL에 의존적인 개발을 피하기 어렵다.
- 객체를 SQL로 바꾸기 위해 SQL작성해야 함(SQL Mapping)

### 객체와 관계형 데이터베이스의 차이점

- 상속
- 연관 관계(참조 vs 외래 키)
- 데이터 타입
- 데이터 식별 방법

> 객체를 객체 답게 설계할수록 Mapping 작업만 증가.
> 

> 객체를 자바 컬렉션에 저장 하듯이 DB에 저장할 수는 없을까 ??
> 

<br>

### JPA(Java Persistence API)

- 자바 진영의 ORM 기술 표준
- 인터페이스의 모음

### ORM(Object-relational mapping) 객체 관계 매핑

- 객체는 객체대로 , RDB는 RDB 답게 설계
- ORM framework가 중간에서 Mapping
- Java application과 JDBC 사이에서 동작
- 패러다임 불일치 해결!!

### JPA를 왜 사용해야 하는가?

- SQL 중심적인 개발에서 객체 중심으로 개발
- 생산성 : 코드가 간결
- 유지 보수
- 패러다임 불일치 해결
    - 상속, 연관 관계 해결
    - 객체 그래프 탐색
    - 신뢰할 수 있는 entity, 계층
    - 동일한 Transaction에서 조회한 entity는 같음을 보장
- 성능
    - 1차 캐시와 동일성(identity) 보장
    - transaction을 지원하는 쓰기 지연(transactional write-behind)
    - 지연 로딩(Lazy Loading) : 객체가 실제 사용될 때 로딩
- 데이터 접근 추상화와 벤더 독립성
- 표준