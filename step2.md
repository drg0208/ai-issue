# Step 2: GitHub CLI 명령어 정리 (ai-issue)

이 문서는 `ai-issue` 저장소를 신규 GitHub 레포지토리로 만들고,
이슈/라벨/마일스톤을 구성하면서 사용한 명령어를 정리합니다.

## 1. 사전 확인

```powershell
& "C:\Program Files\GitHub CLI\gh.exe" --version
git rev-parse --is-inside-work-tree
git remote -v
git branch -a
```

## 2. GitHub CLI 설치 및 PATH 등록

```powershell
winget install GitHub.cli --accept-package-agreements --accept-source-agreements
Get-ChildItem "C:\Program Files\GitHub CLI"
$ghDir = "C:\Program Files\GitHub CLI"
$env:Path = "$env:Path;$ghDir"
[Environment]::SetEnvironmentVariable("Path", "$([Environment]::GetEnvironmentVariable('Path','User'));$ghDir", "User")
```

## 3. GitHub 로그인 (브라우저 인증)

```powershell
gh auth login --web --git-protocol https
gh auth status
```

## 4. 로컬 저장소 초기화 및 원격 생성

```powershell
Set-Location "C:\workspace\2. tongkye\ai-issue"
git init -b main
Set-Content -Path README.md -Value "# ai-issue" -Encoding UTF8
git add README.md
git commit -m "Initial commit"
gh repo create ai-issue --public --source=. --remote=origin --push
```

## 5. 최초 이슈 생성

```powershell
gh issue create --title "배포됨" --body " "
gh issue list
```

## 6. 저장소 설명/토픽 설정

```powershell
gh repo edit --description "Python 통계 분석 프로젝트: 탐색적 데이터 분석, 기술통계, 가설검정 및 리포팅" `
  --add-topic python --add-topic statistics --add-topic data-analysis --add-topic pandas
```

## 7. 라벨 생성

```powershell
gh label create statistics --color "0e8a16" --description "통계 분석/기능 관련"
gh label create data-cleaning --color "1d76db" --description "데이터 수집/정제 관련"
gh label create visualization --color "d4c5f9" --description "시각화/리포트 관련"
gh label create inference --color "5319e7" --description "가설검정/추론 관련"
gh label create tests --color "d93f0b" --description "테스트/커버리지"
gh label create priority:high --color "b60205" --description "우선순위 높음"
gh label create priority:medium --color "fbca04" --description "우선순위 중간"
gh label create priority:low --color "c2e0c6" --description "우선순위 낮음"
```

## 8. 마일스톤 생성 (2주)

```powershell
gh api -X POST repos/drg0208/ai-issue/milestones `
  -f title="Week 1: EDA & Descriptive Stats" `
  -f description="1주차: 데이터 탐색 및 기술통계 구현" `
  -f due_on="2026-11-13T23:59:59Z" `
  -f state="open"

gh api -X POST repos/drg0208/ai-issue/milestones `
  -f title="Week 2: Inference & Reporting" `
  -f description="2주차: 가설검정 및 리포트/배포" `
  -f due_on="2026-11-20T23:59:59Z" `
  -f state="open"
```

## 9. 2주치 예시 이슈 생성

```powershell
gh issue create --title "데이터 로딩/정제 파이프라인 구현" --milestone "Week 1: EDA & Descriptive Stats" --label "enhancement,data-cleaning,priority:high" --body "pandas 기반 CSV/Excel 입력, 결측치 처리, 컬럼 타입 검증"
gh issue create --title "기술통계 함수 구현 (평균/분산/표준편차/왜도/첨도)" --milestone "Week 1: EDA & Descriptive Stats" --label "enhancement,statistics,priority:high" --body "수치형 컬럼에 대한 기술통계 계산 및 엣지 케이스 처리"
gh issue create --title "이상치 탐지 및 처리 로직 구현" --milestone "Week 1: EDA & Descriptive Stats" --label "enhancement,statistics,priority:medium" --body "IQR/Z-score 기반 이상치 탐지와 winsorize/제거 옵션"
gh issue create --title "EDA 자동 리포트 생성" --milestone "Week 1: EDA & Descriptive Stats" --label "enhancement,visualization,priority:medium" --body "matplotlib/seaborn으로 분포/상관관계 리포트 자동 생성"
gh issue create --title "단위 테스트 및 커버리지 설정" --milestone "Week 1: EDA & Descriptive Stats" --label "enhancement,tests,priority:medium" --body "pytest 단위 테스트 및 커버리지(>=80%) 리포트 구성"

gh issue create --title "가설검정 모듈 구현 (t-test/ANOVA/chi-square)" --milestone "Week 2: Inference & Reporting" --label "enhancement,inference,priority:high" --body "t-test, ANOVA, chi-square 검정 및 p-value/효과크기 반환"
gh issue create --title "신뢰구간 및 효과크기 계산" --milestone "Week 2: Inference & Reporting" --label "enhancement,inference,statistics,priority:medium" --body "평균/비율 신뢰구간 및 Cohen's d 등 효과크기 계산"
gh issue create --title "CLI 및 노트북 사용 예제 작성" --milestone "Week 2: Inference & Reporting" --label "documentation,visualization,priority:medium" --body "CLI 명령 예제와 데모 노트북 제공"
gh issue create --title "GitHub Actions CI 파이프라인 구성" --milestone "Week 2: Inference & Reporting" --label "enhancement,tests,priority:low" --body "Python 버전 매트릭스 테스트/린트 CI 워크플로 추가"
gh issue create --title "README 및 API 문서 보강" --milestone "Week 2: Inference & Reporting" --label "documentation,priority:medium" --body "설치, 빠른 시작, API 레퍼런스 문서화"
```

## 10. 확인 명령

```powershell
gh label list
gh api repos/drg0208/ai-issue/milestones --jq '.[] | {number, title, due_on, open_issues}'
gh issue list --state all --limit 30
gh repo view
```

## 11. step2.md 원격 반영

```powershell
git add step2.md
git commit -m "docs: add step2 GitHub CLI command log"
git push origin main
```