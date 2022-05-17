# Network Access Control List(ACL) vs. Security Group

- 예시 문제
    
    ![SmartSelect_20220124-112446_Samsung Notes.jpg](Network%20Access%20Control%20List(ACL)%20vs%20Security%20Group%20c33b59cee8d94458a22092f692436bb5/SmartSelect_20220124-112446_Samsung_Notes.jpg)
    

> 일반적으로 서브넷 - ACL, EC2 인스턴스 - SG이지만, VPC도 보안그룹을 가질 수 있고, S3 인스턴스에 ACL을 설정할 수 있는 등, 서비스에 따라 서브넷/인스턴스의 구분에 차이가 있음
> 

✅ VPC security group

✅ 

`**ACL**`

> 서브넷의 in, out 트래픽을 조절하는 방화벽 역할을 하는 VPC의 보안 계층
> 
- **상태 비저장:** 허용된 인바운드 트래픽의 응답이 아웃바운드 트래픽 규칙에 지배된다 = return traffic이 규칙에 의해 명시되어 있어야 함.
❓ 허용, 거부 규칙 모두 존재하는 이유? 허용 규칙에 없으면 무조건 거부 아닌가?
- 보안 그룹 만으로도 트래픽 허용/거부가 가능하지만, 특정 서브넷에 해당하는 인스턴스에 추가적으로 방화벽 역할을 하는 레이어를 추가하고 싶을 때 사용
- 하나의 서브넷은 하나의 ACL에만 연결, 하나의 ACL은 다수의 서브넷에 연관시킬 수 있음.

**`Security Group`**

> EC2 인스턴스에 대해 인바운드, 아웃바운드 트래픽을 조절하는 가상의 방화벽 역할
> 
- ⭐instance 수준에서 동작, not subnet level = 같은 VPC에 있는 각 인스턴스 들은 각자 다른 보안 그룹을 할당 받을 수 있음
- **상태 저장:** return traffic이 규칙에 관계없이 자동적으로 허용됨

**차이점 정리, 그림**

![Untitled](Network%20Access%20Control%20List(ACL)%20vs%20Security%20Group%20c33b59cee8d94458a22092f692436bb5/Untitled.png)

![Untitled](Network%20Access%20Control%20List(ACL)%20vs%20Security%20Group%20c33b59cee8d94458a22092f692436bb5/Untitled%201.png)

[Internetwork traffic privacy in Amazon VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Security.html#VPC_Security_Comparison)