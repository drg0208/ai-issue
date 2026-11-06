# TIL — Python 통계 프로젝트 (14일)

## Day 1 (Nov 6) — Issue #1 배포됨 환경/레포 부트스트랩
- Why: 독립 신규 레포와 이슈 추적으로 개발 시작점 정리
- What: git init, gh repo create, README, 라벨/마일스톤/이슈 세팅
- How: gh auth login --web, gh repo create, gh issue create
- Result: 원격 레포와 기본 협업 뼈대 생성 완료

## Day 2 (Nov 7) — Issue #2 데이터 로딩/정제 파이프라인
- Why: 모든 통계 기능은 안정 입력 파이프라인에 의존
- What: pandas CSV/Excel 로더, 컬럼 타입 검증, 결측치 옵션 추가
- How: DataFrame schema 검증 + 정제 함수 분리
- Result: 입력 데이터 품질 기반 마련

## Day 3 (Nov 8) — Issue #2 결측치 처리 옵션 확장
- Why: 데이터마다 결측 전략이 달라 단일 규칙은 위험
- What: drop/mean/median/ffill 옵션과 로그 기록
- How: strategy 파라미터 + 처리 메타데이터 반환
- Result: 재현 가능한 정제 이력 확보

## Day 4 (Nov 9) — Issue #4 이상치 탐지/처리
- Why: 이상치가 평균/분산을 크게 왜곡
- What: IQR, Z-score 탐지와 winsorize/제거 옵션
- How: 통계치 계산 함수 재사용, threshold 파라미터화
- Result: 빠르고 안전한 이상치 처리 흐름 확보

## Day 5 (Nov 10) — Issue #3 기술통계 (평균/분산/왜도/첨도)
- Why: EDA의 핵심은 요약 통계를 빠르게 보는 것
- What: describe 확장 함수와 엣지 케이스(n=0, NaN) 처리
- How: numpy/pandas 계산 + 입력 검증
- Result: 기본 통계 라이브러리 MVP 완성

## Day 6 (Nov 11) — Issue #5 EDA 자동 리포트
- Why: 분포/상관관계를 사람이 빠르게 확인해야 함
- What: matplotlib/seaborn 차트 생성 및 PNG/HTML 저장
- How: 리포트 builder 객체로 생성 로직 분리
- Result: 원클릭 EDA 리포트 산출 가능

## Day 7 (Nov 12) — Issue #10 테스트/커버리지
- Why: 통계 계산 회귀 방지 필요
- What: pytest 기반 단위 테스트, 커버리지 기준 80% 설정
- How: edge case fixture + CI 로컬 실행
- Result: 커버리지 82% 달성, 신뢰도 향상

## Day 8 (Nov 13) — Issue #6 가설검정 모듈 (t-test)
- Why: 두 집단 차이 검정은 기본 추론 기능
- What: 독립표본/대응표본 t-test와 p-value 반환
- How: scipy.stats + 결과 dataclass 정의
- Result: 추론 기능의 첫 모듈 추가

## Day 9 (Nov 14) — Issue #6 ANOVA / chi-square
- Why: 다집단/범주형 분석 수요 대응
- What: 일원 ANOVA, 교차표 chi-square 검정 추가
- How: 입력 형식 검증과 효과크기 계산 연결
- Result: 가설검정 모듈 보강

## Day 10 (Nov 15) — Issue #7 신뢰구간/효과크기
- Why: p-value만으로는 결론이 불충분
- What: 평균/비율 신뢰구간과 Cohen's d 계산
- How: bootstrap 옵션과 공식 기반 계산 분리
- Result: 해석 가능한 통계 리포트 강화

## Day 11 (Nov 16) — Issue #8 CLI/노트북 예제
- Why: 라이브러리 사용법을 빠르게 전달
- What: CLI 명령과 데모 노트북 작성
- How: argparse/typer로 명령 매핑, 예제 데이터 추가
- Result: 사용 진입 장벽 감소

## Day 12 (Nov 17) — Issue #9 README/API 문서
- Why: 신규 사용자를 위한 온보딩 필요
- What: 설치, 빠른 시작, API 레퍼런스 정리
- How: Markdown + docstring 기반 문서 생성
- Result: 프로젝트 사용성 향상

## Day 13 (Nov 18) — Issue #11 GitHub Actions CI
- Why: 머지 전 회귀 자동 확인 필요
- What: Python 매트릭스 테스트/린트 워크플로 추가
- How: GitHub Actions + pytest + ruff
- Result: 자동 품질 게이트 구축

## Day 14 (Nov 19) — Issue #1 배포됨/릴리스 준비
- Why: 2주 스프린트 목표는 동작 가능한 배포 산출물
- What: 릴리스 태그, changelog, 최종 검증
- How: gh release create, 이슈/PR 정리
- Result: v0.1.0 릴리스 준비 완료
