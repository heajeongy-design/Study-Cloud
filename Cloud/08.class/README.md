# Azure Storage

## 개요
- **Azure Storage**는 고객의 요구 사항을 충족하기 위해 **내구성(Durability), 가용성(Availability), 확장성(Scalability)** 에 의존하는 최신 애플리케이션을 위한 **클라우드 스토리지 솔루션**이다.
- **Azure Storage Service는 PaaS를 지원**하며, 통합 분산 스토리지 시스템 위에 구축된다.
- 주요 특징
  - 내구성(Durability)
  - 미사용 데이터 암호화(Encryption at rest)
  - 강력한 일관성 복제(Strongly consistent replication)
  - 내결함성(Fault tolerance)
  - 자동 부하 분산(Automatic load balancing)

---

## Azure Premium Storage
- **Azure Premium Storage**는 **Azure Virtual Machines**에서 실행되는 **I/O 집약적 워크로드**에 대해  
  **지연 시간이 짧은(Low latency) 고성능 디스크 지원**을 제공한다.

---

## IaaS 스토리지 (Infrastructure as a Service)
> VM 등 인프라 레벨에서 직접 사용하는 스토리지

### 1) 디스크 (Disk)
- Azure IaaS VM에 대한 **영구 디스크(Persistent Disk)**
- Premium Storage 지원
- 디스크 옵션
  - SSD 기반
  - 높은 IOPS
  - 낮은 대기 시간(Low latency)
- 활용
  - **Lift-and-shift 작업**에 적합

### 2) 파일 (File)
- **SMB 및 REST**로 액세스
- 어디서나 접근 가능
- 보안 액세스 지원

---

## PaaS 스토리지 (Platform as a Service)
> 애플리케이션/데이터 레벨에서 활용하는 스토리지

### 1) Blob (컨테이너 / Blob Storage)
- 비구조적 데이터 저장 (텍스트 또는 이진 데이터)
- Blob 유형
  - Block Blob
  - Page Blob
  - Append Blob

### 2) Table Storage
- NoSQL 데이터 저장소 (구조적 데이터)
- 부하 기반 동적 크기 조정
- 페타바이트 규모로 확장 가능
- 빠른 Key/Value 조회에 강점

### 3) Queue Storage
- 메시지 저장 및 검색
- 확장성 매우 높음
- 메시지를 비동기적으로 처리 가능

---

# 스토리지 계정 (Storage Account)

## 정의
- Azure 내에 데이터를 저장하고 관리할 수 있는 서비스
- 구성 요소
  - Blob(컨테이너)
  - File
  - Queue
  - Table

## 핵심 포인트
- **Blob**: 비정형 데이터를 저장하는 객체 스토리지
- **File**: SMB 3.0 프로토콜을 통해 VM에 Mount 가능
- Blob에는 VM의 디스크 파일도 저장 가능 (**Unmanaged Disk**)

## 도메인 형태 예시
- Blob Endpoint:
  - `https://<스토리지계정이름>.blob.core.windows.net`

---

# 관리 디스크 (Managed Disk)

## 개요
- 성능 및 규모(Scale) 관리 간소화

## 장점
- 관리 단순화로 **용량 확장 계획 실수 방지**
- 확장 용이
- 가상 머신 확장 집합(VM Scale Set)과 직접 통합

---

# 수업 요약 (Summary Sentences)
- Azure Storage는 **내구성/가용성/확장성**을 기반으로 최신 애플리케이션을 위한 **클라우드 스토리지**를 제공한다.  
- Azure Premium Storage는 VM 기반 **I/O 집약 워크로드**를 위해 **저지연 고성능 디스크**를 제공한다.  
- IaaS 스토리지는 VM 중심으로 **Disk와 File**을 사용하며, Disk는 고성능(SSD/IOPS) 워크로드에 적합하고 File은 SMB/REST로 접근 가능하다.  
- PaaS 스토리지는 **Blob/Queue/Table**로 구성되며, Blob은 비정형 데이터, Table은 NoSQL Key-Value, Queue는 비동기 메시징 처리에 강점이 있다.  
- Storage Account는 Blob/File/Queue/Table을 묶어 관리하는 단위이며, 서비스별 Endpoint 도메인을 가진다.  
- Managed Disk는 디스크 운영을 단순화해 확장 리스크를 줄이고, VM Scale Set과의 통합으로 운영 효율을 높인다.
