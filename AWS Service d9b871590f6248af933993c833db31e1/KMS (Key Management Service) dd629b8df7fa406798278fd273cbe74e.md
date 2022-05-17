# KMS (Key Management Service)

<aside>
💡 암호화 작업에 사용되는 키를 쉽게 생성하고 제어할 수 있도록 지원하는 서비스

</aside>

[AWS KMS를 활용하여 안전한 AWS 환경을 구축하기 위한 전략 - 임기성 솔루션즈 아키텍트(AWS)](https://youtu.be/wjsEwusxMqE)

✅ CMK는 엄청 중요하기 때문에 CMK가 삭제되고 나서 복구할 수 있는 기간이 주어짐 (기본 30일, 7~30일)

<aside>
⭐ CMK(Customer Master Key) = KMS key = 마스터키 !!!

</aside>

### KMS Key 종류

> `Customer managed key`: 우리가 생성
`AWS managed key`: 우리의 AWS 계정에서 AWS 서비스가 생성
`AWS owned key:` 서비스 계정에서 AWS 서비스가 생성
> 
> 
> ![[https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html)](KMS%20(Key%20Management%20Service)%20dd629b8df7fa406798278fd273cbe74e/Untitled.png)
> 
> [https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html)
> 
> AWS 서비스 중 일부는 customer managed key만 지원, 일부는 AWS ~ key만 지원, 일부는 모든 타입 지원
> 

### 특징

- 고가용성 키 생성
- 스토리지 (키 저장)
- 관리 및 감사 솔루션
- AWS 서비스 전체에서 데이터의 암호화 제어 (중앙 제어)
- 멀티 리전 키 지원 (한 리전에서 암호화, 다른 리전에서 복호화 가능)
- KMS key가 있어야 암호화, 복호화, 데이터 키 생성 가능

## AWS 암호화 개요

### 클라우드에서의 암호화

1. IT 보안 인력 - 키 접근 정책 관리
2. 소프트웨어 개발자 - 데이터 보호를 위해 암호키 사용
3. 규제 준수팀 (감사팀) - 구성 및 이력 정보를 검증

### 논리적 보안 (고객 입장에서 적용할 보안)

1. 전송중 보안
    1. 네트워크 접근 제어 - VPC, Security group, Network ACL
    2. 채널 암호화 -TLS, IPsec
2. 저장시 보안
    1. 데이터 리소스에 대한 논리적 접근 제어
    2. **데이터 암호화** - 고객 통제키에 의한
    3. 데이터 블록, 파일, 전체 디스크 암호화
3. 사용시 보안
    1. 암호키에 대한 보안 체계 - FIPS 140-2 준수환경

### 전송중 보안

TLS: 채널 암호화 방식, 고객이 본인 소유의 인증서(SSL)를 임포트해서 사용

AWS Certificate Manager (ACM)

= TLS 인증서 발급 서비스 

### Client-side vs. Server-side

1. 클라이언트 측 암호화
    
    > 데이터 전송 전에 암호화 수행
    > 
2. 서버 측 암호화
    
    > AWS가 전송된 데이터에 대해 암호화 작업 수행
    > 

## server-side 암호화

**S3**

- `SSE-S3` (S3-managed keys) AES-256
- `SSE-KMS` (KMS keys stoored in AWS KMS) SSE-S3와 유사하지만 추가 혜택과 요금 부과, S3 개체에 대한 무단 액세스 추가 보호, **감사 추적** 기능, Customer manage key 생성 및 관리,
- `SSE-C` (Customer-Provided keys) 암호화 키를 직접 관리,

### 저장시 데이터 암호화

<aside>
💡 대칭키 암호화 방식(기본) → 봉투 암호화

</aside>

대칭키: 같은 키가 암호화/복호화에 사용

## ⭐ Data keys (대칭키 암호화)

KMS key와는 다르게, 다운로드할 수 없고 KMS 외부에서 사용하기 위해 반환된다.

KMS는 데이터 암호화에 data key를 사용하지는 않음 = 외부용 (OpenSSL or ... 암호화 SDK)

`Data key 생성` 
KMS key 
→ data key 생성 (plaintext + encrypted) 

![Data key 생성](KMS%20(Key%20Management%20Service)%20dd629b8df7fa406798278fd273cbe74e/Untitled%201.png)

Data key 생성

`암호화` 
plaintext data key 
→ encrypt data 
→ plaintext data key 메모리에서 제거 
⇒ 암호화된 데이터, 암호화된 데이터키만 저장된 상태 유지 

![암호화](KMS%20(Key%20Management%20Service)%20dd629b8df7fa406798278fd273cbe74e/Untitled%202.png)

암호화

`복호화` 
KMS key 
→ data key를 복호화 
→ plaintext data key 반환 
→ data 복호화 
→ plaintext data key를 메모리에서 삭제

![복호화](KMS%20(Key%20Management%20Service)%20dd629b8df7fa406798278fd273cbe74e/Untitled%203.png)

복호화

## ⭐ Data key pairs (비대칭 키)

<aside>
💡 수학적으로 연관된 public key + private key로 구성된 비대칭 데이터 키 pair

</aside>

⭐ client-side 암호화 (또는 KMS 외부에서 서명/인증 )를 위해 설계됨

- KMS가 각 data key pair의 private key를 대칭 KMS key 아래에서 보호함
- data key pair를 KMS가 저장, 관리, 트래킹하거나 키 페어로 암호화 작업을 수행하는 건 아님
- KMS 외부에서 키 페어를 사용, 관리해야 함

`Key pair 생성`

→ public key + private key

![Untitled](KMS%20(Key%20Management%20Service)%20dd629b8df7fa406798278fd273cbe74e/Untitled%204.png)

`암호화`

→ client-side에서 공개키로 암호화

![암호화](KMS%20(Key%20Management%20Service)%20dd629b8df7fa406798278fd273cbe74e/Untitled%205.png)

암호화

`복호화`

→ 복호화는 private key로만 수행

![복호화](KMS%20(Key%20Management%20Service)%20dd629b8df7fa406798278fd273cbe74e/Untitled%206.png)

복호화