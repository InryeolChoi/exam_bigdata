# 빅분기 준비용도
## 시험구성
* 총 180분
* 100점 만점에 60점 이상 합격
* 1유형 : 데이터 전처리 (3문제)
* 2유형 : 데이터 분석 (1문제)
* 3유형 : 통계적 가설검정 (2문제)

# uv로 실행하기
## uv 설치하기
macOS에서 homebrew를 통한 설치
```bash
brew install uv
```

Windows에서 PowerShell을 통한 설치
```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

## uv로 가상환경 생성
```zsh
# `uv venv` + `디렉토리 이름` + `--python + (버전)` + `--seed`
uv venv .venv --python 3.13 --seed
```

## uv로 가상환경 켜기 / 끄기
**가상환경 켜기**
```zsh
source .venv/bin/activate
```

**가상환경 끄기**
```zsh
deactivate
```

## uv로 패키지 추가 / 삭제
**uv로 패키지 추가하기**
```bash
# 기본 (런타임 의존성)
uv add pandas

# 개발 전용
uv add --dev pytest ruff

# 선택적 그룹(--group), 예: extras = ["viz"]
uv add --group viz seaborn plotly
```

**uv로 패키지 삭제하기**
```bash
# 기본삭제
uv remove pandas

# dev 전용 패키지 삭제
uv remove --dev pytest
```

## uv로 패키지 관리하기
* 기존 requirements.txt → “pyproject + uv.lock”로 대체
* pyproject.toml : 파이썬 패키지 종류 선언
* uv.lock : 파이썬 패키지 버전 선언

### 패키지 관리소 생성
* 이미 requirements.txt가 있다면
```bash
uv init --bare
uv add -r requirements.txt

# 필요 시
# uv pip compile pyproject.toml -o requirements.txt
```

### 패키지 관리소 업데이트
```zsh
# pyproject.toml 업그레이드 + uv.lock 업그레이드 + 가상환경에 설치
uv sync --upgrade
```