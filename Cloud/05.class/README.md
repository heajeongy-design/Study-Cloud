# Azure Compute 서비스 & VM / Container 정리

## Azure Compute 서비스
- 클라우드상의 **가상 머신(Compute)** 기반 서비스
- Azure에서 **Compute 작업**을 수행하는 서비스
- **Web Server / Application Server** 운영 시 사용
- 사용자가 VM을 직접 조작하므로 **관리 프로세스에 관여**함

---

## Azure Compute 서비스 종류
- **Azure VM**
  - IaaS(서비스형 인프라)의 대표 서비스
  - 워크로드 수행에 가장 유연
  - 운영체제를 관리해야 하며 사용자가 직접 운영

- **VM Scale Sets**
  - Azure VM Image를 이용하여 VM을 **자동 확장/축소**
  - (AWS 오토스케일링 기능과 유사)

- **App Services**
  - 사용자는 **소스 파일만 업로드**하면 서비스가 알아서 동작하는 PaaS(서비스형 플랫폼)
  - Web App, API App, Logic App, Function 등과 같은 서비스들이 있음

- **Functions**
  - App Services의 하나로 **이벤트 기반** 계산 작업을 수행

---

# Azure 가상 머신(Azure VM)

## Azure VM을 사용할 때 장점
- 데이터 센터 확장을 통해 **민첩성 향상**
- 온프레미스 데이터 센터 또는 다른 클라우드 제공 업체에서 워크로드를 **마이그레이션**
- 실제 운영환경/테스트/개발 작업과 상관없이 이용 가능

## Azure VM 사용 시 주요 차이점(제약/특이사항)
- 2세대 Hyper-V VM 지원 없음
- Microsoft 가상화 기술인 Hyper-V의 **VHDX 가상 디스크 형식 지원 없음**
- 동적 확장 또는 차이점 보관용 디스크 지원 없음
- 읽기 전용 VM 콘솔 액세스(미리보기의 직렬 콘솔)

## 초당 계산된 요금(과금) 정리
- VM이 중지될 때 **Compute 요금 계산이 적용되지 않음**
- Azure Storage의 **VM 디스크 요금은 Compute와 분리**되어 과금됨

---

## Azure VM 연결 방법
- **Windows VM 연결**: RDP로 연결  
  1) 포털에서 RDP 파일 다운로드(바로가기 파일)  
  2) VM 생성 시 사용자 이름/암호 설정  
  3) 포털에서 암호 재설정 가능  

- **Linux VM 연결**: SSH 사용 가능  

> **RDP(Remote Desktop Protocol)**  
> **SSH**: 공개키/개인키 기반 로그인

---

# 가상 머신 중지(Stop) 상태 2가지

## 1) 할당 취소(Deallocated)
- **CPU(Compute)에 대한 과금 없음** (단, 저장소는 과금)
- 정적 IP(공용/사설)를 사용하지 않은 경우 **IP 주소 유지되지 않음**
- 포털 또는 명령줄 도구를 통해 중지
- VM이 인식하는 **스토리지(디스크)는 과금됨**

## 2) 중지(Stopped)
- OS는 꺼지지만 **Compute 과금은 계속됨**
- OS 내에서 또는 명령줄 도구(옵션)를 통해 중지

---

# Azure VM 디스크 개념

## Blob
- 이미지/사운드 파일 같은 **하나의 큰 파일** 저장에 적합

## VM 디스크 저장 형태
- VM이 인식하는 가상 하드디스크는 **블록 형태의 Azure 볼륨**이 가상 형태로 저장됨

---

# 관리 디스크 vs 비관리 디스크

## 관리 디스크(Managed Disk)
- 생성 시 **스토리지 계정 불필요**
- Azure Virtual Machines에서 사용하는 대부분의 디스크
- Azure에서 필요한 물리적 인프라를 관리하는 가상 하드디스크
- 종류: Ultra / Premium SSD / Standard SSD / Standard HDD

## 관리되지 않는 디스크(Unmanaged Disk)
- 생성 시 **스토리지 계정 필요**
- VM에서 사용되는 전통적인 유형 디스크
- 확장성 & 관리 기능 지원이 되지 않음
- VM 데이터를 수동으로 설정/관리하는 경우 사용 (요즘은 많이 사용되지 않음)

---

# VM vs 컨테이너 비교

## VM
### 장점
- 하나의 서버에서 다양한 운영 체제 실행 가능
- 물리적 리소스를 효율적으로 사용
- 신속한 서버 프로비저닝

### 단점
- 각 VM은 OS 이미지/라이브러리/애플리케이션 등을 포함 → 사이즈가 커질 수 있음

## 컨테이너(Container)
### 장점
- Host OS를 공유 → OS 부팅/라이브러리 로드 불필요
- 훨씬 더 효율적이고 경량 제작 가능
- 컨테이너화된 애플리케이션 빠른 실행
- VM 대비 더 많은 인스턴스를 한 머신에 올릴 수 있음
- 패치/업데이트 등 유지관리 오버헤드 감소

### 단점
- 이식 가능하지만 운영 체제 제한 존재  
  예) Linux 컨테이너는 Windows에서 실행할 수 없고, 그 반대도 동일

---

# Azure 컨테이너 서비스

## Azure Container Instances(ACI)
- Azure가 관리하는 container cluster에 컨테이너 이미지를 업로드하여
  자동으로 실행할 수 있는 **PaaS 서비스**

## Azure Kubernetes Service(AKS)
- 많은 컨테이너를 관리하기 위한 **컨테이너 오케스트레이터(조율)**
- Azure VM에 Kubernetes cluster를 구성해주며
  Master Node는 Azure에서 무료로 제공

---

## 요약
- Azure Compute는 웹/앱 서버 운영을 위한 컴퓨팅 서비스이며, 대표적으로 VM(IaaS), Scale Sets, App Services(PaaS), Functions가 있다.  
- Azure VM은 유연하지만 OS 운영을 사용자가 관리해야 하고, 과금은 Compute와 디스크(스토리지)가 분리된다.  
- VM 중지 상태는 **Deallocated(Compute 과금 없음, 스토리지는 과금)** vs **Stopped(Compute 과금 지속)**로 나뉜다.  
- 디스크는 관리 디스크(표준)와 비관리 디스크(스토리지 계정 필요)가 있으며, 컨테이너는 VM보다 가볍지만 OS 제약이 있다.  
- 컨테이너 실행은 ACI, 다수 컨테이너 운영/조율은 AKS를 사용한다.
