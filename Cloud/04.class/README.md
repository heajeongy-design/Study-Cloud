# Azure 솔루션 & 관리도구

## 중요도 파악
Azure는 서비스가 많아서 “종류 암기”보다, **리소스를 어떻게 관리/자동화/개선하는지(도구)**가 더 중요하다.

---

## 1) Azure 관리도구 TOP 5
- **Azure Portal**: 웹 UI로 리소스 생성/설정/모니터링
- **Azure CLI / PowerShell**: 스크립트로 자동화(반복 작업, 배포에 유리)
- **Azure Cloud Shell**: 브라우저에서 바로 CLI/PS 실행(환경 세팅 부담↓)
- **Azure Mobile App**: 이동 중 모니터링/알림 확인
- **Azure REST API**: 서비스/도구에서 Azure를 API로 제어(통합/자동화)

---

## 2) 운영 핵심 도구 2개
### Azure Advisor
- 배포된 리소스를 분석해서 **가용성/보안/성능/비용** 개선을 추천
- “지금 환경에서 뭘 고치면 좋은지” 체크리스트처럼 쓰기 좋음

### DevOps(개발/배포 자동화)
- **DevOps Services**: 파이프라인, Git repo, 보드 등 협업/배포 도구
- **DevTest Labs**: 개발/테스트 환경을 빠르게 만들고 비용 낭비 줄이기

---

## 3) (카테고리만) Azure 솔루션 분류
- IoT, Big Data/Analytics, AI/ML, Serverless, App Service 같은 “서비스 묶음”이 존재  
→ 지금 단계에서는 **각 영역 대표 서비스가 있다** 정도만 이해하고,
실습/업무에서 필요할 때 깊게 파는 방식이 효율적.

---

## 마지막 한 줄 정리
서비스 이름을 외우기보다 **Portal/CLI(자동화) + Advisor(개선) + DevOps(배포/협업)** 흐름을 잡는 게 중요한 단원
