# 오현우 | Backend Developer

고객의 요구사항을 이해하고, 실제 운영 환경에서 발견한 문제를 기술적 개선으로 연결하는 백엔드 개발자입니다.

Java/Spring 기반으로 공공시설 예약 및 회원관리 시스템을 개발·운영하고 있습니다. 고객사와 직접 요구사항을 협의하고, 기존 시스템의 제약과 운영 위험을 고려하여 해결 방안을 제안하고 구현한 경험이 있습니다.

최근에는 Python과 Kubernetes를 활용한 ML 워크로드 진단 프로젝트를 진행하며, 새로운 기술 환경에서도 문제를 재현하고 원인을 분석하는 경험을 쌓고 있습니다.

---

## How I Work

### 01. 고객의 요구사항과 운영 환경을 함께 이해합니다

공공시설 예약 시스템에 신규 추첨제를 도입하면서 고객사 담당자와 요구사항 및 운영 정책을 협의했습니다.

기존 레거시 시스템의 변경 위험을 고려해 별도 추첨 관리 페이지 구성을 제안하고 합의했으며, 관리자 화면부터 백엔드 로직까지 직접 개발했습니다.

### 02. 현장에서 발견한 문제를 실제 개선으로 연결합니다

신규 업장 오픈을 지원하는 과정에서 배치 스케줄 변경에 컨테이너 재시작이 필요한 운영상 제약을 확인했습니다.

이후 다른 통합예약 시스템을 재구축하면서 배치 작업의 추가·수정·삭제가 컨테이너 재시작 없이 반영되도록 개선했습니다.

### 03. 실패 상황과 데이터 정합성을 고려해 설계합니다

회원관리 솔루션을 개발하며 트랜잭션 경계와 실패 상황을 검토하고, 데이터 정합성과 운영 안정성을 고려한 설계·개선을 진행했습니다.

동시 요청, 외부 시스템 연동 실패 등 정상적인 처리 흐름 밖에서 발생할 수 있는 문제에도 관심을 두고 있습니다.

---

## Featured Projects

### [ml-job-triage](https://github.com/ohujj/ml-job-triage)

**Kubernetes ML Job 장애 재현 및 진단 실험**

Python 기반 진단 CLI를 작성하고, 로컬 Kubernetes 환경에서 CPU 배치 추론 Job의 메모리 부족 종료를 재현했습니다.

- 배치 크기 96, 메모리 한도 64 MiB에서 `OOMKilled` 재현
- 배치 크기 축소와 메모리 한도 상향을 각각 3회 실행해 작업 완료 검증
- Job·Pod 상태, 이벤트, 로그를 함께 조회하는 진단 CLI 구현
- 관측 결과가 충분하지 않을 때 원인 판단을 보류하도록 설계

기술: Python · Kubernetes · Docker · kind

### [Moyeo](https://github.com/ohujj/MOYEO)

**모임 일정·장소 조율 서비스 | 서버 단독 개발**

외부 API 호출 비용과 응답 성능, 데이터 정합성 및 실패 대응을 고려해 백엔드를 설계·개발했습니다.

- Route API 병렬 처리로 응답시간 **9.63초 → 5.90초 (38.8% 단축)**
- 추천 후보 범위와 API 호출량의 트레이드오프 검증
- 외부 스토리지 연동 실패에 대비한 보상 처리 및 재시도 구조 설계
- 참여 당시 출발지 정보 보존과 동시 참여 정합성 고려

기술: Java · Spring Boot · JPA · MySQL · Docker · AWS EC2 · GitHub Actions

---

## Tech Experience

**Backend**

Java · Spring Boot · Spring Data JPA · MyBatis · QueryDSL · Spring Security

**Database / Infrastructure**

MySQL · Docker · AWS EC2 · GitHub Actions · Jenkins

**Technical Exploration**

Python · Kubernetes · kind

---

## Contact

- Email: hyeonwoo5729@gmail.com
- GitHub: [github.com/ohujj](https://github.com/ohujj)
