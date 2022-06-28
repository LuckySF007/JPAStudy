# JPA 시작하기

- H2 Database를 사용해 실습

## 왜 H2 DataBase를 쓰나요?

1. 실습용으로는 최고의 DB
2. 웹용 쿼리툴을 제공함
3. MySQL, Oracle 데이터베이스 시뮬레이션 기능 제공
4. 시퀀스, AUTO INCREMENT 기능 제공
5. 가벼움(1.5M)

## pom.xml 작성

- maven dependency 설정

```
    <dependencies>
        <!-- JPA 하이버네이트 -->
        <dependency>
            <groupId>org.hibernate</groupId>
            <artifactId>hibernate-entitymanager</artifactId>
            <version>5.3.10.Final</version>
        </dependency>
        <!-- H2 데이터베이스 -->
        <dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
            <version>1.4.199</version>
        </dependency>
    </dependencies>
```

## persistence.xml

### 엔티티 신뢰 문제 해결

- 처음 실행하는 SQL에 따라 탐색 범위가 결정됨 EX) MEMBER TABLE에서 조회하고 Member member에서 member.getOrder() 하면 탐색할때 member까지만 쿼리로 가져왔기때문에 ORDER Table쪽 조회 불가해서 null뜸. 애초에 조인해서 다 가져왔어야함
- 그렇기때문에 엔티티 마다 신뢰성이 문제가 생김
- JPA는 알아서 쿼리를 보내서 member.getOrder() 가능케해줌 (지연로딩 즉시로딩과 관계있음)

### 1차캐싱, 그로인한 동일성 보장

```
  //mybatis
  Member member1 = memberDAO.getMember("100");
  Member member2 = memberDAO.getMember("100");
  member1 == member2; // 다르다.

  //JPA
  Member member1 = memberDAO.getMember("100");
  Member member2 = memberDAO.getMember("100");
  member1 == member2; // 같다.

```

- 같은 transaction 안에서는 이렇게 key가지고 조회할때 같은녀석이면 JPA는 알아서 캐싱해서
  같은녀석을 반환해주기 때문에 같다고 나옴
- 엄청 유의미하진 않지만 약간의 조회 성능 향상

### 지연로딩 즉시로딩

#### 지연로딩

```
  Member member = memberDAO.find(memberID); // SELECT * FROM MEMBER 쿼리발생
  Team team = member.getTeam();
  String teamName = team.getName();  // 실제 member->team으로 연관된 객체의 값 요구할때 SELECT * FROM TEAM 쿼리발생
```

#### 즉시로딩

- 지연로딩과 다르게 member객체에서 team을 거의 확정적으로 참조하는경우가 많은경우 JPA설정을통해 한번에 로딩하게 할 수 있음

```
  Member member = memberDAO.find(memberID); // SELECT * FROM MEMBER JOIN TEAM 쿼리발생.
  Team team = member.getTeam();
  String teamName = team.getName();
```
