# Redis

<aside>
💡 key-value 스토어, in-memory 캐싱

</aside>

> 얘 자체가 DBMS라기 보다는 캐싱용 DB(스토어)라고 생각하면 될 듯
> 

### 특징

- RDS, Document 데이터베이스보다 빠르고 가볍게 동작
- **in memory 데이터 구조 = 캐싱**

### ⭐ RDS와 함께 사용

- RDS 사용 시에 IO 처리량이 많으면 레디스를 사용해 데이터를 캐싱하고, RDS에 업데이트 하는 식으로 RDS에 가해지는 부담을 줄이며 성능을 향상할 수 있음

### 사용 예시

1. RDS IO 처리 캐싱하기
2. 사용자의 세션 관리하기: 사용자의 세션 유지, 불러오고, 활동 추적
3. 메세지 큐잉
4. API 캐싱: 라우트로 들어온 요청에 대해 요청 값을 캐싱하면 동일 요청에 대해 캐싱된 데이터를 리턴
    
    [redis 캐시 활용해서 express API 속도 높이기](https://fors.tistory.com/582)
    

### 레디스의 데이터 구조

1. String (주로)
2. Hash
3. List
4. Set

## ElastiCache와 차이

<aside>
💡 ElasticCache는 캐싱을 위한 **웹 서비스**이고, Redis와 Memcached 두 가지 캐시 엔진을 지원함

</aside>

> ElastiCache + Redis로 사용된다고 생각하면 될 듯?
> 

### ElastiCache for Redis

<aside>
💡 클라우드에서 분산된 in memory 데이터 스토어 또는 캐시 환경을 손쉽게 설정, 관리하는 웹 서비스

</aside>