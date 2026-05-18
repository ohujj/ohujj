# 안녕하세요, 백엔드 개발자 오현우 입니다 👋
# Nice to meet you, I'm Back-End Developer Hyeonwoo Oh 👋

트레이드오프·동시성·결제·운영 안정성 같은 백엔드 깊이를 다지는 것을 목표로 학습합니다.

## 🔭 Currently

- **hanplane** — 한정판 커머스 백엔드, 동시성 4단계 narrative 구축 중
- 코딩 테스트 Level 2 안정화 목표(Programmers)
- 기술 블로그 운영 — 학습 내용 / 트러블슈팅 / 의사결정 기록

## 🌱 Next

- 결제 멱등성 제대로 구현 (Idempotency Key 헤더 기반)
- 분산락 4단계 narrative 완성 (Redisson + Fencing Token)
- Flyway 도입 검토 (ddl-auto 함정 경험 후)

## 🛠 Tech Stack

**Backend**
- Java, Spring Boot
- Spring Data JPA, QueryDSL
- Spring Security + JWT

**Persistence / Cache / Search**
- MySQL
- Redis (Redisson 분산락)

**Infra / Ops**
- AWS EC2
- Docker
- GitHub Actions (CI/CD)

**기타**
- PortOne (PG 연동)
- JUnit (동시성 테스트 포함)

## 🚀 Projects

### 🛒 [hanplane](https://github.com/ohujj/hanplane) — 한정판 커머스 백엔드

한정판 발매 시점의 동시 주문 폭주를 견디는 백엔드. 동시성·결제·검색을 다층적으로 다루는 학습 프로젝트.

- **재고 동시성 4단계 비교** — 비관적 락 → 낙관적 락 → Redisson 분산락 → Fencing Token
- **결제** — PortOne PG 연동, 트랜잭션 분리, 멱등성, 보상 트랜잭션 (3원칙)
- **검색** — QueryDsl 활용
- **CI/CD** — GitHub Actions → EC2 자동 배포

### 🎬 [Ne(o)rdinary Hackathon — Filmo](https://github.com/ohujj/CMC-Hackathon)

영화관에서의 순간을 기록하는 서비스. 너디너리 해커톤 3등 수상.

- 무중단 Blue-Green 배포 (Traefik + Docker Compose)
- Cloudflare Tunnel 로 외부 도메인 라우팅
- GitHub Actions → Docker Hub → EC2 자동 배포

## 📝 Tech Blog

학습 내용, 토이프로젝트 진행 기록, 트러블슈팅, 기술 의사결정 정리를 업로드합니다.

➡ [hyeonwoo5729.tistory.com](https://hyeonwoo5729.tistory.com)

## 📫 Contact

- Blog: [hyeonwoo5729.tistory.com](https://hyeonwoo5729.tistory.com)
- Email: hyeonwoo5729@gmail.com
