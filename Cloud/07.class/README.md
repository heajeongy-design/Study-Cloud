# Azure 네트워크 서비스

---

## 1) Azure 네트워크(Azure Network)
- Azure 내에 **사설 네트워크를 만들고 조작**할 수 있는 서비스
- **SDN(Software Defined Network)** 기반으로 동작하며 모든 네트워크는 **격리(Isolation)**
- Azure VM 등, 가상 네트워크 기능이 필요한 모든 리소스에서 구성 가능
- On-premise와 연결(하이브리드)을 위한 기능 구현 가능
- 부하 분산 장치를 이용하여 여러 대의 서버로 트래픽 분산 가능

---

## 2) Azure 네트워크 서비스 주요 구성
- **Azure Virtual Network(VNet)**
  - 논리적인 사설 네트워크 구성
  - VM 같은 리소스 간 **보안된 통신** 제공

- **Azure Load Balancer**
  - 여러 대의 서버에 트래픽 분산
  - 애플리케이션/리소스에 대한 **고가용성 접근** 제공

- **VPN Gateway**
  - On-premise 또는 다른 네트워크 센터로 네트워크를 확장할 수 있는 **관리형 서비스**
  - 고가용성 지원
  - (하이브리드 클라우드 운영에 필수적인 요소)

- **Azure Application Gateway**
  - 웹 애플리케이션 트래픽을 분산하여 **고가용성 접근** 제공

- **CDN(Content Delivery Network)**
  - 사용자에게 가까운 지역에서 콘텐츠를 캐싱하여 전달하는 **분산 서버 네트워크**
  - 예: 동영상 콘텐츠 등

---

## 3) 가상 네트워크 소개(VNet Overview)
- **Bring your own network**(자체 네트워크 구성)
- 고객의 사설 또는 공용 IP 주소로 **서브넷(관리 단위/연결 요소)** 구성 가능  
  - 네트워크가 필요하면 분할하여 **선택적으로 연결**할 수 있음
- **Bring your own DNS** 또는 Azure 제공 DNS 사용  
  - 클라우드 내 소규모 가상 네트워크 연결을 위해 실제 DNS 서버 또는 Azure DNS 사용
- **VPN and/or ExpressRoute**로 하이브리드 연결 가능

---

## 4) 가상 네트워크(VNet)
- 자신의 네트워크에 대한 **논리적 표현**
- 전용 사설 클라우드용 **전용 VNet** 생성 가능
- VNet을 사용하여 데이터 센터를 **안전하게 확장**
- 하이브리드 클라우드 시나리오에 활용

---

## 5) 서브넷(Subnet)
- 하나의 네트워크가 아닌 여러 개의 작은 **효율적 관리 단위**
- 가상 네트워크는 필요 시 하나 이상의 서브넷으로 분할 가능
- 물리 장치 없이 네트워크의 **논리적 분할** 제공
- 서브넷 분할은 통신 성능을 높이고 보안 구현을 쉽게 구성/관리
- 각 서브넷은 **고유 주소 범위**로 정의되어야 함  
  - Azure 내 다른 가상 네트워크와 **주소 범위 중복 불가**
- (브로드캐스트 트래픽 최소화, 이질적인 물리 네트워크 기술 공존, 관리 용이성 목적)
  
<img width="940" height="350" alt="image" src="https://github.com/user-attachments/assets/ee7f4ffa-4d31-47dc-9765-1f6a48a655b0" />

---

## 6) 가상 네트워크 작성(생성)
- 포털 관리 인터페이스를 통해 새로운 가상 네트워크를 생성하여 특정 용도로 활용 가능
- 필요 시 새 가상 네트워크 작성 가능
- 가상 머신 생성 시 가상 네트워크 추가 가능
- 주소 공간(Address Space)을 정의해야 하며 하나 이상의 서브넷 필요
  - 표준 사설 IP 주소 범위 사용 권장  
    - `10.X.X.X`  
    - `172.16.X.X ~ 172.31.X.X`  
    - `192.168.X.X`
- 주소 공간이 겹치지 않도록 주의

---

## 7) Azure 가상 네트워크 필요성 결정

### 가상 네트워크가 필요한 리소스
- Azure VM
- 가상 머신 확장 집합(VM Scale Sets)
- Azure Application Gateway(내부)
- Azure App Service 환경
- Azure Kubernetes Service(AKS)
- 서비스 패브릭(Service Fabric)

### 가상 네트워크를 지원하는 리소스/기능
- 지점 및 사이트 간 VPN
- 서비스 엔드포인트(최종 통신 목적지)  
  - Azure Storage, SQL Database, Cosmos DB, SQL 데이터웨어하우스, PostgreSQL, MySQL,
    Service Bus, Event Hub

### 가상 네트워크와 통합되지 않는(독립적인) 리소스
- Azure AD
- Traffic Manager
- CDN(Content Delivery Network)
- Container Registry

---

## 8) 도메인 이름 및 ARM(Resource Manager) 관련
- 도메인 이름은 **Resource Manager**에서 구성
- 공용 IP는 옵션이며 VM 또는 로드 밸런서에 연결 가능
- 로드 밸런서당 최대 **100대 VM 지원**
- ARM 모드에서 VM은 더 이상 클라우드 서비스에 배포되지 않고 **가상 네트워크가 필요**함

---

## 9) NAT 규칙(NAT Rules)
- 사설 네트워크와 공용 네트워크 주소 체계에서  
  공용 IP ↔ 사설 IP 변환을 통해 **연결**해주는 서비스
