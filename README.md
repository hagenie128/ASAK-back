# ASAK 백엔드

> **작업 시작점:** [ASAK 프로젝트 작업 허브](../ASAK/PROJECT_HUB.md) → 기능 한 개 선택 → 이 저장소 코드 수정 → 워크로그 기록.

## 중앙 문서

- [ASAK 문서 색인](../ASAK/docs/README.md)
- [Product Bible Pack 11 — 백엔드 구현](../ASAK/docs/product_bible/11_Backend_Implementation/README.md)
- [Product Bible Pack 12 — 프론트엔드 구현](../ASAK/docs/product_bible/12_Frontend_Implementation/README.md)
- [현재 구현 맵](../ASAK/docs/planning/CURRENT_IMPLEMENTATION_MAP.md)
- [구현 우선순위](../ASAK/docs/planning/IMPLEMENTATION_PRIORITY.md)
- [백엔드 구현 계획](IMPLEMENTATION_PLAN.md)
- [API·응답 가이드](../ASAK/docs/implementation_guide/04_API_DB_IMPLEMENTATION.md)

ASAK 키오스크 API용 Spring Boot 백엔드 작업 공간입니다.

## 현재 상태

이 폴더는 Spring Boot 4.1.0 / Java 25 백엔드 골격입니다. Gradle 빌드 설정과 health 엔드포인트는 준비되어 있고, 메뉴·주문·결제·관리자 업무 API는 아직 구현되지 않았습니다.

## 실행과 검증

```powershell
cd C:\ASAK-workspace\ASAK-back
.\gradlew.bat bootRun
.\gradlew.bat test
```

API 구현 시작 전에는 `IMPLEMENTATION_PLAN.md`와 중앙 API 응답 가이드를 확인한다. Product Bible의 Draft contract는 목표 DTO이며, 실제 Controller가 생기기 전에는 구현 완료로 표시하지 않는다.

## 현재 소스 구조

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

## 첫 번째 엔드포인트

백엔드 빌드 설정이 마무리된 뒤, 가장 먼저 확인하는 엔드포인트는 다음과 같습니다.

```text
GET http://127.0.0.1:8080/api/health
```

예상 응답:

```json
{"success":true,"status":200,"code":"HEALTH_OK","message":"ASAK backend is running","data":{"status":"UP"}}
```

## 데이터 경계

- 백엔드 코드는 이 폴더에만 둡니다.
- 파이프라인 결과물, seed JSON, 메뉴 이미지는 이 폴더에 넣지 않습니다.
- 필요할 때만 루트 수준 폴더에서 공유 데이터를 읽습니다.
  - `../data-pipeline/phase1/output/`
  - `../asak-data/seed/`
  - `../asak-data/images/menu/`
