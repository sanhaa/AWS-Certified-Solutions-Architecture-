# AWS Global Accelerator

<aside>
💡 글로벌하게 제공될 애플리케이션의 가용성과 성능을 높이기 위한 네트워킹 서비스

</aside>

> AWS 자체 global network를 활용해서 user → application 인터넷 트래픽을 직접적으로 연결함
> 

### 특징

- application endpoint를 지속적으로 모니터링
- 가장 가까운 `healthy endpoints`로 traffic을 라우팅 함
- `static IP address` 제공 - fixed entry point to app
- ⇒ 특정 IP 주소를 각기 다른 AWS region과 AZ에서 관리하는 복잡도를 제거
- TCP or UDP proxying packets하여 성능 높임

### non-HTTP use case와 잘 맞음

- `gaming`(UDP), `IoT` (MQTT), `Voice over IP`
- 물론 HTTP use case와도 잘 맞음. 특히 static IP 주소가 필요할 때