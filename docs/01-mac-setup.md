# 01. 맥북 세팅 — 복사·붙여넣기만 하면 끝

**터미널을 처음 써도 됩니다.** 회색 박스를 그대로 복사해서 터미널에 붙여넣고 Enter만 치면 됩니다.
각 단계마다 **"이렇게 나오면 성공"** 을 적어뒀으니 화면과 비교해보세요.

---

## 시작 전에 — 이것만 알면 됩니다

### 터미널 여는 법
`Command(⌘) + Space` → `터미널` 이라고 입력 → Enter

검은(또는 흰) 창이 뜨고 이렇게 생긴 줄이 보이면 준비 완료입니다.

```
사용자이름@맥북 ~ %
```

### 붙여넣기 규칙 4가지

| 상황 | 어떻게 |
|---|---|
| 회색 박스 복사 | 박스 오른쪽 위 복사 버튼, 또는 드래그 후 `⌘+C` |
| 터미널에 붙여넣기 | `⌘+V` → **Enter** |
| **비밀번호를 물어볼 때** | 맥 로그인 비번을 칩니다. **화면에 아무것도 안 보이는 게 정상**입니다. 그냥 치고 Enter |
| `(y/N)` 또는 `Press RETURN` | `y` 입력 후 Enter, 또는 그냥 Enter |

