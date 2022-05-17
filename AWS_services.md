# AWS Service

<aside>
💡 서비스 별 중요 내용 정리, 서비스 비교

</aside>

[Amazon FSx](AWS%20Service%20d9b871590f6248af933993c833db31e1/Amazon%20FSx%20845b8c86662e4062a53c6828b356dd10.md)

[AWS EMR](AWS%20Service%20d9b871590f6248af933993c833db31e1/AWS%20EMR%20397da58786254bf7b07a33cee4180f91.md)

[AWS Glue](AWS%20Service%20d9b871590f6248af933993c833db31e1/AWS%20Glue%20e9f2f556a355472bb764b67679d8dee2.md)

[Amazon Inspector](AWS%20Service%20d9b871590f6248af933993c833db31e1/Amazon%20Inspector%207bb1c216efb148179dee9e05a7717211.md)

[Trusted Advisor](AWS%20Service%20d9b871590f6248af933993c833db31e1/Trusted%20Advisor%20842a84fdb2f240f4806999abe4d41eac.md)

---

## Computing

[Amazon ECS](AWS%20Service%20d9b871590f6248af933993c833db31e1/Amazon%20ECS%2053345fe5be6f4c2890b8ea1b987a6245.md)

[Lambda](AWS%20Service%20d9b871590f6248af933993c833db31e1/Lambda%20d05d9c10221941f88530ad9c8bc921d3.md)

[Elastic Beanstalk](AWS%20Service%20d9b871590f6248af933993c833db31e1/Elastic%20Beanstalk%20c41e864f0c56427cad45db01fc2560b8.md)

[EC2 Auto Scaling](AWS%20Service%20d9b871590f6248af933993c833db31e1/EC2%20Auto%20Scaling%20a8c73e54271047348bb104ebb8516099.md)

### Lambda vs. ECS Fargate

> **`Fargate`**: AWS 컨테이너 기반 서버리스 컴퓨팅 서비스로, ECS와 EKS를 기반으로 동작
별도의 EC2 인스턴스 없이도 컨테이너를 실행할 수 있게 해줌
’컨테이너 기반’ 차이 - 실행 환경을 람다보다 자유롭게 구성 가능
`labmda`에 비해 실행 속도가 느리고, 동시 실행 태스크 수가 적고 비싸다.
최대 실행 시간에 제한이 없다. *(람다는 최대 실행 시간이 15?분, warm cold 상태에 따라 차이가 있긴 하지만)*
> 

## Messaging

[SQS](AWS%20Service%20d9b871590f6248af933993c833db31e1/SQS%20de166bae37b34e9c95cb8ace3e8ccdcf.md)

[SNS](AWS%20Service%20d9b871590f6248af933993c833db31e1/SNS%20799bf1209cb3421a85f3707fade79cae.md)

[Amazon EventBridge](AWS%20Service%20d9b871590f6248af933993c833db31e1/Amazon%20EventBridge%20085c20b71fae4a3baaff20e1a5ff23fa.md)

[Amazon Lightsail](AWS%20Service%20d9b871590f6248af933993c833db31e1/Amazon%20Lightsail%20b16b6c6cb6604e2e9c1000f149306b13.md)

### SQS vs. SNS

