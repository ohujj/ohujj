# 오현우 | Java/Spring Backend Developer

Java/Spring 기반 백엔드 개발자입니다.

실무에서는 회원/예약 도메인 API 개발과 MySQL/MyBatis 기반 레거시 유지보수를 경험했습니다. 최근에는 결제 실패처럼 표시되던 운영 이슈를 요청 단위 로그와 DB 상태를 기준으로 추적해, 실제 결제 API 문제가 아니라 결제 완료 후 후속 API 및 공통 예외 처리 흐름 문제로 분리했습니다.

개인 프로젝트에서는 한정판 커머스 도메인을 통해 주문/결제/환불 상태 정합성, 결제 confirm 멱등성, PG 조회 실패/타임아웃 보정, 금액 불일치 취소 보정, 재고 차감 동시성 문제를 구현하고 테스트로 검증했습니다.

---

## 관심 있는 문제

* 주문, 결제, 환불 과정에서의 데이터 정합성
* 결제 confirm 중복 요청과 멱등 처리
* PG 조회 실패/타임아웃처럼 결과를 즉시 확정할 수 없는 상태의 보정
* 재고 차감, 예약 신청과 같은 동시성 문제
* 트랜잭션 경계와 상태 전이 설계
* 운영 이슈를 로그와 DB 상태를 기준으로 추적하는 방법
* 현재 서비스 규모에 맞는 기술 선택과 복잡도 조절

---

## Tech Experience

### Used at Work

* Java
* Spring Boot
* MySQL
* MyBatis
* GitLab
* Jenkins

### Used in Projects

* Spring Data JPA
* QueryDSL
* Spring Security, JWT
* PortOne PG
* AWS EC2
* Docker
* GitHub Actions
* JUnit 5

---

## Projects

### [hanplane](https://github.com/ohujj/hanplane) — 한정판 커머스 백엔드

한정판 상품 판매 상황에서 발생할 수 있는 주문, 결제, 환불, 재고 정합성 문제를 다룬 Spring Boot 기반 백엔드 프로젝트입니다.

단순 CRUD 구현보다 결제 중복 요청, PG 응답 불명확 상태, 금액 불일치, 환불 검증, 재고 동시성처럼 상태 전이와 데이터 정합성이 중요한 문제를 중심으로 설계했습니다.

#### 주요 구현

* **결제 confirm 멱등 처리**

  * `Idempotency-Key` 기반으로 같은 `orderId + Idempotency-Key` confirm 재요청 시 기존 Payment를 재사용하도록 구현했습니다.
  * 기존 Payment가 있는 경우 PG 조회와 결제 후처리 로직을 다시 실행하지 않도록 분리했습니다.

* **중복 Payment 생성 방지**

  * 같은 주문에 서로 다른 `Idempotency-Key` 요청이 동시에 들어오는 상황을 고려해 Order row를 `PESSIMISTIC_WRITE`로 조회했습니다.
  * `payment(order_id, idempotency_key)` unique constraint를 추가해 같은 주문/같은 멱등키 조합의 중복 insert를 DB 레벨에서도 방어했습니다.

* **PG 조회 실패/타임아웃 보정**

  * PG 조회 실패나 타임아웃처럼 결제 결과를 즉시 확정할 수 없는 경우를 `VERIFY_REQUIRED` 상태로 보류했습니다.
  * 이후 보정 배치에서 PG 결제 정보를 재조회하고 성공, 실패, 금액 불일치, 재시도 유지 상태로 분기하도록 구성했습니다.

* **금액 불일치 결제 보정**

  * PG 승인 금액과 내부 주문 금액이 다를 경우 정상 결제 완료로 처리하지 않고 PortOne 전액 취소를 먼저 시도했습니다.
  * 취소 성공 시 `ILLEGAL`, 취소 실패 시 `CANCEL_REQUIRED` 상태로 분리하고, 보정 배치에서 취소를 재시도하도록 구현했습니다.

* **환불 정합성**

  * 성공한 결제에 대해서만 환불을 허용했습니다.
  * 주문 소유자, 주문상품 상태, 이미 환불된 상품 여부를 검증해 타 사용자 주문 환불과 중복 환불을 차단했습니다.

* **재고 동시성**

  * 동시 주문 상황에서 Lost Update와 초과 판매 가능성을 재현했습니다.
  * 상품 재고 조회 구간에 DB 비관적 락을 적용해 재고 차감 요청이 순차 처리되도록 수정했습니다.

* **검색 단순화**

  * 초기에는 Elasticsearch를 검토했지만, 현재 검색 조건에서는 RDB와 QueryDSL로 충분하다고 판단했습니다.
  * Elasticsearch 의존성을 제거하고 QueryDSL 기반 동적 검색으로 단순화했습니다.

* **배포 자동화**

  * GitHub Actions, Docker, AWS EC2 기반 배포 흐름을 구성하고 배포를 검증했습니다.
  * 현재 EC2 인스턴스는 비용 관리를 위해 중지한 상태입니다.

---

### [Filmo](https://github.com/ohujj/CMC-Hackathon) — 영화 기록 앱 백엔드

영화관에서의 순간을 기록하는 앱 서비스의 백엔드 API를 구현했습니다.
Ne(o)rdinary Hackathon 우수상, Filmo - CMC + UMC 연합 해커톤 10팀 중 3위를 기록했습니다.

#### 담당한 내용

* Android 앱 클라이언트와 연동되는 REST API 구현
* 공통 응답 스펙과 예외 처리 구조 구현
* 토큰 기반 인증 흐름 구현
* GitHub Actions, Docker Hub, AWS EC2 기반 배포 흐름 구성

---

## Portfolio Focus

현재 포트폴리오에서는 아래 경험을 중심으로 정리하고 있습니다.

* 결제 실패처럼 표시되던 운영 이슈의 원인 분리 및 로그 추적성 개선
* enum 공유 인스턴스에 요청별 메시지를 저장하던 공통 예외 처리 구조 개선
* 동일 예약 자원에 대한 중복 예약 방지를 위한 DB 비관적 락 적용
* hanplane의 결제 confirm 멱등성, 보정 배치, 환불/재고 정합성 구현

---

## Contact

* Email: [hyeonwoo5729@gmail.com](mailto:hyeonwoo5729@gmail.com)
* GitHub: https://github.com/ohujj
