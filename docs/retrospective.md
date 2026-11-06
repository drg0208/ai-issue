# 회고 — 2-스프린트

## Sprint 1 (Week 1: EDA & Descriptive Stats)

### Why
- 1주차 목표는 데이터 intake → 기술통계/EDA 리포트 MVP.

### What
- 완료: Issue #2, #3, #4, #5, #10
- 결과: 데이터 정제/이상치/기술통계/EDA 리포트/테스트 구축

### How
- pandas 기반 파이프라인 + pytest 커버리지 82%

### Result
- 안정 입력/EDA MVP 확보, 회귀 테스트 토대 마련

### Start / Stop / Continue
- Start: golden dataset 기반 회귀 테스트 강화
- Stop: 수동 차트 옵션 과다 추가
- Continue: 작은 PR 단위, 테스트 우선 개발

## Sprint 2 (Week 2: Inference & Reporting)

### Why
- MVP에 추론/CI/배포 파이프라인을 얹어 릴리스 준비

### What
- 완료: Issue #6, #7, #8, #9, #11 (Issue #1 릴리스)
- 결과: 가설검정 모듈, 신뢰구간/효과크기, CLI 예제, 문서, CI

### How
- scipy.stats + GitHub Actions 매트릭스

### Result
- v0.1.0 릴리스 준비 완료, 자동 품질 게이트 확보

### Start / Stop / Continue
- Start: 성능/대용량 데이터 benchmark
- Stop: README 수동 반복 업데이트
- Continue: WWH 기반 이슈-문서 동시 갱신
