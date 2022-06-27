# 01.JPA 소개

## SQL 중심적인 개발의 문제점

- SQL에 너무 의존적
    - CRUD를 반복적으로 작성해야함
    - 컬럼에 변경이 있을 경우 sql문 다 수정해줘야함
    
- 객체와 관계형 데이터베이스의 차이
    - 상속 : DB에 저장할 객체에는 상속관계 안쓴다
    - 연관 관계 : 객체는 참조를 사용, 테이블은 외래키를 사용
    - 객체답게 모델링할수록 매핑 작업만 늘어남(객체지향적으로 설계할수록) → 객체를 자바 컬렉션에 저장하듯이 db에 저장하는 방법을 만든 것이 JPA
    

<br>

## JPA 소개

- ORM (Object-relational mapping, 객체 관계 매핑)
    - 객체는 객체대로 설계하고 관계형 db는 관계형 db대로 설계
    - ORM 프레임워크가 중간에서 매핑
- 생산성
    - 저장 : jpa.persist(member)
    - 조회 : jpa.find(memberId)
    - 수정 : member.setName(”name”)
    - 삭제 : jpa.remove(member)
- 유지보수 : 컬럼 추가 시 자바 필드만 추가하면 됨. sql문은 수정안해도 JPA가 처리
- JPA와 상속(조회) : jpa.find(Album.class, albumId) → JPA가 조인 sql문으로 조회
- 자유로운 객체 그래프 탐색
- 동일한 트랜잭션에서 조회한 엔티티는 같음을 보장

```java
String memberId = "100";
Member member1 = jpa.find(Member.class, memberId);  //조회
Member member2 = jpa.find(Member.class, memberId);  //캐시

member1 == member 2; //true
```

- JPA의 성능 최적화 기능
    - 1차 캐시와 동일성(identity) 보장
    - 트랜잭션을 지원하는 쓰기 지연 (insert) : 트랜잭션을 커밋할때까지 모든 insert문을 모아서 JDBC BATCH SQL 기능으로 한번에 전송
    - 지연 로딩과 즉시 로딩
        - 지연 로딩 : 객체가 실제 사용될 때 로딩
        - 즉시 로딩 : 조인 sql로 한번에 연관된 객체까지 미리 조회