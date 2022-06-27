# 01. JPA 기본 1

## SQL 중심적인 개발의 문제점

- 어플리케이션은 객체지향 언어를 사용하지만, SQL을 더 많이 작성하게됨
    
    → 여러 문제점 발생
    
    - CRUD 반복 작성
    - 컬럼 수정시 모든 SQL문 수정 불가피
- 패러다임의 불일치
    - 객체를 SQL로 변환하여 관계형 데이터베이스(RDB)에 저장해야함.
- 객체와 관계형 데이터베이스의 차이
    - 상속 : DB에 저장될 객체에는 상속관계가 없다.
    - 연관관계 : 객체는 참조, DB는 PK, FK사용
    - 문제점 : 객체지향적으로 설계시 맵핑작업이 복잡해진다.
    - 객체를 자바 컬렉션에 저장하듯 DB를 사용 → JPA

## JPA란?

- **Java Persistence API**의 약자

### ORM

- Object-relational mapping(객체 관계 맵핑)
- 객체는 객체대로, 관계형 DB는 관계형 DB대로 설계하고, 중간에 ORM프레임 워크가 맵핑을 해준다.

### JPA CRUD

```java
/* 저장 */
jpa.persist(member)

/* 조회 */
Member member = jpa.find(memberId)

/* 수정 */
member.setName("변경할 이름")

/* 삭제 */
jpa.remove(member)
```

### JPA의 장점

- 유지보수 : 컬럼 추가시 필드만 추가해도 SQL은 JPA가 처리해줌
- JPA와 패러다임의 불일치 해결
    - JPA가 Join을 통해 상속을 해결해줌
- 자유로운 객체 그래프 탐색
- 동일한 트랜잭션에서 조회한 엔티티는 같음을 보장

### JPA의 성능 최적화 기능

1. 1차 캐시와 동일성(identity) 보장
    - 같은 트랜잭션 안에서는 같은 엔티티 반환 - 약간의 조회 성능 향상
    - DB Isolation Level이 Read Commit이어도 어플리케이션에서 Repeatable Read보장
2. 트랜잭션을 지원하는 쓰기 지연(transactional write-behind)
    - 트랜잭션을 커밋할 때까지 Insert SQL을 모음
    - JDBC BATCH SQL 기능을 사용해서 한번에 SQL 전송
3. 지연 로딩(Lazy Loading)과 즉시로딩
    - 지연로딩 : 객체가 실제 사옹될 때 로딩
    - 즉시 로딩 : Join SQL로 한번에 연관된 객체까지 미리 조회
    
    위 2방식을 옵션 하나로 변경이 가능하다.