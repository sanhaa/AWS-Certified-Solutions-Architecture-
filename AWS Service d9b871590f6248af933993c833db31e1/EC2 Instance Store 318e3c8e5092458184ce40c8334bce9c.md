# EC2 Instance Store

<aside>
💡 temporary block-level storage for instance

</aside>

### 도대체 Instance Store 왜 쓰냐

> 장기 데이터는 X, 단, 물리적으로 같은 디스크 볼륨을 사용하기 때문에 IO 성능은 엄청 좋음 `performance`
> 
1. 무조건 `high performance` 필요한데, 장기 보관하거나 데이터를 유지할 필요 없을 때
2. or 내결함성 아키텍처가 보장되어 있으면 data loss 신경쓰지 않고 high performance 이득을 취할 수 있음 

### 특징

- host computer에 물리적으로 attached
- `자주 바뀌는` information을 `임시`로 저장하기에 이상적
- ex. buffers, caches, scratch data, `data that is replicated across a fleet of instances`
- instance type에 따라 지원하는 instance store volume 개수가 다름

![Instance store 안에 ephemeral[0-23]들은 store volumes](EC2%20Instance%20Store%20318e3c8e5092458184ce40c8334bce9c/Untitled.png)

Instance store 안에 ephemeral[0-23]들은 store volumes

❓ 애초에 instance = 가상의 컴퓨터 1대인데, 사진에서 host computer는 개발자가 설정할 수 있는 건지? 

> The virtual devices for instance store volumes are `ephemeral[0-23]`. Instance types that support one instance store volume have `ephemeral0`. Instance types that support two instance store volumes have `ephemeral0` and `ephemeral1`, and so on. 
→ ❓ 그럼 계속 볼륨이 1개인 인스턴스만 생성하면 ephemeral0 볼륨만 사용하는 건지.
그리고 그럼 instances A와 B가 같은 볼륨에 접근하게 되는 건지..
> 

### Instance Store lifetime

> The data in an instance store persists only during the lifetime of its associated instance
> 
- instance store volumes는 인스턴스 시작시에만 명시할 수 있다. = 볼륨을 떼어서 다른 인스턴스에 붙이기 불가능, **중간에 추가도 불가능**
- instance `리부팅`- instance store 유지
- **instance store 데이터 유실 경우**
    - underlying `disk drive fails`
    - instance `stops`
    - instance `hibernates` (최대 절전모드)
    - instance `terminates`
- 인스턴스의 AMI를 생성할 경우: volume에 있던 데이터 보존X, AMI로 실행한 인스턴스의 볼륨에도 표시되지 않음