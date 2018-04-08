# JPA

## Entity

### Lifecycle
![Lifecycle](http://cfile21.uf.tistory.com/image/233A5A475551AB561749D3)

#### New(비 영속 객체)

- Entity 객체가 DB에 반영되지 않았고, Managed 상태가 아닌 상태를 말한다. 이 상태는 new 키워드를 사용해 생성한 Entity 객체를 말하고 영속화되지 않는다.
- 일반 Java Entity Instance를 Save하지 않고 새로 생성된 상태를 말한다.

#### Managed(영속 객체)

- Entity 객체가 영속 객체가 된 상황은 크게 2가지가 있다.
- New (비 영속 객체) 상태에서 persist 메소드를 이용해 저장한 경우와 DB 테이블에 저장되어 있는 데이터를 find 메소드 또는 query를 사용해 조회한 경우다.
- 이 상태는 Persistence Context가 관리하는 상태이며, 해당 객체를 수정했는지(자동 변경 감지) 알아낼 수 있다.

#### Removed(삭제 객체)

- Managed 상태인 객체를 remove 메소드를 이용해 삭제한 경우에 Removed (삭제 객체) 상태에 해당한다. 작업 단위가 종료되는 시점에 실제로 DB 테이블에 삭제가 동기화 된다. 이 상태에 객체는 작업 단위가 종료되는 동시에 DB에서 삭제되므로 재사용하면 안된다.


#### Detached(준 영속 객체)

- 트랜잭션이 commit되었거나, clear, flush 메소드가 실행된 경우 Managed (영속 객체) 상태의 객체는 모두 Detached (준 영속 상태) 상태가 된다.
- 이 상태는 더 이상 DB와 동기화를 보장하지 않는다. 다시 Managed (영속 객체) 상태로 만들기 위한 merge 메소드가 존재한다.

### 주의사항

- Managed(영속상태) 의 객체 수정은 Transacion 종료 시점에 DB에 반영 되므로, Entity 객체의 수정은 주의가 필요하다.

## Join

### 다중성

- 연관 관계에 대한 표현
- JPA에서는 Annotation 형태로 표현한다
- 종류
    + 일대일(@OneToOne)
    + 일대다(@OneToMany)
    + 다대일(@ManyToOne)
    + 다대다(@ManyToMany)

### 단방향/양방향

- 테이블은 외래키 하나로 조인을 사용해서 양방향 쿼리가 가능하므로 방향 개념이 없음
- 하지만 객체에서는 참조 여부에 따라 방향성이 존재
    + 한 쪽만 참조하는 것이 단방향
    + 서로 참조하는 것이 양방향

### 연관관계의 주인

- 데이터베이스 관점에서는 FK 하나만으로 설정 가능
- 하지만 엔티티 관계에서는 방향성에 따라 주인이 존재
- 외래키가 있는 엔티티 쪽이 일반적으로 연관관계의 주인

### 미리보는 Select Manual

- JPQL 을 이용한 Query 작성
- Native SQL 을 이용한 Query 작성
- Java Source 내에서  for(...) 등을 이용한 직접적인 연결

## 다중성에 따른 JPA

### 다대일

- 일(1) 대 다(N) 관계에서는 외래키는 항상 다 쪽에 존재
- 따라서 객체 양방향 관계에서 연관관계의 주인은 항상 다(N)
    + 예) 회원(N)과 팀(1)이 있으면 회원 쪽이 연관관계의 주인
- JoinColumn을 통해서 대상 엔티티에서 어떤 컬럼을 FK로 삼을지 표현
```java
@Entity
public class Member {
    @Id
    @GeneratedValue
    private Long id;

    private String username;

    @ManyToOne
    @JoinColumn(name = "TEAM_ID")
    private Team team;

    // getter, setter
}
```
- mappedBy를 사용하는 쪽은 연관관계에 있어 주인 쪽이 아니다.
- 연관관계의 방향성에 따라 @OneToMany(mappedBy = "team") 관계 설정은 필요 없을 수 있음
```java
@Entity
public class Team {
    @Id
    @GeneratedValue
    private Long id;

    private String name;

    @OneToMany(mappedBy = "team")
    private List members = new ArrayList<>();

    // getter, setter
}
```

### 일대일

- 일대일 관계에서도 외래키가 존재하는 쪽이 주인이 됨
- JPA 설정 개념은 다대일과 같음 (@OneToOne 을 사용)

```java
@Entity
public class Member {
    @Id
    @GeneratedValue
    private Long id;

    private String username;

    @OneToOne
    @JoinColumn(name = "TEAM_ID")
    private Team team;

    // getter, setter
}
```
```java
@Entity
public class Team {
    @Id
    @GeneratedValue
    private Long id;

    private String name;

    @OneToOne(mappedBy = "team")
    private List members = new ArrayList<>();

    // getter, setter
}
```

### 다대다

- 일반적인 경우에는 단방향/양방향 설정 모두 일대일/일대다 경우와 동일
    + 사용하는 어노테이션이 @ManyToMany 일 뿐
- 다만, 단순한 연관관계 설정만이 아니라 관계에 대해 추가 정보(컬럼)이 필요하면 연결 엔티티를 사용
    + 사용자, 상품 엔티티가 있고 사용자가 상품을 주문하는 관계가 있을 경우 수량, 주문일 등의 정보가 필요한 경우
    + 위의 상황에서는 연결 엔티티인 주문 엔티티가 사용자, 상품 엔티티와 각각 다대일 관계를 맺게 되는 것
    + 주문엔티티에서 상품 엔티티의 키와 상품 엔티티의 키를 복합 키로 사용할 수도 있고 별도의 대체 키를 만들어서 주 키로 사용할 수 있음

```java

@Entity
public class Meeting {
    @Id
    @Column(name="id")
    @GeneratedValue(strategy=GenerationType.AUTO)
    private int id;   

    @Column(name="name")
    private String name;    // ...   

    @OneToMany(mappedBy = "meeting")
    private List participationList = new ArrayList<>();
}
```
```java
@Entity
public class User {
    @Id
    @Column(name="id")
    private int id;

    @Column(name="name")
    private String name;   

    @Column(name="password")
    private String password;    // ...   

    @OneToMany(mappedBy = "user")
    private List participationList = new ArrayList<>();
}
```
```java
@Entity
@IdClass(ParticipationId.class)
public class Participation{
    @Id
    @ManyToOne
    @JoinColumn(name = "meeting_id")
    private Meeting meeting;

    @Id
    @ManyToOne
    @JoinColumn(name = "user_id")
    private User user;    // ...
}
```
```java
public class ParticipationId implements Serializable {
    private int meeting;
    private int user;   

    public ParticipationId() { }

    public ParticipationId(int meeting, int user) {
        this.meeting = meeting;
        this.user = user;
    }
}
```
```java
public interface ParticipationRepository extends CrudRepository<participation, participationid=""> { }</participation,>
```

- JPA 복합 키의 제약조건
    + 별도의 식별자 클래스로 만들어야 함
    + Serializable 을 구현
    + equals 와 hashCode  메소드를 구현
    + 기본 생성자가 있어야 함
    + 식별자 클래스는 public 이어야 함