- 기업에서는 라우터 같은 장치가 NAT 역할을 수행(라우터가 NAT 기능 제공)

  <img width="379" height="260" alt="image" src="https://github.com/user-attachments/assets/c630daed-90ca-4f65-80ab-6e20cf4984de" />


### 사설 IP
- 외부 공용 네트워크와 직접 통신 불가  
- 내부 통신을 위해 사용하는 네트워크 요소

### 포트 포워딩(Port Forwarding)
- 공용 트래픽을 단일 VM의 내부 포트로 포워딩

### 부하 분산(Load Balancing)
- 트래픽을 여러 VM의 내부 포트로 포워딩

---

## 10) Azure Load Balancer
- **VIP** : 로드밸런서 (클라우드 상 만들어낸 웹서버, 서비스 서버를 통해서 Port Forwarding을 통해 연결할 수 있겠금 함)
  - 로드 밸런서를 통해 포트 포워딩으로 웹 서버/서비스 서버에 연결할 수 있게 하는 개념

- **Azure Load Balancer**
  - Azure에서 운영 중인 VM/애플리케이션/컨테이너 서비스로 유입되는 트래픽을 자동 분산 처리
  - 중계 장치 역할 + 부하 분산
<img width="636" height="179" alt="image" src="https://github.com/user-attachments/assets/6903ef94-993c-443f-9749-a6967d636d72" />

---

## 11) 전통적인 로드 밸런서 기능(업무 분장)
- 단일 지점을 통해 서버에 연결
- 애플리케이션 환경 분리
- 고가용성과 내결함성 제공
- 탄력성과 확장성 향상

---

## 12) 로드 밸런싱 개념(L4 vs L7)

### 기본 개념
- 로드밸런싱은 기존 온프레미스 환경에서도 존재
- L은 OSI 7 Layer의 **Layer**에서 유래

### L4(네트워크) 스위치
- TCP와 SSL 지원
- 클라이언트와 서버 연결 중계
- 헤더 변경 없음
- 프록시 프로토콜로 요청에 대해 소스/목적지 IP, 포트 추가 가능

### L7(애플리케이션) 스위치
- HTTP와 HTTPS 지원
- 클라이언트 연결은 로드 밸런서에서 종료되고, 로드 밸런서 ↔ 서버는 별도 연결
- `X-Forwarded-For` 헤더를 통해 클라이언트 IP를 백엔드 인스턴스로 전달 가능  
- (웹 서비스/보안 웹 서비스 트래픽 분산을 위해 동작하는 소프트웨어 네트워크 장치)

---

## 13) Layer7 로드 밸런싱 플랫폼(정리)
- Azure Load Balance는 새롭고 풍부한 기능을 가진 **레이어7 로드 밸런싱 플랫폼**
- Azure에서 완전 관리, 확장성, 높은 가용률 보장
- 1개의 로드 밸런서로 여러 애플리케이션에 대해 동시 분산 처리 가능
- 일반 웹 트래픽: 80 포트  
- 인증서 기반 보안 트래픽: 443 포트

---

## 요약
- Azure에서 네트워크를 어떻게 구성하는지, 특히 **가상 네트워크(VNet)** 를 중심으로 학습했다.  
- Azure 네트워크는 SDN(Software Defined Network) 기반으로 동작하며, Azure 내부에서 **사설 네트워크를 생성하고 격리된 환경**을 만들 수 있다.
- 또한 온프레미스 환경과 연결하거나(하이브리드), 트래픽이 몰릴 때 부하분산을 통해 안정적으로 서비스를 제공하는 구조도 함께 다뤘다.

- 핵심 서비스로는 **Azure Virtual Network(VNet)**, **Load Balancer**, **VPN Gateway**, **Application Gateway**, **CDN**이 있다.  
- VNet은 Azure 리소스(예: VM, AKS 등) 간에 안전한 통신을 제공하는 논리적 사설 네트워크이고, VNet 내부는 필요에 따라 **서브넷(Subnet)**으로 분할해 관리한다.
- 서브넷은 네트워크를 논리적으로 나눠서 보안과 운영 효율을 높이며, 각 서브넷은 고유한 주소 범위를 가져야 하고 다른 VNet과 주소 공간이 겹치지 않도록 설계해야 한다.
- 주소 공간은 일반적으로 사설 IP 대역(10.x, 172.16~31.x, 192.168.x)을 사용한다.

- 또한 Azure에서 하이브리드 연결을 구성할 때는 **VPN Gateway**나 **ExpressRoute**를 사용하며, DNS 역시 자체 DNS를 쓰거나 Azure 제공 DNS를 선택할 수 있다는 점을 배웠다.  
- 네트워크와 함께 중요한 개념으로는 **NAT(공용 IP ↔ 사설 IP 변환)**가 있으며, 이를 통해 포트 포워딩(특정 VM으로 전달) 또는 부하 분산(여러 VM으로 분산) 같은 트래픽 제어가 가능하다.
- 실제 트래픽 분산은 **Azure Load Balancer**(고가용성/트래픽 분산) 또는 웹 트래픽 특화인 **Application Gateway**(웹 애플리케이션 트래픽 제어)로 구현한다.

- 마지막으로, 모든 Azure 리소스가 VNet과 항상 통합되는 것은 아니며(예: Azure AD, Traffic Manager 등은 독립적), 리소스 성격에 따라 VNet 통합 여부가 달라진다는 점도 정리했다.

