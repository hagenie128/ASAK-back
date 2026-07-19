# ASAK Backend 구현 계획

> 기준일: **2026-07-20** · 코드/git 실측 (**`GET /api/health`만** business HTTP).  
> 문서 입구: [`ASAK/docs/START_HERE.md`](../ASAK/docs/START_HERE.md)  
> 정본 WBS: [`ASAK/docs/wiki/wbs-v2.md`](../ASAK/docs/wiki/wbs-v2.md) **WBS2-046 ~ WBS2-056** (P5)  
> 연동: **WBS2-057 ~ WBS2-060** (P6, 현재 BLOCKED)  
> Canonical API: [`ASAK/docs/governance/CANONICAL_CONTRACT_DECISIONS.md`](../ASAK/docs/governance/CANONICAL_CONTRACT_DECISIONS.md)

## 현재 상태

| 항목 | 상태 |
| --- | --- |
| Spring Boot 4.1.0 / Java 25 | 있음 |
| `GET /api/health` | **유일한** HTTP business endpoint |
| `ApiResponse` 골격 | 부분 (오류/validation 정책 미완) |
| Entity / Repository / Service / Controller (도메인) | **없음** |
| Flyway/JPA/schema 연결 | **없음** (스키마는 DevCopilot·ASAK docs에만) |
| 프론트 연동 | **불가** → Kiosk/Admin은 mock만 |

문서·Figma·DevCopilot의 API는 **목표 계약**이지 실행 endpoint가 아니다.

## Canonical 경로 (구현 목표)

```text
GET    /api/kiosk/menuList
GET    /api/kiosk/menuDetail/{menuId}
POST   /api/kiosk/orders
POST   /api/kiosk/payments
PATCH  /api/admin/soldOut
GET    /api/admin/orders ...
GET    /api/admin/sales/summary|monthly|daily
```

응답 필드: `totalAmount`, `approvedAmount`, `approvedAt`, `waitingOrderCount`  
JSON camelCase · DB snake_case · Entity를 API로 직접 반환하지 않음.

## 구현 순서 (WBS2)

| 순서 | WBS | 내용 |
| --- | --- | --- |
| 1 | WBS2-046~047 | persistence·schema/migration/seed 방식 결정 |
| 2 | WBS2-055 | 공통 envelope·validation·exception |
| 3 | WBS2-048~049 | 메뉴 목록·상세 세로 슬라이스 |
| 4 | WBS2-050~051 | 주문·결제 (서버 가격 재계산, idempotency) |
| 5 | WBS2-052~053 | 품절·관리자 주문/상태 |
| 6 | WBS2-054 | 매출 집계 |
| 7 | WBS2-056 | Modeler vs backend DB 감사 |
| 이후 | WBS2-057~060 | 프론트 adapter·실연동 |

## 세로 슬라이스 완료 조건

- Controller → Service → Repository → Entity/DB → DTO/Mapper → Test가 **한 기능**으로 연결
- 주문 가격은 **서버 재계산**
- 결제 중복·상태 전이는 서버에서 차단
- 오류는 `{ success, status, code, message, data }`

## 구현 전 체크

- [ ] Canonical path·DTO가 Product Bible Contract와 일치하는가
- [ ] Kiosk/Admin mock·store 필드와 adapter 영향 범위
- [ ] DevCopilot DB model(26+4)과 migration 범위
- [ ] WBS2 Primary Owner 확정 (`NEEDS_CONFIRMATION` 해소)

## 원본 링크

- [Backend Implementation Bible](../ASAK/docs/product_bible/11_Backend_Implementation/README.md)
- [Current Implementation Map](../ASAK/docs/planning/CURRENT_IMPLEMENTATION_MAP.md)
- [WBS 상태 메모](../ASAK/docs/wiki/wbs-status-notes.md)
- [DevCopilot sync](../ASAK/docs/wiki/devcopilot-sync-report.md)

## Documentation status

- Status: **Current (2026-07-20)** — health-only 사실 유지, WBS2 ID·Canonical 경로 명시.
