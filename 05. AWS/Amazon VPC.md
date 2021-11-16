## Amazon VPC(Virtual Private Cloud)
**사용자의 AWS 계정 전용 가상 네트워크**

- AWS 클라우드에서 논리적으로 격리된 공간을 프로비저닝하여 고객이 정의하는 가상 네트워크에서 AWS 리소스 시작 가능

- IP 주소 범위 선택, 서브넷 생성, 라우팅 테이블 및 네트워크 게이트웨이 구성 등 가상 네트워킹 환경 완벽 제어

- IPv4와 IPv6를 모두 사용하여 리소스와 애플리케이션에 안전하고 쉽게 액세스 가능

- 양방향 액세스를 제공하고 공개적으로 제어 가능

- 모든 사용자에게 강제적으로 적용하기 때문에 VPC 없이는 대부분의 서비스 사용이 불가능

- 애플리케이션에 대한 격리/분리된 공간 제공

- 리소스가 차지할 특정 CIDR 지정 가능

- 엄격한 인바운드 및 아웃바운드 트래픽 규칙 제공

- 계정 당 리전 당 최대 5개의 VPC 보유 가능하지만 AWS Support를 통해 서비스 제한 증가 요청 가능

<br/>

### Subnet
**리소스 그룹을 격리할 수 있는 VPC IP 주소 범위의 세그먼트 또는 파티션**

#### Public Subnet
- IGW., ELB, Public IP/Elastic IP를 가진 인스턴스를 내부에 소유

- NAT Instance를 통해 Private Subnet 내에 있는 instances의 연결 가능

#### Private Subnet
- 기본적으로 외부와 차단

- 인스턴스들은 Private IP만을 갖고 있으며 internet inbound/outbount가 불가능하고 오직 다른 서브넷과의 연결만이 가능

- 일반적으로 제한된 아웃 바운드 퍼블릭 인터넷 액세스를 지원하기 위해 NAT GW 사용

<br/>

### Routing Table
- VPC 리소스 간에 트래픽 연결에 필요

- 모든 서브넷에는 연결된 라우팅 테이블 요구

- VPC를 생성하면, 자동으로 기본 라우팅 테이블 생성

- 처음엔 VPC 내 모든 리소스에 대하여 통신을 허용하는 로컬 경로만 포함
  - ex)  10.10.0.0/16 - 로컬

- VPC에서 인스턴스를 시작할 때마다 로컬 경로는 해당 인스턴스에 자동으로 적용

- 로컬 경로는 수정 불가

<br/>

### IGW(Internet GateWay)
- VPC와 인터넷 간의 연결

- 라우팅 테이블에서 상위부터 매칭되는 IP에 대한 타깃을 찾고, 없으면 가장 마지막 대상 igw-id를 찾아 주소 확인

- 인터넷으로 라우팅 가능한 트래픽에 대한 서브넷 라우팅 테이블에 대상 제공

<br/>

### VPG(Virtual Private Gateway)
- VPC의 Private Resource에 액세스 하기 위해 사용

- VPC와 사설 네트워크(온프레미스 데이터 센터, 내부 회사 네트워크, ..)간에 VPN 연결을 설정 가능

- 승인된 네트워크에서 오는 경우에만 VPC로의 트래픽 허용

<br/>

### AWS Direct Connect
**데이터 센터와 VPC 간에 전용 프라이빗 연결을 설정할 수 있는 서비스**

- AWS Direct Connect가 제공하는 프라이빗 연결은 네트워크 비용을 줄이고 네트워크를 통해 이동할 수 있는 대역폭의 양을 늘리는 데 도움

<br/>

### NAT Gateway
- Private Subnet이 인터넷과 연결하기 위한 아웃바운드 인스턴스

- Private Network가 인스턴스의 펌웨어나 주기적인 업데이트가 필요하여 아웃바운드 트래픽만 허용되어야할 경우에 사용

- Public Subnet 상에서 동작하는 NAT GW는 Private Subnet에서 외부로 요청하는 아웃바운드 트래픽을 받아 인터넷 게이트웨이와 연결