### 이것만 기억하세요
- 글자가 와르르 쏟아지는 건 **정상**입니다. 설치 중이라는 뜻이에요.
- 다시 `사용자이름@맥북 ~ %` 줄이 나타나면 그 명령이 **끝난 것**입니다.
- `warning:` 는 무시해도 됩니다. `error:` 만 신경 쓰면 됩니다.
- 중간에 막히면 → 맨 아래 [문제 해결](#문제-해결) 표를 보세요.

⏱️ 전체 소요시간 **약 30분** (설치 대기시간이 대부분)

---

# 1단계. 개발 도구 설치 (5~10분)

맥에 기본으로 필요한 도구를 깝니다.

```bash
xcode-select --install
```

**▶ 이렇게 나오면 성공 (A)** — 팝업창이 뜹니다.
```
"xcode-select" 명령을 실행하려면 명령어 라인 개발자 도구가 필요합니다.
```
→ **[설치]** 버튼 클릭 → **[동의]** → 진행바가 다 찰 때까지 기다립니다 (5~10분).

**▶ 이렇게 나와도 성공 (B)** — 이미 깔려 있다는 뜻입니다. 그냥 2단계로.
```
xcode-select: error: command line tools are already installed,
use "Software Update" to install updates
```

> `error` 라고 써 있어도 (B)는 정상입니다. 놀라지 마세요.

---

# 2단계. Homebrew 설치 (5분)

맥용 앱스토어 같은 것. 앞으로 필요한 프로그램을 전부 이걸로 깝니다.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**중간에 두 번 멈춥니다:**

**① 이렇게 나오면 → Enter**
```
Press RETURN/ENTER to continue or any other key to abort:
```

**② 이렇게 나오면 → 맥 로그인 비밀번호 입력 후 Enter** (화면에 안 보이는 게 정상)
```
Password:
```

**▶ 이렇게 나오면 성공**
```
==> Installation successful!

==> Next steps:
- Run these commands in your terminal to add Homebrew to your PATH:
```

### 이어서 — Homebrew 등록 (이것도 꼭 하세요)

아래 3줄을 **통째로** 복사해서 붙여넣으세요.

```bash
if [ -x /opt/homebrew/bin/brew ]; then BREWPATH=/opt/homebrew/bin/brew; else BREWPATH=/usr/local/bin/brew; fi
echo "eval \"\$($BREWPATH shellenv)\"" >> ~/.zprofile
eval "$($BREWPATH shellenv)"
```

아무 반응 없이 다음 줄이 나오면 잘 된 겁니다. 확인해봅시다.

```bash
brew --version
```

**▶ 이렇게 나오면 성공** (숫자는 다를 수 있음)
```
Homebrew 4.6.0
```

**▶ 이렇게 나오면 실패**
```
zsh: command not found: brew
```
→ 터미널을 완전히 종료(`⌘+Q`)하고 다시 열어서 `brew --version` 재시도.
→ 그래도 안 되면 위 3줄 블록을 다시 붙여넣기.

---

# 3단계. Git · GitHub CLI · VS Code 설치 (5분)

세 개를 한 번에 깝니다.

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

---

# 4단계. Git에 내 정보 등록 (1분)

⚠️ **이 단계만 직접 수정이 필요합니다.**
아래 블록을 복사한 뒤, **따옴표 안의 내용 두 군데를 본인 것으로 바꾸고** 붙여넣으세요.

```bash
git config --global user.name "홍길동"
git config --global user.email "hong@example.com"
git config --global init.defaultBranch main
```

예시:
```bash
git config --global user.name "Jihun Kim"
git config --global user.email "jihun@company.com"
git config --global init.defaultBranch main
```

**▶ 확인**

```bash
git config --global --list | grep user
```

**▶ 이렇게 나오면 성공**
```
user.name=Jihun Kim
user.email=jihun@company.com
```

> 여기 적은 이름/이메일이 나중에 작업 기록에 남습니다. 회사 이메일 권장.

---

# 5단계. GitHub 로그인 (3분)

```bash
gh auth login --hostname github.com --git-protocol https --web
```

**▶ 이런 화면이 나옵니다**
```
! First copy your one-time code: A1B2-C3D4
Press Enter to open github.com in your browser...
```

**할 일 (순서대로):**

1. `A1B2-C3D4` 같은 **8자리 코드를 복사**합니다 (사람마다 다름)
2. 터미널에서 **Enter** → 브라우저가 자동으로 열립니다
3. GitHub 로그인 (아직 계정이 없으면 https://github.com/signup 에서 먼저 가입)
4. 코드 입력칸에 **붙여넣기** → **Continue**
5. **Authorize github** 버튼 클릭
6. 터미널로 돌아옵니다

**▶ 이렇게 나오면 성공**
```
✓ Authentication complete.
✓ Configured git protocol
✓ Logged in as 내깃허브아이디
```

**▶ 혹시 아래 질문이 뜨면** (버전에 따라 나올 수 있음)
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

# 6단계. Claude Code 설치 (5분)

드디어 본체입니다.

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

**▶ 이렇게 나오면 성공**
```
Claude Code installed successfully!
```

### ⚠️ 여기서 터미널을 껐다 켜세요

`⌘+Q` 로 터미널을 완전히 종료한 뒤 다시 엽니다. (안 하면 다음 명령이 실패합니다)

```bash
claude --version
```

**▶ 이렇게 나오면 성공** (숫자는 다를 수 있음)
```
2.0.14 (Claude Code)
```

**▶ `command not found: claude` 가 나오면** 아래를 붙여넣고 다시 시도:
```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
claude --version
```

---

# 7단계. Claude 로그인 (2분)

```bash
claude
```

처음 실행하면 질문 3개가 순서대로 나옵니다. **화살표 키(↑↓)로 고르고 Enter** 입니다.

### 질문 ① 화면 색상
```
Choose the text style that looks best with your terminal:
❯ Dark mode
  Light mode
```
→ 아무거나 골라도 됩니다. 그냥 **Enter**.

### 질문 ② 로그인 방법 ⭐ 중요
```
Select login method:
❯ 1. Claude account with subscription
  2. Anthropic Console account
```
→ **1번 (Claude account with subscription)** 선택 후 Enter.

> 2번은 API 요금이 따로 나가는 방식입니다. 구독(Pro/Max)을 쓸 거면 반드시 **1번**.

### 질문 ③ 브라우저 인증
브라우저가 자동으로 열립니다. → Claude 계정 로그인 → **Authorize** 클릭
→ 터미널로 돌아오면 로그인 완료.

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

`>` 프롬프트가 보이면 끝입니다. 여기에 한국어로 아무거나 쳐보세요.

```
> 안녕! 지금 내가 있는 폴더가 어디야?
```

**나가는 법:** `/exit` 입력 후 Enter (또는 `Ctrl+C` 두 번)

---

# 8단계. 레포 받기 (1분)

⚠️ 이 레포는 **비공개(Private)** 입니다. 먼저 **초대 이메일의 링크를 눌러 수락**하세요.

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

**▶ 이렇게 나오면 초대 수락이 안 된 것**
```
remote: Repository not found.
```
→ 초대 메일 확인, 또는 https://github.com/jihunx-collab/TY_AI 접속해서 수락.

### 이제 여기서 클로드 실행

```bash
claude
```

```
> 이 레포 구조랑 README 읽고 뭘 하는 곳인지 설명해줘
```

🎉 **설치 끝!** 다음은 → [02-skill-guide.md](02-skill-guide.md)

---

# 전체 점검

한 번에 다 확인하고 싶으면 아래를 통째로 붙여넣으세요.

```bash
echo "── 설치 점검 ──"
brew --version    | head -1
git --version
gh --version      | head -1
claude --version
gh auth status 2>&1 | grep "Logged in"
echo "──────────────"
```

**▶ 이렇게 5줄이 다 나오면 완료**
```
── 설치 점검 ──
Homebrew 4.6.0
git version 2.51.0
gh version 2.65.0
2.0.14 (Claude Code)
  ✓ Logged in to github.com account 내아이디
──────────────
```

빠진 줄이 있으면 그 단계로 돌아가세요.

---

# 문제 해결

| 화면에 나온 것 | 뜻 | 해결 |
|---|---|---|
| `command not found: brew` | Homebrew 경로 등록 안 됨 | 터미널 `⌘+Q` 후 재실행 → 2단계 "Homebrew 등록" 3줄 다시 |
| `command not found: claude` | Claude 경로 등록 안 됨 | 6단계 아래쪽 `export PATH...` 블록 실행 |
| `command not found: gh` | 설치 안 됨 | 3단계 `brew install git gh` 다시 |
| `Permission denied` | 권한 부족 | 명령 맨 앞에 `sudo ` 를 붙여서 재실행 (⚠️ Homebrew 설치엔 붙이지 말 것) |
| `Repository not found` | 초대 미수락 | 초대 메일 링크 클릭해서 수락 |
| git push 할 때 비번을 물어봄 | GitHub 로그인 만료 | `gh auth login --hostname github.com --git-protocol https --web` 다시 |
| 클로드가 계속 "허용할까요?" 물어봄 | 승인 모드 | 클로드 안에서 `Shift + Tab` |
| 클로드 답변이 이상함 / 헤맴 | 대화가 길어짐 | 클로드 안에서 `/clear` 후 다시 요청 |
| `xcode-select: error: ... already installed` | 이미 설치됨 | **정상.** 그냥 넘어가세요 |

## 그래도 막히면 — 클로드한테 물어보세요

에러 메시지를 **그대로 복사**해서 터미널에 이렇게 치면 됩니다.

```bash
claude "터미널에서 이 에러가 났어. 어떻게 고쳐? → 여기에 에러메시지 붙여넣기"
```

실제 예시:
```bash
claude "brew install 했는데 Error: Permission denied @ dir_s_mkdir 라고 나와. 맥북이고 어떻게 고쳐?"
```

---

# 부록. 나중에 필요하면 (지금은 건너뛰세요)

### VS Code 연동 — 클로드가 고친 내용을 보기 좋게

1. VS Code 실행
2. `⌘ + Shift + P` → `shell command` 입력 → **Shell Command: Install 'code' command in PATH** 선택
3. 터미널에서:
```bash
code --install-extension anthropic.claude-code
```

이후 VS Code 안에서 터미널(`Ctrl + \``)을 열고 `claude` 를 실행하면,
클로드가 파일을 고칠 때마다 **변경 전/후를 나란히** 보여줍니다.

### 보고서를 Word / PDF 로 변환

```bash
brew install pandoc
brew install --cask libreoffice
```

사용:
```bash
# 마크다운 → 워드
pandoc 투자심의보고서.md -o 투자심의보고서.docx

# 워드 → PDF
soffice --headless --convert-to pdf 투자심의보고서.docx
```

> 이것도 클로드한테 시키면 됩니다: `> 방금 만든 보고서 워드로 변환해줘`

### cmux — 클로드 여러 개 동시에 돌리기

보고서 3~4건을 병렬로 처리할 때 유용합니다. **익숙해진 뒤에** 하세요.

```bash
brew tap manaflow-ai/cmux
brew install --cask cmux
```

공식: https://cmux.com

### Claude Code 업데이트 (한 달에 한 번쯤)

```bash
claude update
```
