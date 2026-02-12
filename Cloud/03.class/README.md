# Azure 핵심 서비스 정리 (Compute / Container / Network / Storage / Database)

## 1) Azure 컴퓨팅 서비스(Compute)
- 클라우드 기반 애플리케이션 실행을 위해 **필요할 때 언제든 사용 가능한 컴퓨팅 서비스**

---

## 2) 가상 머신 기반 서비스(Virtual Machine)

### Azure Virtual Machines (VM)
- **IaaS(Infrastructure as a Service)** 기반
- 클라우드에서 서버(컴퓨팅 파워)를 제공 → OS/패치/보안 등 운영은 사용자가 관리

### VM Scale Sets
- VM 인스턴스 수를 **자동으로 조정(오토 스케일)**하도록 설계
- 작업 부하 분산(Load balancing) 및 트래픽 집중 시 성능 최적화에 유리

### App Service
- **PaaS(Platform as a Service)** 기반
- 엔터프라이즈급 **웹/모바일/API 앱**을 작성, 배포, 확장할 수 있는 서비스

### Azure Functions
- **이벤트 기반(Event-driven)**으로 코드 실행
- 트리거(이벤트)가 발생하면 계산 작업 수행 (Serverless 성격)

---

## 3) 컨테이너 서비스(Container)
- 가상화 환경을 제공하지만 **가상 머신과 달리 OS를 직접 관리하지 않음**
- 컨테이너는 **가볍고 빠르게 생성/확장/중지**되도록 설계

### Azure Container Instances (ACI)
- 컨테이너 이미지를 업로드하면 **자동으로 실행**할 수 있는 서비스
- 비교적 “간단하게 컨테이너를 띄우는” 용도에 적합

### Azure Kubernetes Service (AKS)
- 여러 컨테이너를 운영/확장/배포하기 위한 **컨테이너 오케스트레이션(조율) 서비스**
- 대규모/복잡한 컨테이너 운영 환경에 적합

---

## 4) Azure 네트워크 서비스(Network)
- **Azure Virtual Network(VNet)**를 통해 Azure 리소스 간 **안전한 통신** 제공

### Load Balancer
- 애플리케이션/리소스에 대한 **고가용성 접근** 제공
- 트래픽을 분산하여 성능/가용성 향상

### VPN Gateway
- 온프레미스 ↔ Azure 간 **보안 연결(VPN)** 제공
- 확장성과 고가용성을 지원하는 플랫폼 관리형 게이트웨이

### Application Gateway
- 웹 애플리케이션 트래픽을 관리하는 구성요소
- (L7 레벨에서) HTTP/HTTPS 트래픽 라우팅/제어에 활용

### Content Delivery Network (CDN)
- 사용자가 있는 지역에서 웹 콘텐츠를 **빠르고 안정적으로 제공**하기 위한 분산 서버 네트워크

---

## 5) 데이터 형태(Data Types)
- **구조적 데이터(Structured)**: 관계형 데이터베이스(테이블/행/열)
- **반구조적 데이터(Semi-structured)**: 테이블 고정 구조 X, NoSQL/문서 형태  
  - 예: JSON, HTML, 블로그/문서 형태 데이터
- **비구조적 데이터(Unstructured)**: Blob 형태의 비정형 데이터  
  - 예: PDF, JPG, 비디오 등

---

## 6) Azure 스토리지 서비스(Storage)

### IaaS 관점
#### Disk
- Azure IaaS VM을 위한 **영구 디스크**
- Premium Storage(SSD 기반), 높은 IOPS, 낮은 지연 시간
- Lift & Shift(기존 시스템을 그대로 옮기는 방식) 작업에 유리

#### File
- **SMB 및 REST**로 액세스 가능
- 어디서나 접근 가능 + 보안 액세스 지원

### PaaS 관점
#### Blob(컨테이너)
- 비구조적 데이터(텍스트/이진) 저장
- Blob 유형: Block Blob / Page Blob / Append Blob

#### Table
- **NoSQL 키-값 저장소**
- 부하 기반의 동적 크기 조정
- 페타바이트 규모까지 확장 가능, 빠른 조회에 유리

#### Queue
- 메시지 저장/검색을 위한 서비스
- 매우 높은 확장성, 메시지 **비동기 처리**에 활용

> Azure Storage는 통합 분산 스토리지 시스템 기반으로 구성되며,  
> 내구성, 미사용 데이터 암호화, 강력한 복제, 내결함성, 자동 부하 분산 기능을 제공한다.

---

## 7) Azure 데이터베이스 서비스(Database)

### Azure Cosmos DB
- 전역 분산(Global distribution) 데이터베이스 서비스
- 처리량(Throughput)과 스토리지를 **탄력적으로 독립 확장** 가능

### Azure SQL Database
- Microsoft SQL Server 엔진 기반의 **관계형 데이터베이스**
- DB를 서비스로 제공하는 형태(DaaS/Managed DB 성격)

### Azure Database Migration Service
- 다양한 DB 소스를 Azure 데이터 플랫폼으로 **최소 중단 시간으로 마이그레이션**할 수 있는 관리형 서비스

---

## 요약
- Azure 핵심 서비스는 **Compute / Container / Network / Storage / Database**로 크게 나뉘며,  
  목적에 따라 **VM(IaaS)** 또는 **App Service/Functions(PaaS·Serverless)** 같은 실행 방식을 선택한다.  
- 컨테이너는 **OS 관리 부담을 줄이고**(VM보다 가벼움) 필요 시 **빠르게 확장/중지**할 수 있으며,  
  단일 실행은 **ACI**, 다수 컨테이너 운영/조율은 **AKS**가 핵심이다.  
- 네트워크는 **VNet 기반의 안전한 통신**을 중심으로 Load Balancer / VPN Gateway / Application Gateway / CDN을 조합해  
  **고가용성·보안·트래픽 제어·콘텐츠 전송 속도**를 확보한다.  
- 데이터는 **구조적/반구조적/비구조적**으로 구분하며, 저장소는 Disk/File/Blob/Table/Queue로 목적에 맞게 선택한다.  
- 데이터베이스는 관계형(예: **Azure SQL**)과 전역 분산형(예: **Cosmos DB**)을 이해하고,  
  이전이 필요할 경우 **Database Migration Service**로 중단 시간을 최소화할 수 있다.

