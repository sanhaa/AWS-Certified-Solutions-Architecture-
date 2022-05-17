# GuardDuty

<aside>
💡 AWS 계정, 워크로드, S3의 데이터를 지속적으로 모니터링하여 위협을 찾고 보호함

</aside>

![Untitled](GuardDuty%2092f910c188c243c0b4ebe763ca278c2b/Untitled.png)

- 서비스 `diable` → 남아있는 모든 데이터, 구성을 삭제함.
- `suspend`(정지) the service → 즉시 서비스를 정지함, 구성과 발견점을 삭제하진 않음

### GuardDuty가 지원하는 데이터 소스

- VPC Flow Logs
- DNS logs
- CloudTrail events (계정활동 기록 이벤트)

> S3 데이터 모니터링 기능이 있어서 S3 access log 분석할 것 같은데, CloudTrail S3 data events 데이터를 분석함
>