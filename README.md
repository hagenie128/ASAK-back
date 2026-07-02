# ASAK-back

`ASAK-back`은 `ASAK (A Salad A Kiosk)`의 실제 백엔드 저장소입니다.

현재는 기본 구조만 먼저 분리한 상태이며, 1차 크롤링 파이프라인은 별도로 `ASAK` 통합 저장소 안의 `data-pipeline/phase1`에서 관리합니다.

## 구조

```text
src/
  main/
    java/
    resources/
  test/
    java/
```

## 목적

- API 서버 구현
- 인증/권한
- 키오스크용 서비스 로직
- 프론트와 연결되는 백엔드 기능 개발
