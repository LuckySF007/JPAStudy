# JPA 기본 1

## 데이터 베이스의 세계

- 현재는 Oracle, MySQL과 같은 관계형 DB의 세상
  - 즉, SQL 중심적인 개발로 돌아갈 수밖에 없다.
- CRUD SQL을 무한 반복해서 짠다는 것에 대한 회의감...



## 객체와 관계형 DB의 차이

### 상속

- 객체 상속 관계와 유사한 Table 슈퍼/서브 타입 관계를 사용
- DB에 저장할 객체에는 상속 관계를 사용하지 않는다.
  - SQL 매핑 작업이 중노동이 될 수 있기 때문에

### 연관관계

- 객체는 참조 사용
- 관계형 DB는 FK 사용

### 문제점

- 객체 지향적으로 설계할수록 번잡한 매핑 작업만 늘어나게 된다.

### 해결책

- 객체를 자바 컬렉션에 저장 하듯이 관계형 DB를 사용하는 방법을 고안했다.
  - 이것이 JPA다.



## JPA란?

- Java Persistence API

- 자바 진영의 ORM 기술 표준

  > ORM이란?
  >
  > Object-relational mapping (객체 관계 매핑)
  >
  > 객체는 객체대로, 관계형 DB는 관계형 DB대로 설계하고 ORM 프레임워크가 이를 중간에서 매핑하는 구성을 갖는다.

- JDBC API를 내장하고 있다.

### Hibernate

- JPA 구현체로, 오픈소스다.



## JPA CRUD

### Persist (Insert)

~~~java
jpa.persist(o1);
~~~

### Find

~~~java
jpa.find(o1);
~~~

### Set (Modify)

~~~java
jpa.setVariable(o1);
~~~

### Remove

~~~java
jpa.remove(o1);
~~~



## JPA 장점

### 유지보수

- JPA를 사용하면 새로운 컬럼 추가 시 필드만 추가하면 된다.
- 나머지 SQL 동작은 JPA가 알아서 처리한다.

### 객체와 관계형 DB의 불일치를 해결

- 개발자가 DB 구조에 대해 신경쓰지 않아도 되도록 구성되어 있다.
- 예를 들어, `pizza`가 `food`를 상속한다고 할 때, `jpa.persist(pizza);`를 통해 `pizza`를 저장하면 `food`와 `pizza` 테이블에 값을 각각 추가해 조회 시 성능 문제를 해결했다.
- 동일 Transaction에서 조회한 엔티티는 동일함을 보장한다.

### JPA의 성능 최적화

- 1차 캐시와 동일성(identiry) 보장
  - 같은 트랙잭션 안에서는 같은 엔티티를 보장 -> 조회 성능 향상 (캐싱을 통해)
    - 같은 트랜잭션이라는 짧은 시간동안 캐싱이 가능하기에 큰 성능 향상을 기대하기는 힘들다.
- 트랜잭션을 지원하는 쓰기 지연 (버퍼링)
  - JDBC BATCH SQL 기능을 사용해서 한번에 SQL을 전송/처리하는 것이 가능해진다.
    - begin, commit 명령을 통해 가능

### 즉시 로딩과 지연 로딩

- 지연 로딩 : 객체가 실제 사용될 때 로딩된다.
- 즉시 로딩 : Join SQL로 한번에 연관된 객체까지 미리 조회한다.
- 지연로딩과 즉시로딩은 옵션 하나로 on/off 가능하기에 편리하다.
