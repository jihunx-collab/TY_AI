# 01. 맥북 세팅 (설치 명령어 전부)

터미널 열기: `Command + Space` → `터미널` 입력 → Enter
아래 블록을 **위에서부터 순서대로** 복사-붙여넣기 하면 됨.

---

## 0단계. 내 맥 확인

```bash
uname -m
```

- `arm64` → M1/M2/M3/M4 (애플 실리콘). 대부분 여기.
- `x86_64` → 인텔 맥.

Homebrew 경로가 달라져서 확인하는 것. 아래에서 다시 씀.

---

## 1단계. Xcode Command Line Tools (git 등 기본 도구)

```bash
xcode-select --install
```

- 팝업 뜨면 **설치** 클릭. 5~10분.
- `already installed` 나오면 이미 있는 것. 넘어가면 됨.

---

## 2단계. Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

- 맥 로그인 비밀번호 물어봄. 입력해도 화면에 안 보이는 게 정상. 그냥 치고 Enter.
- 설치 끝나면 **PATH 등록** (한 번만):

```bash
# 애플 실리콘(arm64)인 경우
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"

# 인텔(x86_64)인 경우
echo 'eval "$(/usr/local/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/usr/local/bin/brew shellenv)"
```

확인:

```bash
brew --version
```

버전 숫자 나오면 성공.

---

## 3단계. Git + GitHub CLI + VS Code 한 방에

```bash
brew install git gh
brew install --cask visual-studio-code
```

### Git 이름/이메일 등록 (커밋에 찍힘)

```bash
git config --global user.name "본인이름"
git config --global user.email "본인@이메일.com"
git config --global init.defaultBranch main
```

### GitHub 로그인

```bash
gh auth login
```

선택지가 순서대로 나옴. 이렇게 고르면 됨:

```
? What account do you want to log into?     → GitHub.com
? What is your preferred protocol?          → HTTPS
? Authenticate Git with your GitHub creds?  → Yes
? How would you like to authenticate?       → Login with a web browser
```

- 화면에 **8자리 코드**(예: `ABCD-1234`)가 뜸 → 복사
- Enter 누르면 브라우저 열림 → 코드 붙여넣기 → 권한 승인
- 터미널에 `✓ Logged in as ...` 나오면 끝

확인:

```bash
gh auth status
```

> 이걸 해두면 앞으로 `git push` 할 때 토큰/비밀번호 안 물어봄.

---

## 4단계. Claude Code 설치

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

설치 후 터미널을 **완전히 껐다 켜고** 확인:

```bash
claude --version
```

### 로그인

```bash
claude
```

- 처음 실행하면 로그인 방식 물어봄 → **Claude account with subscription** 선택
  (Pro/Max 구독으로 로그인. API 키 결제 아님)
- 브라우저 열리면 Anthropic 계정으로 로그인 → 승인
- 터미널로 돌아와서 프롬프트(`>`) 뜨면 성공

나가기: `/exit` 또는 `Ctrl + C` 두 번

### 업데이트 (가끔)

```bash
claude update
```

---

## 5단계. VS Code 연동 (선택이지만 추천)

VS Code 안에서 터미널 열고 `claude` 치면 자동으로 확장이 붙음.
수동으로 하려면:

```bash
# VS Code에서 `code` 명령 쓰게 등록
# VS Code 실행 → Cmd+Shift+P → "Shell Command: Install 'code' command in PATH" 선택

# 확장 설치
code --install-extension anthropic.claude-code
```

연동되면 좋은 점:
- 클로드가 고친 파일이 **diff 화면**으로 바로 보임
- VS Code에서 선택한 코드/텍스트를 클로드가 인식

---

## 6단계. 레포 받기

```bash
cd ~
git clone https://github.com/jihunx-collab/TY_AI.git
cd TY_AI
claude
```

끝. 이제 클로드 안에서 `스킬 목록 보여줘` 쳐보면 됨.

---

## (선택) cmux — 클로드 여러 개 동시에

보고서 3~4개를 병렬로 돌릴 때 유용. **처음엔 건너뛰어도 됨.**
macOS 전용 네이티브 터미널이고, 세로 탭으로 에이전트별 세션을 나눠서 관리함.

```bash
brew tap manaflow-ai/cmux
brew install --cask cmux
```

- 공식: https://cmux.com
- 소스: https://github.com/manaflow-ai/cmux

## (선택) 문서 변환 도구

보고서를 md → PDF/DOCX/PPTX 로 자동 변환할 거면:

```bash
brew install pandoc
brew install --cask libreoffice
```

변환 예시:

```bash
# 마크다운 → Word
pandoc reports/회사명/투자심의보고서.md -o 투자심의보고서.docx

# Word/PPT → PDF
soffice --headless --convert-to pdf 투자심의보고서.docx
```

---

## 문제 생겼을 때

| 증상 | 해결 |
|---|---|
| `command not found: brew` | 터미널 껐다 켜기. 그래도 안 되면 2단계 PATH 등록 다시 |
| `command not found: claude` | 터미널 껐다 켜기 → `echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc` 후 재실행 |
| `permission denied` | 명령 앞에 `sudo` 붙여보기 (Homebrew 설치엔 붙이지 말 것) |
| git push 할 때 비번 물어봄 | `gh auth login` 다시 (3단계) |
| 클로드가 자꾸 승인 물어봄 | `Shift + Tab` 으로 자동 승인 모드 |
| 응답이 이상하거나 헤맴 | `/clear` 로 대화 초기화 후 다시 |

**막히면 클로드한테 직접 물어보면 됨.** 터미널에서:

```bash
claude "brew 설치했는데 command not found 뜬다. 어떻게 고쳐?"
```
