# DynamoDB

<aside>
💡 NoSQL Database

</aside>

- Document
- Key-value

## DynamoDB Global Tables

> dynamoDB 테이블을 자동으로 선택한 AWS 리전들에 복제
> 

multi-region, multi-master database

![Untitled](DynamoDB%20b0095fdfc2e34bb7b64d1c8e22d1f09c/Untitled.png)

## DynamoDB Accelerator(DAX)

<aside>
💡 DynamoDB를 위한 in-memory cache

</aside>

- VPC 환경에서 실행되도록 설계
- DAX 사용 = 읽기 중심의 워크로드에서 빠른 응답 속도
- 온디맨드 확장 (노드 3개의 DAX 클러스터로 시작, 이후에 노드 추가하여 용량 확장)

![Untitled](DynamoDB%20b0095fdfc2e34bb7b64d1c8e22d1f09c/Untitled%201.png)

[Amazon DynamoDB Accelerator(DAX)](https://aws.amazon.com/ko/dynamodb/dax/)