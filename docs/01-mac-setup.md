# 01. 맥북 세팅 — 복사·붙여넣기만 하면 끝

**터미널을 처음 써도 됩니다.** 회색 박스를 그대로 복사해서 붙여넣고 Enter만 치면 됩니다.
각 단계마다 **"▶ 이렇게 나오면 성공"** 을 적어뒀으니 화면과 비교만 하세요.

⏱️ **필수 단계만 하면 약 15분**, 전부 다 하면 30분 (대부분 설치 대기시간)

---

## 목차

| | 단계 | 필수? | 시간 |
|---|---|---|---|
| 0 | [시작 전에 알아둘 것](#0-시작-전에--이것만-알면-됩니다) | — | 2분 |
| 1 | [**Claude Code 설치**](#1단계-claude-code-설치-2분) | ✅ 필수 | 2분 |
| 2 | [**Claude 로그인**](#2단계-claude-로그인-2분) | ✅ 필수 | 2분 |
| 3 | [Homebrew 설치](#3단계-homebrew-설치-5분) | 🟡 권장 | 5분 |
| 4 | [git · gh · VS Code 설치](#4단계-git--gh--vs-code-설치-5분) | ✅ 필수 | 5분 |
| 5 | [Git에 내 정보 등록](#5단계-git에-내-정보-등록-1분) | ✅ 필수 | 1분 |
| 6 | [GitHub 로그인](#6단계-github-로그인-3분) | ✅ 필수 | 3분 |
| 7 | [레포 받기](#7단계-레포-받기-1분) | ✅ 필수 | 1분 |
| — | [전체 점검](#전체-점검) / [문제 해결](#문제-해결) | — | — |
| — | [부록 (나중에)](#부록-나중에-필요하면-지금은-건너뛰세요) | ⬜ 선택 | — |

### ❓ 미리 답하는 질문

<details>
<summary><b>Homebrew 꼭 깔아야 해요?</b> (눌러서 펼치기)</summary>

**아니요, 필수는 아닙니다.** Claude Code 자체는 Homebrew 없이 `curl` 한 줄로 깔립니다 (1단계).

그런데 그 다음에 필요한 `gh`(GitHub 로그인 도구)와 VS Code를 깔려면,
Homebrew가 없으면 매번 이렇게 해야 합니다:

> 홈페이지 접속 → 내 맥이 M칩인지 인텔인지 확인 → 맞는 파일 다운로드 → 열어서 드래그 → 반복

Homebrew를 5분 투자해서 깔아두면 이게 전부 `brew install 이름` 한 줄이 됩니다.
나중에 pandoc, cmux 같은 것도 마찬가지고요. **그래서 권장합니다.**

</details>

<details>
<summary><b>Xcode를 설치해야 하나요?</b></summary>

**거대한 Xcode 앱은 필요 없습니다.** `git` 이 들어있는 "명령어 라인 개발자 도구(약 1GB)"만 필요한데,
**3단계 Homebrew를 설치할 때 자동으로 같이 깔립니다.** 그래서 별도 단계가 없습니다.

Homebrew를 안 쓸 거라면 이것만 따로 깔면 됩니다:
```bash
xcode-select --install
```
</details>

<details>
<summary><b>돈이 드나요?</b></summary>

**Anthropic 구독(Claude Pro, 월 $20~) 하나만** 필요합니다.
나머지(GitHub, Homebrew, VS Code, git, gh)는 전부 무료입니다.
API 키를 따로 사지 않아도 구독으로 Claude Code가 그대로 돌아갑니다.
</details>

---

# 0. 시작 전에 — 이것만 알면 됩니다

## 터미널 여는 법

`Command(⌘) + Space` → `터미널` 입력 → Enter

검은(또는 흰) 창이 뜨고 이렇게 생긴 줄이 보이면 준비 완료입니다.

```
사용자이름@맥북 ~ %
```

## 붙여넣기 규칙 4가지

| 상황 | 어떻게 |
|---|---|
| 회색 박스 복사 | 박스 오른쪽 위 복사 버튼, 또는 드래그 후 `⌘+C` |
| 터미널에 붙여넣기 | `⌘+V` → **Enter** |
| **비밀번호를 물어볼 때** | 맥 로그인 비번을 칩니다. **화면에 아무것도 안 보이는 게 정상**입니다. 그냥 치고 Enter |
| `(y/N)` 또는 `Press RETURN` | `y` 입력 후 Enter, 또는 그냥 Enter |

## 이것만 기억하세요

- 글자가 와르르 쏟아지는 건 **정상**입니다. 설치 중이라는 뜻이에요.
- 다시 `사용자이름@맥북 ~ %` 줄이 나타나면 그 명령이 **끝난 것**입니다.
- `warning:` 는 무시해도 됩니다. `error:` 만 신경 쓰면 됩니다.
- 중간에 막히면 → 맨 아래 [문제 해결](#문제-해결) 표를 보세요.

---

# 1단계. Claude Code 설치 (2분)

본체부터 깝니다. **다른 걸 아무것도 안 깔아도 이건 됩니다.**

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

**▶ 이렇게 나오면 성공**
```
Downloading Claude Code...
Installing to ~/.local/bin/claude
Claude Code installed successfully!
```

### ⚠️ 여기서 터미널을 껐다 켜세요

`⌘+Q` 로 터미널을 **완전히 종료**한 뒤 다시 엽니다.
(방금 설치한 프로그램의 위치를 터미널이 아직 모르기 때문입니다. 안 하면 다음 명령이 실패합니다.)

확인:

```bash
claude --version
```

**▶ 이렇게 나오면 성공** (숫자는 다를 수 있습니다)
```
2.0.14 (Claude Code)
```

**▶ `command not found: claude` 가 나오면** 아래 두 줄을 붙여넣고 다시 시도하세요.
```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

---

# 2단계. Claude 로그인 (2분)

```bash
claude
```

처음 실행하면 질문이 순서대로 나옵니다. **화살표 키(↑↓)로 고르고 Enter** 입니다.

### 질문 ① 화면 색상
```
Choose the text style that looks best with your terminal:
❯ Dark mode
  Light mode
```
→ 아무거나 골라도 됩니다. 그냥 **Enter**.

### 질문 ② 로그인 방법 ⭐ 여기가 중요
```
Select login method:
❯ 1. Claude account with subscription
  2. Anthropic Console account
```
→ **1번 (Claude account with subscription)** 선택 후 Enter.

> ⚠️ 2번은 쓴 만큼 요금이 청구되는 방식입니다. 구독(Pro/Max)을 쓸 거면 **반드시 1번**.

### 질문 ③ 브라우저 인증
브라우저가 자동으로 열립니다 → Claude 계정 로그인 → **Authorize** 클릭
→ 터미널로 자동으로 돌아옵니다.

> 아직 계정이 없으면 https://claude.ai 에서 가입 후 Pro 구독을 먼저 하세요.

### 질문 ④ 폴더 신뢰
```
Do you trust the files in this folder?
❯ Yes, proceed
  No, exit
```
→ **Yes, proceed** 선택 후 Enter.

**▶ 이렇게 나오면 성공**
```
╭──────────────────────────────────────╮
│ ✻ Welcome to Claude Code             │
╰──────────────────────────────────────╯

>
```

### 🎉 지금 바로 써보세요

`>` 뒤에 한국어로 아무거나 쳐도 됩니다.

```
> 안녕! 지금 내가 있는 폴더가 어디야?
```

```
> 맥 터미널 기본 명령어 5개만 알려줘
```

**나가는 법:** `/exit` 입력 후 Enter (또는 `Ctrl+C` 를 두 번)

> 여기까지가 최소 세팅입니다. 이제 팀 레포를 받고 스킬을 공유하기 위해 GitHub 쪽을 설정합니다.

---

# 3단계. Homebrew 설치 (5분)

🟡 **필수는 아니지만 권장** — [왜 필요한지](#-미리-답하는-질문)

맥용 앱스토어 같은 것입니다. 앞으로 필요한 프로그램을 전부 한 줄로 깔 수 있게 해줍니다.
**git이 들어있는 개발자 도구도 이때 자동으로 같이 깔립니다.**

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**중간에 두 번 멈춥니다:**

**① 이렇게 나오면 → 그냥 Enter**
```
The Xcode Command Line Tools will be installed.

Press RETURN/ENTER to continue or any other key to abort:
```

**② 이렇게 나오면 → 맥 로그인 비밀번호 입력 후 Enter**
```
Password:
```
> 화면에 아무 글자도 안 보이는 게 정상입니다. 그냥 치고 Enter 누르세요.

그 다음 몇 분간 글자가 쏟아집니다. 정상입니다. 기다리세요.

**▶ 이렇게 나오면 성공**
```
==> Installation successful!

==> Next steps:
- Run these commands in your terminal to add Homebrew to your PATH:
```

### 이어서 — Homebrew 등록 (이것도 꼭 하세요)

방금 화면이 "PATH에 추가하라"고 안내한 부분입니다. 아래 3줄을 **통째로** 복사해서 붙여넣으세요.
(M칩이든 인텔이든 알아서 처리합니다.)

```bash
if [ -x /opt/homebrew/bin/brew ]; then BREWPATH=/opt/homebrew/bin/brew; else BREWPATH=/usr/local/bin/brew; fi
echo "eval \"\$($BREWPATH shellenv)\"" >> ~/.zprofile
eval "$($BREWPATH shellenv)"
```

아무 반응 없이 다음 줄이 나오면 잘 된 겁니다. 확인해봅시다.

```bash
brew --version
```

**▶ 이렇게 나오면 성공** (숫자는 다를 수 있습니다)
```
Homebrew 4.6.0
```

**▶ `zsh: command not found: brew` 가 나오면**
→ 터미널을 `⌘+Q` 로 완전히 종료하고 다시 열어서 `brew --version` 재시도
→ 그래도 안 되면 위 3줄 블록을 다시 붙여넣기

---

# 4단계. git · gh · VS Code 설치 (5분)

- **git** — 파일 변경 이력 관리. 팀과 스킬을 주고받는 데 필수
- **gh** — GitHub 로그인 도구. 이게 있으면 비밀번호/토큰을 안 만들어도 됨
- **VS Code** — 보고서 편집기. 클로드가 고친 내용을 보기 좋게 보여줌

```bash
brew install git gh
```

```bash
brew install --cask visual-studio-code
```

**▶ 이렇게 나오면 성공** (`==>` 줄이 잔뜩 지나간 뒤)
```
🍺  /opt/homebrew/Cellar/git/2.51.0: 1,7xx files, 51.2MB
🍺  gh was successfully installed!
🍺  visual-studio-code was successfully installed!
```

맥주잔 이모지(🍺)가 나오면 성공입니다.

> 두 번째 명령에서 비밀번호를 물어보면 맥 로그인 비번을 입력하세요.

<details>
<summary><b>Homebrew를 안 깔았다면</b> (눌러서 펼치기)</summary>

- **git** — 터미널에 `git --version` 을 치면 팝업이 뜨면서 자동 설치됩니다.
- **VS Code** — https://code.visualstudio.com 에서 다운로드 → 압축 풀고 **응용 프로그램** 폴더로 드래그
- **gh** — https://github.com/cli/cli/releases 에서 최신 버전의
  `gh_..._macOS_arm64.pkg` (M칩) 또는 `gh_..._macOS_amd64.pkg` (인텔) 다운로드 후 실행
  - 내 맥이 뭔지 모르겠으면: 터미널에 `uname -m` → `arm64` 면 M칩, `x86_64` 면 인텔

</details>

---

# 5단계. Git에 내 정보 등록 (1분)

⚠️ **여기만 직접 수정이 필요합니다.**
아래 블록을 복사한 뒤, **따옴표 안 두 군데를 본인 것으로 바꾸고** 붙여넣으세요.

```bash
git config --global user.name "홍길동"
git config --global user.email "hong@example.com"
git config --global init.defaultBranch main
```

실제로는 이렇게 됩니다:
```bash
git config --global user.name "Jihun Kim"
git config --global user.email "jihun@company.com"
git config --global init.defaultBranch main
```

**▶ 확인**

```bash
git config --global --list | grep user
```

```
user.name=Jihun Kim
user.email=jihun@company.com
```

> 여기 적은 이름/이메일이 앞으로 모든 작업 기록에 남습니다. 회사 이메일을 권장합니다.
> 나중에 바꾸고 싶으면 위 명령을 다시 실행하면 덮어써집니다.

---

# 6단계. GitHub 로그인 (3분)

```bash
gh auth login --hostname github.com --git-protocol https --web
```

**▶ 이런 화면이 나옵니다**
```
! First copy your one-time code: A1B2-C3D4
Press Enter to open github.com in your browser...
```

**할 일 (순서대로):**

1. `A1B2-C3D4` 같은 **8자리 코드를 복사**합니다 (사람마다 다릅니다)
2. 터미널에서 **Enter** → 브라우저가 자동으로 열립니다
3. GitHub 로그인 — 계정이 없으면 https://github.com/signup 에서 먼저 가입
4. 코드 입력칸에 **붙여넣기** → **Continue**
5. **Authorize github** 버튼 클릭
6. 터미널로 돌아옵니다

**▶ 이렇게 나오면 성공**
```
✓ Authentication complete.
✓ Configured git protocol
✓ Logged in as 내깃허브아이디
```

**▶ 혹시 이 질문이 뜨면** (버전에 따라 나올 수 있습니다)
```
? Authenticate Git with your GitHub credentials? (Y/n)
```
→ `Y` 입력 후 Enter

**▶ 확인**

```bash
gh auth status
```

```
github.com
  ✓ Logged in to github.com account 내깃허브아이디
```

> 이걸 해두면 앞으로 파일을 올릴 때 비밀번호를 안 물어봅니다.

---

# 7단계. 레포 받기 (1분)

⚠️ 이 레포는 **비공개(Private)** 입니다.
먼저 **초대 이메일의 링크를 눌러 수락**하거나, https://github.com/jihunx-collab/TY_AI 에 접속해 수락하세요.

터미널에서 (클로드 안이면 `/exit` 로 나온 뒤):

```bash
cd ~
git clone https://github.com/jihunx-collab/TY_AI.git
cd TY_AI
```

**▶ 이렇게 나오면 성공**
```
Cloning into 'TY_AI'...
remote: Enumerating objects: 12, done.
Receiving objects: 100% (12/12), done.
```

**▶ `remote: Repository not found.` 가 나오면**
초대 수락이 안 된 상태입니다. 위 링크에서 수락 후 다시 시도하세요.

### 이제 여기서 클로드 실행

```bash
claude
```

```
> 이 레포 구조랑 README 읽고 뭘 하는 곳인지 설명해줘
```

## 🎉 설치 끝!

다음 → **[02-skill-guide.md](02-skill-guide.md)** (보고서 양식을 스킬로 만드는 법)

> 앞으로 작업을 시작할 때는 항상 이 두 줄입니다:
> ```bash
> cd ~/TY_AI
> claude
> ```

---

# 전체 점검

한 번에 다 확인하고 싶으면 아래를 통째로 붙여넣으세요.

```bash
echo "── 설치 점검 ──"
claude --version
git --version
gh --version      | head -1
brew --version    | head -1
gh auth status 2>&1 | grep "Logged in"
echo "──────────────"
```

**▶ 이렇게 나오면 완료**
```
── 설치 점검 ──
2.0.14 (Claude Code)
git version 2.51.0
gh version 2.65.0
Homebrew 4.6.0
  ✓ Logged in to github.com account 내아이디
──────────────
```

빠진 줄이 있으면 해당 단계로 돌아가세요.
(`Homebrew` 줄만 없는 건 괜찮습니다 — 선택 사항이니까요.)

---

# 문제 해결

| 화면에 나온 것 | 뜻 | 해결 |
|---|---|---|
| `command not found: claude` | 경로 등록 안 됨 | 터미널 `⌘+Q` 후 재실행 → 그래도 안 되면 [1단계](#1단계-claude-code-설치-2분) 아래 `export PATH` 두 줄 |
| `command not found: brew` | 경로 등록 안 됨 | 터미널 `⌘+Q` 후 재실행 → [3단계](#3단계-homebrew-설치-5분) "Homebrew 등록" 3줄 다시 |
| `command not found: gh` | 설치 안 됨 | [4단계](#4단계-git--gh--vs-code-설치-5분) `brew install git gh` 다시 |
| `Permission denied` | 권한 부족 | 명령 맨 앞에 `sudo ` 를 붙여 재실행 (⚠️ Homebrew 설치 명령엔 붙이지 마세요) |
| `Repository not found` | 초대 미수락 | 초대 링크에서 수락 후 다시 clone |
| `git push` 할 때 비번을 물어봄 | GitHub 로그인 만료 | [6단계](#6단계-github-로그인-3분) 명령 다시 실행 |
| `xcode-select: error: ... already installed` | 이미 설치됨 | **정상.** 그냥 넘어가세요 |
| 클로드가 계속 "허용할까요?" 물어봄 | 매번 승인받는 모드 | 클로드 안에서 `Shift + Tab` |
| 클로드 답변이 이상하거나 헤맴 | 대화가 너무 길어짐 | 클로드 안에서 `/clear` 후 다시 요청 |
| 창을 닫아버렸는데 어디서부터? | — | 터미널 다시 열고 `cd ~/TY_AI` → `claude` |

## 그래도 막히면 — 클로드한테 물어보세요

에러 메시지를 **그대로 복사**해서 터미널에 이렇게 치면 됩니다.

```bash
claude "터미널에서 이 에러가 났어. 맥북인데 어떻게 고쳐? → 여기에 에러 붙여넣기"
```

실제 예시:
```bash
claude "brew install 했는데 Error: Permission denied @ dir_s_mkdir 라고 나와. 맥북이고 어떻게 고쳐?"
```

---

# 부록. 나중에 필요하면 (지금은 건너뛰세요)

## VS Code 연동 — 클로드가 고친 내용을 보기 좋게

1. VS Code 실행
2. `⌘ + Shift + P` → `shell command` 입력 → **Shell Command: Install 'code' command in PATH** 선택
3. 터미널에서:
```bash
code --install-extension anthropic.claude-code
```

이후 VS Code 안에서 터미널(`Ctrl` + `` ` ``)을 열고 `claude` 를 실행하면,
클로드가 파일을 고칠 때마다 **변경 전/후를 나란히** 보여줍니다.

## 보고서를 Word / PDF 로 변환

```bash
brew install pandoc
brew install --cask libreoffice
```

사용법:
```bash
# 마크다운 → 워드
pandoc 투자심의보고서.md -o 투자심의보고서.docx

# 워드 → PDF
soffice --headless --convert-to pdf 투자심의보고서.docx
```

> 외울 필요 없습니다. 클로드한테 시키면 됩니다: `> 방금 만든 보고서 워드로 변환해줘`

## cmux — 클로드 여러 개 동시에 돌리기

보고서 3~4건을 병렬로 처리할 때 유용합니다. **충분히 익숙해진 뒤에** 하세요.

```bash
brew tap manaflow-ai/cmux
brew install --cask cmux
```

공식: https://cmux.com

## Claude Code 업데이트 (한 달에 한 번쯤)

```bash
claude update
```
