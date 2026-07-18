# ASAK Backend

> **작업 시작점:** [ASAK 프로젝트 작업 허브](../ASAK/PROJECT_HUB.md) → 기능 한 개 선택 → 이 저장소 코드 수정 → 워크로그 기록.

## Central documentation

- [ASAK docs index](../ASAK/docs/README.md)
- [Product Bible Pack 11 — Backend Implementation](../ASAK/docs/product_bible/11_Backend_Implementation/README.md)
- [Product Bible Pack 12 — Frontend Implementation](../ASAK/docs/product_bible/12_Frontend_Implementation/README.md)
- [Current Implementation Map](../ASAK/docs/planning/CURRENT_IMPLEMENTATION_MAP.md)
- [Implementation Priority](../ASAK/docs/planning/IMPLEMENTATION_PRIORITY.md)
- [Backend Implementation Plan](IMPLEMENTATION_PLAN.md)
- [API·Response Guide](../ASAK/docs/implementation_guide/04_API_DB_IMPLEMENTATION.md)

Spring Boot backend workspace for the ASAK kiosk API.

## Current State

This folder is a Spring Boot 4.1.0 / Java 25 backend skeleton. Gradle build setup and the health endpoint are present; menu·order·payment·admin business APIs are not yet implemented.

## 실행과 검증

```powershell
cd C:\ASAK-workspace\ASAK-back
.\gradlew.bat bootRun
.\gradlew.bat test
```

API 구현 시작 전에는 `IMPLEMENTATION_PLAN.md`와 중앙 API 응답 가이드를 확인한다. Product Bible의 Draft contract는 목표 DTO이며, 실제 Controller가 생기기 전에는 구현 완료로 표시하지 않는다.

## Current Source Layout

```text
backend/
  build.gradle
  settings.gradle
  src/
    main/
      java/com/asak/backend/
      resources/application.yml
    test/
      java/com/asak/backend/
```

## First Endpoint

After the backend build setup is finalized, the first check endpoint is:

```text
GET http://127.0.0.1:8080/api/health
```

Expected response:

```json
{"success":true,"status":200,"code":"HEALTH_OK","message":"ASAK backend is running","data":{"status":"UP"}}
```

## Data Boundary

- Keep backend code here.
- Do not place pipeline outputs, seed JSON, or menu images in this folder.
- Read shared data from root-level folders only when needed:
  - `../data-pipeline/phase1/output/`
  - `../asak-data/seed/`
  - `../asak-data/images/menu/`