- Public Subnet에 존재하는 인스턴스들은 IGW와 연결되어 있으므로 Private Subnet의 인스턴스들도 인터넷 사용이 가능

<br/>

### ENI(Elastic Network Interface)
**동일한 가용 영역의 EC2 인스턴스간에 이동할 수 있는 가상 네트워크 인터페이스**

- 프라이빗 IP 주소, 탄력적 IP 주소, MAC 주소 유지

- 여러 네트워크 인터페이스를 하나의 인스턴스에 연결하면 유용

<br/>

### EIP(Elastic IP)
**동적 클라우드 컴퓨팅을 위해 설계된 고정 Public IPv4 주소**

- EIP를 사용하지 않으면 인스턴스를 재부팅할 때마다 할당 받은 IP 주소가 변경

- EIP 주소를 인스턴스와 직접 연결하는 대신 네트워크 인터페이스에 연결하면 네트워크 인터페이스의 모든 속성을 한 번에 한 인스턴스에서 다른 인스턴스로 이동 가능

<br/>

### VPC 연결
#### CGW(Customer GateWay)
**AWS VPC와 기업의 온프레미스 간의 연결 시, VPN과 연결**

- VPN 터널 당 1개 사용

- CGW 당 Public IP 1개 사용

#### AWS Direct Connect
**물리적인 회선을 AWS와 온프레미스 데이터 센터 사이에 연결해 주는 기능**  
(공용 인터넷을 통한 VPN이 아닌 광 라인을 통한 전용 프라이빗 연결)

- 프라이빗 광 라인이므로 데이터 전송 비용 크게 감소

- 비용 감소와 안전적인 속도를 보장받고 싶은 경우에 사용

#### VPC Peering
**두 VPC 간에 트래픽을 라우팅할 수 있도록 하기 위한 두 VPC 사이의 네트워킹 연결**

- 1:1 설정만 가능

- IGW나 VGW를 거치지 않고 직접적인 연결

- PCX(Peering Connection Gateway)를 통해 구성

<br/>

### Route 53
**Cloud Domain Name System (DNS) 웹 서비스**

- 상태 확인 및 DNS 장애 조치 가능

<br/>

### Security Group
**인스턴스에 대한 인바운드 및 아웃바운드 트래픽을 제어하는 가상 방화벽**

- 모든 송, 수신 트래픽은 모든 IP Protocol, Port 또는 IP 주소로 제한

- 같은 SG를 사용하는 Instance간 통신 허용

- Default로 인바운드는 모두 거부, 아웃바운드는 모두 허용

- 인스턴스 재시작으로 IP가 바뀌어도 SG 이름으로 접근 가능

- Stateful(상태 저장) 방식이므로 인바운드 요청이 허용되는 경우 자동으로 아웃바운드 허용

<br/>

### NACL(Network ACL)
**1개 이상의 서브넷 내부와 외부의 트래픽을 제어하기 위한 방화벽**

- 서브넷 단위로 가상의 방화벽을 만들어 트래픽 제어

- Default로 모든 인바운드 및 아웃바운드 트래픽 허용

- Stateless(상태 비저장) 방식이므로 인바운드 및 아웃바운드 트래픽 모두에 대한 명시적인 규칙(1024~65535 포트 허용) 필요

<br/>

### Security Group과 NACL 비교
Security Group | NACL
:---: | :---:
인스턴스 레벨 운영 | 서브넷 레벨 운영
허용 규칙 지원 | 허용 및 거부 규칙 지원
상태 저장<br/>규칙에 관계없이 반환 트래픽 자동 허용 | 상태 비저장<br/>반환 트래픽이 규칙에 의해 명시적으로 허용되어야 함
트래픽 허용 여부를 결정하기 전에 모든 규칙 평가 | 트래픽 허용 여부를 결정할 때 번호가 가장 낮은 규칙부터 순서대로 규칙 처리
인스턴스 시작 시 누군가 보안 그룹을 지정하거나, 나중에 보안 그룹을 인스턴스와 연결하는 경우에만 인스턴스에 적용 | 연결된 서브넷의 모든 인스턴스에 자동 적용