NoSQL 데이터베이스
===============

### 비-관계형 데이터베이스 (NoSQL DataBase)
- NoSQL 데이터베이스는 행과 테이블을 사용하는 관계형 데이터베이스(RDB)보다 훨씬 다양한 방식으로 빠르게 바뀌는 대량의 비정형 데이터를 처리할 수 있다
1960년대부터 다양한 이름으로 존재해 온 NoSQL 기술은 데이터 환경이 변화하고 개발자들이 클라우드, 모바일, 소셜 미디어와 빅 데이터로부터 생성되는 다양한 대규모 데이터를 처리해야 할 필요가 늘어남에 따라 그 인기가 급증하고 있습니다.

NoSQL 데이터베이스로 사용할 수 있는 데이터모델의 유형 
- 키-값(key-value)
  - key-value쌍의 형태로 저장한다. 
  - 주로 key값은 정해졌지만, value 값은 정해지지 않을 때, 사용한다.
  - REDIS, Oracle NoSQL Database, VoldeMorte 등의 데이터비스가 있다. 

- 문서(document)
  - 문서 전체를 컬렉션이라 부르는 그룹으로 구성하여 key-value 데이터베이스의 개념을 확장한 것이다. 
  - 중첩된 key-value 값을 지원하며, 문서 내에 있는 모든 속성에 대한 쿼리를 허용한다. 
  - MongoDB, CouchDB, Azure Cosmos DB 등의 데이터베이스가 있다.
  
- 열 형식(wide columnar)
  - 희소 데이터 행에 걸쳐 데이터와 쿼리를 효율적으로 저장하며 데이터베이스의 특정 열에 대한 쿼리 실행 시 이점을 제공한다.
  - Hbase, GoogleBigTable, Vertica 등의 데이터베이스가 있다.


- 그래프(graph)
  - 노드 및 에지 기반 모델을 바탕으로 상호 연결된 데이터를 표현하고 복잡한 관계를 간단하게 스토리지하고 살펴볼 수 있도록 지원
  - 예시로 SNS을 사용하는 사용자들간의 관계를 들 수 있다.
  - Neo4j, BlazeGraph, OrientDB 등의 데이터베이스가 있다.

### MongoDB

### RethinkDB

### Couch DB

### Dynamo DB
