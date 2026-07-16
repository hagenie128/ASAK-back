# ASAK Backend 구현 계획

> Status: Current. 이 계획은 Spring Boot 구현 순서를 정한다. API 상세 DTO는 [중앙 API·응답 가이드](../ASAK/docs/implementation_guide/04_API_DB_IMPLEMENTATION.md)와 Product Bible의 기능별 Contract가 정본이다.

## 현재 상태

- 구현됨: Spring Boot 4.1.0, Java 25, `GET /api/health`, 공통 `ApiResponse` 골격.
- 미구현: menu/order/payment/admin domain의 Entity, Repository, Service, Controller, migration, business/API 테스트.
- 따라서 Figma와 문서의 API는 목표 계약이며 실행 가능한 endpoint가 아니다.

## 구현 순서

1. 공통 오류 envelope, validation, exception handler와 DTO/Mapper 규칙을 확정한다.
2. 메뉴 목록·상세 읽기 API를 구현한다. Kiosk의 SCR-003/004가 사용할 최소 데이터만 먼저 제공한다.
3. 주문 생성 API를 구현한다. 서버에서 메뉴·옵션·품절·수량을 검증하고 `totalAmount`를 재계산한다.
4. 결제 API를 구현한다. `idempotencyKey`, `APPROVED/FAILED`, `approvedAmount`, `approvedAt`, `waitingOrderCount`를 처리한다.
5. 관리자 주문 조회·상태 전이와 품절 관리 API를 구현한다.
6. 메뉴 관리·결제수단·매출 API는 MVP 우선순위와 Backend 준비 상태에 따라 추가한다.

## 세로 슬라이스 완료 조건

- Controller → Service → Repository → Entity/DB → DTO/Mapper → Test가 한 기능 단위로 연결된다.
- JSON은 camelCase, DB는 snake_case이며 Entity를 API 응답으로 직접 반환하지 않는다.
- 주문 가격은 클라이언트가 보낸 값이 아니라 서버 재계산 값이다.
- 상태 전이와 결제 중복은 서버에서 막는다. 완료 재요청은 중복 매출/TTS를 만들지 않는다.
- 오류는 `success`, `status`, `code`, `message`, `data` envelope로 반환하고 프론트가 복구 행동을 선택할 수 있게 한다.

## 구현 전 확인

- [ ] Screen ID와 05-C/06-C 상태를 확인했다.
- [ ] 기능별 API Contract가 Draft인지 Current인지 확인했다.
- [ ] 요청 DTO, 성공 DTO, 오류 code, DB 변경과 테스트를 함께 적었다.
- [ ] Kiosk/Admin의 기존 mock/store 필드와 adapter 영향 범위를 확인했다.

## 원본 링크

- [Backend Implementation Bible](../ASAK/docs/product_bible/11_Backend_Implementation/README.md)
- [Order API Contract](../ASAK/docs/product_bible/02_Order_Cart_Payment/docs/09-features/order/ORDER_API_CONTRACT.md)
- [Payment API Contract](../ASAK/docs/product_bible/02_Order_Cart_Payment/docs/09-features/payment/PAYMENT_API_CONTRACT.md)
- [Current Implementation Map](../ASAK/docs/planning/CURRENT_IMPLEMENTATION_MAP.md)
