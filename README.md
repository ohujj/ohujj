# 안녕하세요, 백엔드 개발자 오현우입니다 👋
# Nice to meet you, I'm Back-End Developer Hyeonwoo Oh 👋

Java/Spring 기반 백엔드 개발자입니다.

트랜잭션, 데이터 정합성, 결제/환불 상태 관리, 동시성 제어처럼 백엔드에서 중요한 문제를 재현하고 검증하는 방향으로 학습하고 있습니다.

## 🔭 Currently

- **hanplane** — 한정판 커머스 백엔드 프로젝트
  - 주문/결제/환불 정합성
  - 상품 재고 동시성 제어
  - 쿠폰 발급 동시성 실험
  - QueryDSL 기반 검색
- 코딩 테스트 Level 2 안정화 목표(Programmers)
- 기술 블로그 운영 — 학습 내용 / 트러블슈팅 / 의사결정 기록

## 🌱 Next

- 결제 멱등성 개선 — 클라이언트 Idempotency-Key 기반 중복 요청 방지
- hanplane README 고도화 — 재고 동시성, 결제 정합성, 테스트 결과 정리
- REST API 설계와 테스트 코드 작성 역량 보강

## 🛠 Tech Experience

**Work Experience**
- Java
- Spring Boot
- MySQL
- MyBatis

**Project Experience**
- Spring Data JPA
- QueryDSL
- Spring Security, JWT
- PortOne PG
- Redis, Redisson
- AWS EC2, Docker, GitHub Actions
- JUnit 5

## 🚀 Projects

### 🛒 [hanplane](https://github.com/ohujj/hanplane) — 한정판 커머스 백엔드

한정판 상품 판매 상황에서 발생할 수 있는 주문, 결제, 환불, 재고 정합성 문제를 학습하기 위한 백엔드 프로젝트입니다.

- **재고 동시성**  
  100명 동시 주문 테스트에서 Lost Update와 초과 판매 가능성을 재현한 뒤, DB 비관적 락을 적용해 재고 수량만큼만 주문이 성공하도록 검증했습니다.

- **결제 정합성**  
  PortOne PG 결제 승인 정보를 조회하고, PG 결제 금액과 내부 주문 금액을 비교해 금액 불일치 요청을 분리했습니다.  
  결제 승인 중 예외가 발생하면 Payment는 FAIL로 기록하고, Order는 다시 결제 가능한 PENDING 상태로 복구하도록 처리했습니다.

- **환불 정합성**  
  환불 요청 시 결제 상태, 주문 소유자, 주문상품 환불 상태를 검증해 잘못된 환불 요청을 차단했습니다.  
  수량 3개 주문상품 환불 금액, 이미 환불된 주문상품 재환불 방지, 다른 유저 주문 환불 방지 케이스를 테스트로 검증했습니다.

- **검색 단순화**  
  초기에는 Elasticsearch를 검토했지만, 현재 검색 조건에서는 RDB + QueryDSL로 충분하다고 판단해 Elasticsearch 의존성을 제거하고 QueryDSL 기반 검색으로 단순화했습니다.

- **CI/CD**  
  GitHub Actions와 AWS EC2를 활용해 자동 배포 흐름을 구성했습니다.

### 🎬 [Ne(o)rdinary Hackathon — Filmo](https://github.com/ohujj/CMC-Hackathon)

영화관에서의 순간을 기록하는 서비스입니다.  
Ne(o)rdinary Hackathon 우수상, Filmo - CMC + UMC 연합 해커톤 10팀 중 3위

- 무중단 Blue-Green 배포 구성
- Traefik + Docker Compose 기반 라우팅
- Cloudflare Tunnel을 활용한 외부 도메인 연결
- GitHub Actions → Docker Hub → EC2 자동 배포

## 📝 Tech Blog

학습 내용, 토이프로젝트 진행 기록, 트러블슈팅, 기술 의사결정 정리를 업로드합니다.

➡ [hyeonwoo5729.tistory.com](https://hyeonwoo5729.tistory.com)

## 📫 Contact

- Blog: [hyeonwoo5729.tistory.com](https://hyeonwoo5729.tistory.com)
- Email: hyeonwoo5729@gmail.com