> SNS: broadcasting 방식, 주제(topic)에 대한 구독자들에게 메세지를 모두 뿌림 
SQS: 서비스(1개, 보통 EC2)가 대기열에서 메세지를 polling 해야 함
> 
> 
> [[AWS] SNS vs SQS 차이점](https://seohyun0120.tistory.com/entry/AWS-SNS-vs-SQS-%EC%B0%A8%EC%9D%B4%EC%A0%90)
> 

### SNS로 이메일 보내기?

---

## Storage

[Amazon EBS](AWS%20Service%20d9b871590f6248af933993c833db31e1/Amazon%20EBS%2038cdf07aae044483900b36899e404054.md)

[EFS](AWS%20Service%20d9b871590f6248af933993c833db31e1/EFS%207332e623fd6845428e9a0803231aa235.md)

[Amazon S3](AWS%20Service%20d9b871590f6248af933993c833db31e1/Amazon%20S3%203abdfdacf0a94ca3afa296ea2711c969.md)

[AWS Storage Gateway](AWS%20Service%20d9b871590f6248af933993c833db31e1/AWS%20Storage%20Gateway%205c804defc24c406da6fcf321ead329cf.md)

[DynamoDB](AWS%20Service%20d9b871590f6248af933993c833db31e1/DynamoDB%20b0095fdfc2e34bb7b64d1c8e22d1f09c.md)

[Redis](AWS%20Service%20d9b871590f6248af933993c833db31e1/Redis%20134e69c4bda241ecad92fa086c9461cf.md)

[Aurora](AWS%20Service%20d9b871590f6248af933993c833db31e1/Aurora%2088089f15007d4101bee1f2826928130e.md)

[EC2 Instance Store](AWS%20Service%20d9b871590f6248af933993c833db31e1/EC2%20Instance%20Store%20318e3c8e5092458184ce40c8334bce9c.md)

### EFS vs. Others

> 다른 스토리지는 EC2 하나에 한 개만 결합하여 사용할 수 있는 반면, EFS는 여러 EC2가 동시에 접근할 수 있음 **(ACID 보장)**
> 

### RDS의 현재 데이터와 새로운 데이터를 암호화하기

- 이미 가동 중인 DB를 암호화 못함
- 암호화 되지 않은 상태로 read replica 생성해서 암호화 못함
- **암호화된 snaptshot을 생성하고 그걸로 RDS 인스턴스 복구**

### RDS Read Replica vs. Multi AZ

둘 다 durability (내구성)

> `Multi-AZ`는 다른 AZ에 RDS를 동기화시켜서 primary RDS fail 일 때 복원하기 위해 standby, **복원력 혹은 가용성,** **동기 복제
최소 2개이상의 AZ in single region**
> 

> `Read replica`는 읽기 요청을 동시에 처리하게 해서 트래픽 분산에 초점을 맞춤, **성능, scaling,** **비동기 복제
하나의 AZ, Cross-AZ, Cross-Region**
> 

![Untitled](AWS%20Service%20d9b871590f6248af933993c833db31e1/Untitled.png)

### S3에서 data duration 고려하기

> 항상 s3-IA가 standard보다 cost-effective한 것은 아니다.
> 

> `S3-IA`는 최소 30일간 데이터를 보관해야하기 때문에 짧은 기간동안 유지될 데이터를 저장할 때는 그냥 standard가 낫다.
> 

ex. 중간 쿼리를 24시간정도 저장할 목적으로는 S3 Standard가 비용 효율적인 옵션이다. = 어차피 24시간 저장해도 다른 옵션은 30일치 (혹은 90일치) 요금 청구됨

## Networking & Content Transfer

[Load Balancer](AWS%20Service%20d9b871590f6248af933993c833db31e1/Load%20Balancer%20e7fd922de9cf4f309646759a98da3d4e.md)

[CloudFront](AWS%20Service%20d9b871590f6248af933993c833db31e1/CloudFront%2021d08bc723e4497a82f2c20c440f7511.md)

[API Gateway](AWS%20Service%20d9b871590f6248af933993c833db31e1/API%20Gateway%20fc5e1527ced147c2b201a5d6cd0cd93e.md)

[AWS Step Functions](AWS%20Service%20d9b871590f6248af933993c833db31e1/AWS%20Step%20Functions%20d6c48700d95a4e17a2e51c159125858d.md)

[AWS Direct Connect](AWS%20Service%20d9b871590f6248af933993c833db31e1/AWS%20Direct%20Connect%20c9bf7f62dd024a5ba89f94a9254fb7a2.md)

[Network Access Control List(ACL) vs. Security Group](AWS%20Service%20d9b871590f6248af933993c833db31e1/Network%20Access%20Control%20List(ACL)%20vs%20Security%20Group%20c33b59cee8d94458a22092f692436bb5.md)

[AWS Transit Gateway](AWS%20Service%20d9b871590f6248af933993c833db31e1/AWS%20Transit%20Gateway%20f753ced669f94694a6618eec3db7ea4a.md)

[AWS Global Accelerator](AWS%20Service%20d9b871590f6248af933993c833db31e1/AWS%20Global%20Accelerator%20f338435149ef4c89bbf49bd5d967d4eb.md)

[AWS WAF](AWS%20Service%20d9b871590f6248af933993c833db31e1/AWS%20WAF%20cdb13bd5913243bda030b6d4ef796b7f.md)

[DNS](AWS%20Service%20d9b871590f6248af933993c833db31e1/DNS%20664bf446f6be4e1b91aedf35a75949c7.md)

- Load Balancer vs. Routing
    
    ALB를 이용해서 header에 따라 어떤 서버로 트래픽을 보낼지 결정할 수 있는데(?) 이 개념이 라우팅이 아닌가? → 맞다. LB도 트래픽을 라우팅한다는 용어 사용.
    다만 route53과 LB는 지역/AZ 인지 범위가 다름
    

### 지리적 제한

⭐ 각 서비스의 지리적 제한 기능이 올바른 범위에서 실행되는지 확인할 것 (ex. CloudFront georestriction in VPC❌)

1. georestriction through CloudFront
    
    > georestriction = geo-blocking (CF의 기능)
    > 
    
    > 허용된 국가에서만 콘텐츠에 접근하도록 or 금지된 국가에서 접근하지 못하도록
    > 
2. Route53 - geolocation routing policy
    
    > 유럽에서 발생하는 모든 쿼리를 프랑크푸르트 리전에 있는 ELB로 라우트되도록 조절할 수 있다.
    > 
    
    > 배포 권한이 있는 지역에만 콘텐츠 배포하도록 할 수 있다.
    > 
3. WAF + ALB in VPC
    
    > WAF가 geo match condition 지원 (+ACL)
    > 

`security group`은 지리 제한 못함

❓`ACL`만으로도 지리 제한은 못하는 듯?

### 🔴Privat Link vs. Direct Connect vs. VPC

---

## Logging and Monitoring

[Amazon CloudWatch](AWS%20Service%20d9b871590f6248af933993c833db31e1/Amazon%20CloudWatch%20eb139430e3ce4019a1aaf7805f9c4142.md)

[CloudTrail](AWS%20Service%20d9b871590f6248af933993c833db31e1/CloudTrail%204e1fa123473b4637b1b6102f5cfb370e.md)

[Kinesis](AWS%20Service%20d9b871590f6248af933993c833db31e1/Kinesis%207db9303efa7c40538df82f9a2d683844.md)

### Management

[CloudFormation](AWS%20Service%20d9b871590f6248af933993c833db31e1/CloudFormation%20c7a7509b925f4a7288fecb4d4dfd52e3.md)

## Security & Compliance

[KMS (Key Management Service)](AWS%20Service%20d9b871590f6248af933993c833db31e1/KMS%20(Key%20Management%20Service)%20dd629b8df7fa406798278fd273cbe74e.md)

[IAM](AWS%20Service%20d9b871590f6248af933993c833db31e1/IAM%20b8fb0f7e602d4817b2c3fab4e5d3eda9.md)

[AWS Shield](AWS%20Service%20d9b871590f6248af933993c833db31e1/AWS%20Shield%20620bba93f09f4517912d158c93ff876c.md)

[GuardDuty](AWS%20Service%20d9b871590f6248af933993c833db31e1/GuardDuty%2092f910c188c243c0b4ebe763ca278c2b.md)

[Resource Access Manager](AWS%20Service%20d9b871590f6248af933993c833db31e1/Resource%20Access%20Manager%20e15cadc8a70f4f75844f07e3b264a060.md)

[OpsWorks](AWS%20Service%20d9b871590f6248af933993c833db31e1/OpsWorks%2035341c7c2d634587a04f69b07a83f8d2.md)

[Amazon Cognito](AWS%20Service%20d9b871590f6248af933993c833db31e1/Amazon%20Cognito%20c693f9db42c3471081c6c37c2229ad74.md)

### Organization vs. Single sign-on

> `**AWS Organization**`: 여러 AWS 계정을 조직으로 묶어서 중앙 관리
계정 관리, 통합 청구 기능
**연합 capability 제공 X**
> 

> `**AWS SSO**` : 중앙화된 디렉토리에 있는 그룹 멤버에 따라 연합 접근 권한 정의 가능
다중 디렉토리를 사용하고 user 특성에 따라 권한을 관리하고 싶다면 `IAM` 사용
>