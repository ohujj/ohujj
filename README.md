# 백엔드 개발자 오현우입니다

Java/Spring 기반 백엔드 개발을 하고 있습니다.

회원관리 솔루션 회사에서 API 개발, 서버 측 검증 로직 개선, MySQL/MyBatis 기반 레거시 유지보수를 경험했습니다. 최근에는 커머스 도메인 프로젝트를 통해 주문/결제/환불 정합성, 재고 동시성, QueryDSL 검색을 학습하고 있으며, 트랜잭션과 데이터 정합성을 검증하는 백엔드 개발을 지향합니다.

---

## 관심 있는 문제

* 주문, 결제, 환불 과정에서의 데이터 정합성
* 재고 차감, 쿠폰 발급과 같은 동시성 문제
* 트랜잭션 경계와 상태 전이 설계
* 운영 복잡도를 고려한 기술 선택
* 장애 원인 추적과 서버 측 검증 로직 개선

---

## Tech Experience

### Used at Work

* Java
* Spring Boot
* MySQL
* MyBatis

### Used in Projects

* Spring Data JPA
* QueryDSL
* Spring Security, JWT
* PortOne PG
* AWS EC2, Docker, GitHub Actions
* JUnit 5

---

## Projects

### [hanplane](https://github.com/ohujj/hanplane) — 한정판 커머스 백엔드

한정판 상품 판매 상황에서 발생할 수 있는 주문, 결제, 환불, 재고 정합성 문제를 학습하기 위한 Spring Boot 기반 커머스 백엔드 프로젝트입니다.

* **재고 동시성**
  동시 주문 상황에서 Lost Update와 초과 판매 가능성을 확인하고, 상품 재고 조회 구간에 DB 비관적 락을 적용해 재고 차감 요청이 순차 처리되도록 수정했습니다.

* **결제 정합성**
  PortOne PG 결제 승인 정보를 조회한 뒤 PG 결제 금액과 내부 주문 금액을 비교했습니다. 금액 불일치 요청은 ILLEGAL 상태로 분리하고, 결제 승인 중 예외가 발생하면 Payment는 FAIL로 기록하며 Order는 다시 결제 가능한 PENDING 상태로 복구했습니다.

* **환불 정합성**
  환불 요청 시 결제 성공 여부, 주문 소유자, 주문상품 환불 상태를 검증해 타 사용자 주문 환불과 중복 환불을 차단했습니다. 환불 금액 계산, 재환불 방지, 타 사용자 주문 환불 방지 케이스를 테스트로 검증했습니다.

* **검색 단순화**
  초기에는 Elasticsearch를 검토했지만, 현재 검색 조건에서는 RDB와 QueryDSL로 충분하다고 판단했습니다. Elasticsearch 의존성을 제거하고 QueryDSL 기반 동적 검색으로 단순화했습니다.

* **배포 자동화**
  GitHub Actions, Docker, AWS EC2 기반 배포 흐름을 구성하고 배포를 검증했습니다. 현재 EC2 인스턴스는 비용 관리를 위해 중지한 상태입니다.

### [Filmo](https://github.com/ohujj/CMC-Hackathon) — 영화 기록 앱 백엔드

영화관에서의 순간을 기록하는 앱 서비스의 백엔드 API를 구현했습니다. Ne(o)rdinary Hackathon 우수상, Filmo - CMC + UMC 연합 해커톤 10팀 중 3위를 기록했습니다.

* Android 앱 클라이언트와 연동되는 백엔드 API 구현
* 공통 응답 스펙, 예외 처리, 토큰 기반 인증 흐름 구현
* GitHub Actions, Docker Hub, AWS EC2 기반 배포 흐름 구성

---

## Contact

* Email: [hyeonwoo5729@gmail.com](mailto:hyeonwoo5729@gmail.com)
