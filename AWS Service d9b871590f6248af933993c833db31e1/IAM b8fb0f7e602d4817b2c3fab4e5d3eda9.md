# IAM

<aside>
💡 식별과 접근 관리 Identity and Access Management

</aside>

> 서비스, 리소스 액세스 관리, **target = user, groups, roles, AWS resources**
> 
- 이때 user, group, role 들을 `IAM indentities` 라고 함

## 기본 내용

- `IAM identities`: users, groups of users, roles
- `IAM principal`: user or role
- `IAM entity`: user or role
- `Policy`: identity나 resource에 연계되어 permission을 정의
- AWS는 IAM principal (user or role)이 요청을 보낼 때 policies 검토함
- `Permission`: 요청의 허용/거부를 결정하는 권한, in policy
- Polilcy 저장 = JSON document (단, ACL 제외)

### Policy type (6가지)

1. **`Identity-based policy`:** IAM identities에 policy 부여
    
    > user, group, role
    > 
    1. Managed policies: standalone 정책
    2. Inline policies: 하나의 user, group, role에 직접적으로 추가하는 정책 (policy - identity 간 1대 1관계)
2. **`Resource-based policy`** : resource에 inline policies 부여
    
    > resource
    > 
    1. ex. S3 bucket 정책, IAM role trust policy
3. **`Permission boundary` :** IAM entity에게 permission boundary를 지정하는 policy 사용
    
    > user, group, role
    > 
    1. identity-based policies가 entity에게 부여할 수 있는 최대 permission을 정의
    2. ❌permission을 부여하는 것은 아님❌
    3. resource-based policy가 부여할 수 있는 최대 권한을 정의하지는 않음
    4. ex. user or role (entity)에 permission boundary가 적용되면, 그 entity는 indentity-based policies와 permission boundaries 모두 만족하는 행동만 수행할 수 있음
4. **`Organization SCP`** : 조직의 계정 멤버, 조직 유닛에 최대 permission을 정의하는 AWS Organization service control policy를 사용
    
    > AWS organizations organizational unit
    > 
    1. identity-based policies or resource-based policies가 부여할 권한을 제한
    2. (마찬가지로) 권한을 직접 부여하지는 않음
5. **`ACL(Access control list)`** : 다른 계정의 어떤 principal이 resource에 접근할 수 있는지 컨트롤
    
    > resource
    > 
    1. resource-based policy와 비슷
    2. JSON policy document 구조를 사용하지는 않음
    3. 특정 principal에 권한을 부여하는 cross-accound permission policies
    4. 같은 계정의 다른 entity에게 권한 부여 X
6. **`Session policy`** : AWS CLI or AWS API를 사용할 때, role과 federated user를 가정하기 위해 사용
    
    > role or federated user session
    > 
    1. session에 role이나 user의 identity-based policies를 부여하는 권한을 제한함
    2. 생성된 세션에 권한을 제한할 뿐, 권한을 부여하지는 않는다.

### Identity-based vs. resource-based policies

![Untitled](IAM%20b8fb0f7e602d4817b2c3fab4e5d3eda9/Untitled.png)

**Identity-based**

```json
{
  "Version": "2012-10-17",
  "Statement": {
    "Effect": "Allow",
    "Action": "s3:ListBucket",
    "Resource": "arn:aws:s3:::example_bucket"
  }
}
```

**Resource-based**

```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Sid": "1",
    "Effect": "Allow",
    "Principal": {"AWS": ["arn:aws:iam::account-id:root"]},
    "Action": "s3:*",
    "Resource": [
      "arn:aws:s3:::mybucket",
      "arn:aws:s3:::mybucket/*"
    ]
  }]
}
```

## IAM users

- AWS와 상호작용할 IAM user = 사람 or service
- 주로 사용: 누군가에게 AWS 관리 콘솔에 로그인할 능력을 주거나, API or CLI를 사용하여 AWS 서비스 프로그램적인 요청을 만들 때
- IAM user 생성한 후, 권한 주는 방법 두 가지
    1. 특정 권한 정책이 있는 user group의 멤버로 설정
    2. user에게 직접적으로 정책을 부여

> ❓ IAM account에서 IAM user 생성할 수 있나?
> 

### IAM user vs. IAM roles

AWS에서 뭐를 할 수 있고 할 수 없는지를 결정하는 권한 정책

차이점: role은 credential 없다. (비밀번호나 접근 키 등) → 특정 사람과 연결된 게 아니라 필요한 누군가가 역할을 가지게 됨.

IAM user는 특정 task에 대해 임시적으로 다른 권한을 가지게 될 수 있음 

모든 경우에 IAM 계정을 만들어서 권한을 부여할 필요 없다. 장기적으로 credential하려면 IAM user를 만들고, 그렇지 않고 임시적으로 권한을 권한을 허용하려면 IAM role을 사용

- IAM user를 생성해야 하는 경우
    - AWS 계정을 생성한 후, 그 계정에서 혼자 작업한다면
        
        > root user 권한으로 AWS를 사용할 수 있지만 추천하지 않음
        자신에 대한 IAM user를 생성하고 사용하는 것을 추천
        > 
    - AWS 계정에서 여럿이 일해야 하고, user group이 다른 식별 메커니즘이 없다면
        
        > AWS 리소스에 접근할 개인을 위한 IAM user를 생성하고 각자에게 credential 주기.
        여러명이 credential 공유하지 않는 것을 추천
        > 
- IAM role을 생성해야 하는 경우
    - EC2에서 동작하는 어플리케이션을 제작 중인데, 그 앱이 AWS에 요청을 보낼 때
        
        > application에 IAM user를 생성하고 credentials을 넘기거나 application에 credential을 임베드 하지 말아라.
        EC2 인스턴스에 attach할 IAM role을 생성하고 그 인스턴스에서 동작하는 애플리케이션에 임시 security credential 주기
        > 
    - mobile phone에서 동작하는 어플리케이션, AWS에 요청을 보낼 때
        
        > IAM user를 생성하고 app에 IAM user의 access key를 분산하지 않도록
        인증된 user로 로그인하도록 하고, user와 IAM role를 연결시키기
        앱은 그 role에 연결된 정책이 명시한 권한을 가진 임시 security credentials을 얻을 수 있음.
        > 
    - 회사 사람이 회사 네트워크에 있을 때 인증된다. 다시 로그인하지 않고도 AWS를 사용하도록 하고 싶음.
        
        > 
        > 
    

## MFA

<aside>
💡 Multi Factor Authentication

</aside>

- IAM user or AWS account root user에 대해 MFA  활성화할 수 있다.

> 보안강화를 위해 로그인 + 보안질문
> 
1. Virtual MFA device
2. U2F security key
3. HArware MFA device

[https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_compare-resource-policies.html](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_compare-resource-policies.html)

[https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#managedpolicy](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#managedpolicy)