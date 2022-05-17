# API Gateway

<aside>
💡 개발자가 API를 생성, 유지, 모니터링하기 쉽게 만들어주는 완전 관리형 서비스

</aside>

1. RESTful API
    1. HTTP-based
    2. stateless client-server communication
    3. 표준 HTTP methods 구현 (GET, POST, PUT, DELETE)
2. WebSocket API
    1. Websocket protocol 기반
    2. stateful, full-duplex communication between client - server
    

[Study/HTTP.md at main · Sanhaa/Study](https://github.com/Sanhaa/Study/blob/main/Network/HTTP.md)

### ❓왜 RESTful API가 stateless 인가?

<aside>
💡 RESTful API는 REST에 기반한 API이고, REST는 **HTTP** 프로토콜에 기반한 아키텍처이다. HTTP는 stateless protocol 이므로 RESTful API도 마찬가지이다.

</aside>

HTTP는 왜 stateless인가?

**HTTP 특징**

- HyperText Transfer Protocol
- HTTP라는 프로토콜은 www의 기본이 되는 통신 규약으로,
- 클라이언트(요청) - 서버(응답) 구조로 설계되었다.
- 요청 - 응답에서 stateless, connectionless 특징을 가진다.

**HTTP Stateless**

- 서버에 클라이언트가 요청을 보낼 때, 한 번에 모든 정보를 포함하도록 해야 한다.
- 서버는 클라이언트의 이전 상태(state)를 저장하지 않기(less) 때문이다.
- ex. Stateless) 아메리카노 아이스로 주세요. 결제는 카드로 할거에요.
- ex. Stateful) 아메리카노 주세요. → (아이스 or 핫?) → 아이스로 할게요 → (결제 수단은?) → 카드요

**Stateless 특징**

- 각 요청(request)는 별개로 처리된다.
- = 요청들끼리 영향을 받지 않는다.
- 각 request는 server가 이해할 수 있도록 필요한 정보를 모두 포함해야 함.
- storing session state on the server = REST 구조의 stateless 제약을 위반한다. session state는 전적으로 클라이언트 측에서 관리되어야 한다.