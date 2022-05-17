# Amazon S3

<aside>
💡 객체 스토리지

</aside>

✅ S3는 data (from internet)의 경우 전송 요금이 없다. (보관 기간과 storage class에 따른 요금만)

✅ object가 versioning 되면 버전에 따라 retain 기간을 달리 설정할 수 있다. 

## S3 Storage Class

1. **S3 Standard**
    
    범용
    
2. **S3 Intelligent-Tiering**
    
    알 수 없거나 변화하는 액세스 (액세스 패턴을 모니터링하여 객체를 저렴한 액세스 계층으로 자동 변환)
    
3. **S3 Standard-IA**
    
    빈번하지 않은 액세스, 그러나 빠르게 액세스 해야할 때
    
4. **S3 One Zone-IA**
    
    최소 3개의 AZ에 데이터를 저장하는 다른 S3 스토리지 클래스와 달리 단일 AZ에 저장, 저렴, 가용성 낮음, 복원력 낮음 = 
    
5. **S3 Glacier Instant Retrieval**
    
    거의 액세스하지 않음, 밀리초 단위의 검색이 필요한 장기 데이터, 가장 저렴한 아카이브 스토리지
    
6. **S3 Glacier Flexible Refrieval**
    
    5 GIR보다 더 적은 액세스, 비동기식 검색(몇 분 ~ 몇 시간의 액세스 시간), 더 저렴
    
7. **S3 Glacier Deep Archive**
    
    아카이브 스토리지 중에서도 가장 저렴, 연 1~2회, 데이터의 장기 보관
    
8. **S3 Outposts**
    
    온프레미스 Outpost 환경에 객체 스토리지 제공
    

![Untitled](Amazon%20S3%203abdfdacf0a94ca3afa296ea2711c969/Untitled.png)

---

**Minimum storage duration charge**

> 최소 보관 기간, 이것보다 더 짧게 보관해도 이 기간만큼 비용 청구
> 

## 추가 기능

### S3 Transfer Acceleration (S3TA)

<aside>
💡 speed up content transfers to and from S3 (50~500%) 큰 오브젝트, 장거리용

</aside>

- accelerated transfer에 대한 요금만 지불하면 된다.
- accelerate 효과를 못봣을 때는 지불하지 않아도 됨

### Multi part upload

<aside>
💡 Object를 여러 파트로 분할하여 업로드

</aside>

`performance` `resilience`

### Versioning

<aside>
💡 keep multiple variants of an object in same bucket

</aside>

- 한 번 enable로 설정하면 unversioned state로 되돌릴 수 없음

### S3의 scalability

- 자동적으로 높은 요청 속도를 달성하기 위해 scaling

```
s3://{bucket_name}/{prefix}/{file_name}
```

- prefix 이용?? → parallel reading 가능 = performance 높일 수 있다.

### Lifecycle transition

**불가능한 전환**

S3 Intelligent-Tiering → S3 standard, S3 standard-IA

S3 One Zone-IA → S3 standard-IA, S3-Intelligent-Tiering

- 항상 S3 standard가 상단에서 전환되어야 하고, 전환된 결과가 standard 일 수는 없다.
- 마찬가지로 `폭포수` 형태의 transition을 이루기 때문에 하단 → 상단 전환은 불가능

![Untitled](Amazon%20S3%203abdfdacf0a94ca3afa296ea2711c969/Untitled%201.png)

**제약**

> S3 standard → S3 Standard-IA
> 

> S3 standard-IA → S3 One zone-IA
> 
- **전환하기 위해서는 최소 기간 30일 필요**