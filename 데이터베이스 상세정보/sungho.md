# DB 상세정보
## ORM (Object Relational Mapping)
- 객체와 관계형 DB의 데이터를 자동으로 매핑해주는 것
  - 객체 지향 프로그래밍은 클래스를 사용하고, 관계형 데이터베이스는 테이블을 사용한다.
  - 객체 모델과 관계형 모델 간에 불일치가 존재한다.
  - ORM을 통해 객체 간의 관계를 바탕으로 SQL을 자동으로 생성하여 불일치를 해결한다.
- 데이터베이스 데이터 <-> Object 필드
  - 객체를 통해 간접적으로 데이터베이스 데이터를 다룬다.
   
![ORM](https://blog.kakaocdn.net/dn/zmBmh/btrfREPXUNv/Jd4nKONiHm69N2z0pZKD21/img.jpg)   
   
- ORM의 장단점
  - 장점
    - 객체 지향적인 코드로 인해 더 직관적이고 비즈니스 로직에 더 집중할 수 있게 도와준다.
      - ORM을 이용하면 SQL Query가 아닌 직관적인 코드(메서드)로 데이터를 조작할 수 있어 개발자가 객체 모델로 프로그래밍하는 데 집중할 수 있도록 도와준다.
      - 선언문, 할당, 종료 같은 부수적인 코드가 없거나 급격히 줄어든다.
      - 각종 객체에 대한 코드를 별도로 작성하기 때문에 코드의 가독성을 올려준다.
      - SQL의 절차적이고 순차적인 접근이 아닌 객체 지향적인 접근으로 인해 생산성이 증가한다.
    - 재사용 및 유지보수의 편리성이 증가한다.
      - ORM은 독립적으로 작성되어있고, 해당 객체들을 재활용 할 수 있다.
      - 때문에 모델에서 가공된 데이터를 컨트롤러에 의해 뷰와 합쳐지는 형태로 디자인 패턴을 견고하게 다지는데 유리하다.
      - 매핑정보가 명확하여, ERD를 보는 것에 대한 의존도를 낮출 수 있다.
    - DBMS(DataBase Management System)에 대한 종속성이 줄어든다.
      - 객체 간의 관계를 바탕으로 SQL을 자동으로 생성하기 때문에 RDBMS의 데이터 구조와 Java의 객체지향 모델 사이의 간격을 좁힐 수 있다.
      - 대부분 ORM 솔루션은 DB에 종속적이지 않다.
      - 종속적이지 않다는것은 구현 방법 뿐만아니라 많은 솔루션에서 자료형 타입까지 유효하다.
      - 프로그래머는 Object에 집중함으로 극단적으로 DBMS를 교체하는 거대한 작업에도 비교적 적은 리스크와 시간이 소요된다.
      - 또한 자바에서 가공할경우 equals, hashCode의 오버라이드 같은 자바의 기능을 이용할 수 있고, 간결하고 빠른 가공이 가능하다.


  - 단점
    - 완벽한 ORM 으로만 서비스를 구현하기가 어렵다.
      - 사용하기는 편하지만 설계는 매우 신중하게 해야한다.
      - 프로젝트의 복잡성이 커질경우 난이도 또한 올라갈 수 있다.
      - 잘못 구현된 경우에 속도 저하 및 심각할 경우 일관성이 무너지는 문제점이 생길 수 있다.
      - 일부 자주 사용되는 대형 쿼리는 속도를 위해 SP를 쓰는등 별도의 튜닝이 필요한 경우가 있다.
      - DBMS의 고유 기능을 이용하기 어렵다. (하지만 이건 단점으로만 볼 수 없다 : 특정 DBMS의 고유기능을 이용하면 이식성이 저하된다.)
    - 프로시저가 많은 시스템에선 ORM의 객체 지향적인 장점을 활용하기 어렵다.
      - 이미 프로시저가 많은 시스템에선 다시 객체로 바꿔야하며, 그 과정에서 생산성 저하나 리스크가 많이 발생할 수 있다.

## 트랜잭션
- 데이터베이스의 상태를 변화시키기 위해서 수행하는 작업의 단위.
- 특징
  1. 트랜잭션은 데이터베이스 시스템에서 병행 제어 및 회복 작업 시 처리되는 작업의 논리적 단위이다.
  2. 사용자가 시스템에 대한 서비스 요구 시 시스템이 응답하기 위한 상태변환 과정의 작업단위이다.
  3. 하나의 트랜잭션은 Commit되거나 Rollback된다.


## ACID
- 데이터의 유효성을 보장하기 위한, 트랜잭션의 특징들의 앞글자를 딴 단어.
- 원자성(Atomicity)
  - 트랜잭션과 관련된 작업들이 부분적으로 실행되다가 중단되지 않는 것을 보장하는 능력.
- 일관성(Consistency)
  - 트랜잭션이 실행을 성공적으로 완료하면 언제나 일관성있는 데이터베이스 상태로 유지하는 것.
- 독립성(Isolation)
  - 트랜잭션을 수행 시 다른 트랜잭션의 연산 작업이 끼어들지 못하도록 보장하는 것.
  - 트랜잭션 밖에 있는 어떤 연산도 중간 단계의 데이터를 볼 수 없음을 의미.
- 지속성(Durability)
  - 성공적으로 수행된 트랜잭션은 영원히 반영되어야 함을 의미. 시스템 문제, DB 일관성 체크 등을 하더라도 유지되어야 함.


## N+1 문제
- 연관 관계에서 발생하는 이슈로 연관 관계가 설정된 엔티티를 조회할 경우에 조회된 데이터 갯수(n) 만큼 연관관계의 조회 쿼리가 추가로 발생하여 데이터를 읽어오게 되는데, 이를 N+1 문제라고 한다.
- 해결방법
  1. join fetch
  2. @EntityGraph
  3. the second-level cache 사용하기
![](https://incheol-jung.gitbook.io/docs/q-and-a/spring/n+1)


## DB 정규화
- 정규화(Normalization)의 기본 목표는 테이블 간에 중복된 데이터를 허용하지 않는 것이다.
- 중복된 데이터를 허용하지 않음으로써 무결성(Integrity)를 유지할 수 있으며, DB의 저장 용량 역시 줄일 수 있다.
- 정규화의 법칙은 1차정규화, 2차정규화, 3차정규화, BCNF, 4차정규화, 5차정규화까지 나눌 수 있다. (실무적으로 4,5차까지 하는 경우는 많지 않다고 함)

1. 1차정규화
  - 테이블의 컬럼이 원자값(Atomic Value)을 갖도록 테이블을 분해하는 것   
![](https://blog.kakaocdn.net/dn/bNbQUm/btqT18yag04/pTXJX3wB23ouk8az7EgWQ1/img.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbMlNZj%2FbtqT17FWVot%2FjUKTAUyOdrH83pRraKw3K0%2Fimg.png)

2. 2차정규화
  - 1차정규화를 진행한 테이블에 대해 완전 함수 종속을 만족하도록 테이블을 분해하는 것.
  - 완전 함수 종속 = 기본키의 부분집합이 결정자가 되어선 안된다는 것
![](https://blog.kakaocdn.net/dn/ylbaZ/btqT8Jc4K3s/0VFTPoKKFkbxZghKWDwKo1/img.png)
---
![](https://blog.kakaocdn.net/dn/bluCnc/btqT7VEOf04/Me8DfY7rtycgJPYlYQKEWK/img.png)

3. 3차정규화
  - 2차정규화를 진행한 테이블에 대해 이행적 종속을 없애도록 테이블을 분해하는 것.
  - 이행적 종속 = A->B, B->C가 성립할 때, A->C가 성립되는 것.
![](https://blog.kakaocdn.net/dn/enwN1N/btqUeiMyErd/sP8NKCe70NKsZncGuhO9uK/img.png)
---
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fci1le3%2FbtqUeXnPnpD%2FyKkURqr8cZl21f5erx42QK%2Fimg.png)

4. BCNF 정규화
  - 3차정규화를 진행한 테이블에 대해 모든 결정자가 후보키가 되도록 테이블을 분해하는 것.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbBN6xu%2FbtqT6IlqRF4%2FMvBoxYMxtgS1JT7t1AymnK%2Fimg.png)
---
![](https://blog.kakaocdn.net/dn/3cbHr/btq3mNylPan/c6b2lBuH4OkdDNmrzGHWUk/img.png)

- 참고: <https://mangkyu.tistory.com/110>


## 인덱스와 작동방식
- 인덱스란?
  - 추가적인 쓰기 작업과 저장 공간을 활용하여 데이터베이스 테이블의 검색 속도를 향상시키기 위한 자료구조
  - 데이터베이스에서 테이블의 모든 데이터를 검색하면 시간이 오래 걸리기 때문에 데이터와 데이터의 위치를 포함한 자료구조를 생성하여 빠르게 조회할 수 있도록 도움.
  - 인덱스를 활용하면, 데이터를 조회하는 SELECT 외에도 UPDATE나 DELETE의 성능이 함께 향상된다. 그러한 이유는 해당 연산을 수행하려면 해당 대상을 조회해야만 작업을 할 수 있기 때문이다.
![인덱스](https://blog.kakaocdn.net/dn/cBQD97/btqKRtpm2pl/rmo7jTbiiE9tsSQsUg0JPK/img.png)

- 인덱스의 관리
  - 인덱스를 항상 최신의 정렬된 상태로 유지해야 원하는 값을 빠르게 탐색할 수 있다. 그렇기 때문에 인덱스가 적용된 컬럼에 insert, update, delete 할 때 다음과 같은 연산을 추가적으로 해주어야 한다.
    - INSERT: 새로운 데이터에 대한 인덱스를 추가
    - DELETE: 삭제하는 데이터의 인덱스를 사용하지 않는다는 작업을 진행
    - UPDATE: 기존의 인덱스를 사용하지 않음 처리하고, 갱신된 데이터에 대한 인덱스를 추가함.
- 장단점
  - 장점
    - 테이블을 조회하는 속도와 그에 따른 성능을 향상시킬 수 있다.
    - 전반적인 시스템의 부하를 줄일 수 있다.
  - 단점
    - 인덱스를 관리하기 위해 DB의 약 10%에 해당하는 저장공간이 필요하다
    - 인덱스를 관리하기 위해 추가 작업이 필요하다.
    - 인덱스를 잘못 사용할 경우 오히려 성능이 저하되는 역효과가 발생할 수 있다.

- 인덱스의 자료구조
  - Hash table, B+ tree등 다양한 구조가 있는듯.
  - 참고: <https://chartworld.tistory.com/18>
  - <https://mangkyu.tistory.com/96>

