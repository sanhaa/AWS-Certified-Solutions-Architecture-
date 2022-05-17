# Load Balancer

<aside>
💡 Traffic 분산 → 여러 EC2 instances, containers, IP address, Lambda

</aside>

= Routing Traffic

`Route53`과 차이점은 route53은 여러 region 간의 라우팅을 담당하지만, LB는 같은 지역에서 다른 AZ 혹은 다른 인스턴스들에게 트래픽 routing합니다.

### Load Balancer의 이해 (성능 x, `복원력` `가용성`)

> 트래픽 분산이 목적이다. 일단 같은 트래픽을 처리하는 서버(instance, IP, container)를 가용성의 이유로 여러대 둘 수 있다. 이때 로드 밸런서를 이용해서 여러 서버에 트래픽을 보내야 한다.
> 

> 결국, 많은 트래픽을 처리한다는 느낌보다는, `가용성`을 높이기 위해 여러 대의 서버를 사용하려면 거쳐야 하는 layer
> 

> `복원력`있는 설계에 로드 밸런서를 사용하는 이유는, 어떤 인스턴스가 fail일 때 트래픽을 다른 서버로 보내줄 수 있기 때문이다.
> 

## ⭐ Application Load Balancer

<aside>
💡 7계층 로드 밸런서

</aside>

> 웹 개발할 때, API 요청에 따라 각기 다른 MSA를 호출
> 

target = instance, IP(private IP address ), container, lambda

### ALB type

1. Host-based Routing
    
    > HTTP header의 `Host` field (request hedaer 속성 중 하나)에 따라 
    같은 로드 밸런서로부터 `다중 도메인`으로 routing
    > 
2. Path-based Routing
    
    > HTTP header의 `URL path`에 따라 routing
    > 
3. HTTP header-based Routing
    
    > standard or custom HTTP header에 따라 routing
    > 
4. HTTP method-based Routing
    
    > standard or custom HTTP method에 의해 routing
    > 
5. Query string parameter-based routing
6. Source IP address CIDR-based routing

### Content based routing

weighted load balancing

### ALB 오류 예시

1. HTTP 502: Bad gateway
    
    > 로드 밸런서가 예상치 못한 응답을 받았을 때, 
    TCP connection
    target response 
    SSL handshake error
    등록되지 않은 delay period
    Target is lambda function + response 문제, 에러
    > 
2. HTTP 504: Gateway timeout
    
    > 모든 timeout, 연결 시간이 지정 시간보다 오래 걸리면
    > 
3. HTTP 503: Service unavailable
    
    > load balancer의 타겟 그룹이 등록되지 않았을 때
    > 
4. HTTP 500: Internal Server error
    
    > WAF ACL을 구성했는데 ACL 규칙에 에러가 있을 때,
    로드 밸런서가 IdP 토큰과 통신할 수 없다. = 보안그룹 or ACL 문제
    > 
    

## Gateway Load Balancer