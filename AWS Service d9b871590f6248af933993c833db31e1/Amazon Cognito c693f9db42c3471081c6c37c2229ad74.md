# Amazon Cognito

## User pool

<aside>
💡 User directory in Amazon Cognito 인증,**(자격 증명 확인)을 위함**

</aside>

> 사용자 로그인, 인증을 위해 활용됨
> 

### 활용

- built-in user 관리 제공
- 외부 identity provider(페이스북, 트위터, 등)과의 통합

> 직접 로그인을 하든, 외부 라이브러를 통하든 상관없이 user pool에 있는 모든 멤버가 `directory profile`을 가진다. 
→ 개발자가 SDK를 통해 접근할 수 있음
> 
1. 회원가입과 로그인 서비스
2. 빌트인, 커스터마이징이 가능한 web UI 로그인
3. 소설 로그인과 SAML identity providers from user pool
4. User directory 관리와 user profile
5. 보안 기능 (MFA), 핸드폰 이메일 인증 등
6. 커스터마이징된 workflow, 람다 함수 트리거를 통한 user migration

![Untitled](Amazon%20Cognito%20c693f9db42c3471081c6c37c2229ad74/Untitled.png)

## Identity pool

<aside>
💡 다른 AWS services에 접근할 수 있도록 AWS credential을 user에게 부여함, **권한 부여(액세스 제어)를 위함**

</aside>

> S3 버킷, DynamoDB 테이블과 같이 AWS 리소스에 대한 액세스 권한 부여
> 

> user pool에 있는 사용자에게 리소스 액세스를 허용하려면 identity pool을 user pool token을 credential로 교환하도록 설정해야 한다.
> 

사용자에 대한 고유한 자격증명 생성 → 해당 사용자에게 AWS 서비스에 대한 액세스 권한 부여

![Untitled](Amazon%20Cognito%20c693f9db42c3471081c6c37c2229ad74/Untitled%201.png)