# 01. 태엽 설치 — 복사·붙여넣기만 하면 끝

**터미널을 처음 써도 됩니다.** 회색 박스를 그대로 복사해서 붙여넣고 Enter만 치면 됩니다.
각 단계마다 **"▶ 이렇게 나오면 성공"** 을 적어뒀으니 화면과 비교만 하세요.

⏱️ **10분이면 클로드가 돌아갑니다.**

---

## 준비물

| | 필요한 것 | 어디서 |
|---|---|---|
| ✅ | **Claude 계정 + 구독 (Pro, 월 $20~)** | https://claude.ai — 이것만 결제하면 됩니다 |
| ✅ | **git** | 대부분 이미 깔려 있습니다. 없으면 팝업이 떠서 클릭 한 번이면 끝 (3단계) |
| ⬜ | VS Code, GitHub 계정, Homebrew 등 | 지금은 필요 없습니다. → [부록](#부록-나중에-필요해지면) |

> 이 레포는 **공개**라서 GitHub 계정이나 로그인 없이 그냥 받을 수 있습니다.

## 목차

| 단계 | 내용 | 시간 |
|---|---|---|
| 0 | [시작 전에 알아둘 것](#0-시작-전에--이것만-알면-됩니다) | 2분 |
| 1 | [Claude Code 설치](#1단계-claude-code-설치-2분) | 2분 |
| 2 | [Claude 로그인](#2단계-claude-로그인-3분) | 3분 |
| 3 | [레포 받기](#3단계-레포-받기-2분) | 2분 |
| — | [전체 점검](#전체-점검) · [문제 해결](#문제-해결) · [부록](#부록-나중에-필요해지면) | — |

---

# 0. 시작 전에 — 이것만 알면 됩니다

## 터미널 여는 법

`Command(⌘) + Space` → `터미널` 입력 → Enter

> **cmux를 깔았다면** `터미널` 대신 `cmux` 를 입력해서 여세요. 아래 내용은 전부 똑같습니다.
> (cmux도 터미널입니다. 나중에 클로드를 여러 개 동시에 돌릴 때 편해집니다)

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

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

**▶ 이렇게 나오면 성공**
```
Downloading Claude Code...
Installing to ~/.local/bin/claude
Claude Code installed successfully!
```

## ⚠️ 여기서 터미널을 껐다 켜세요

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

# 2단계. Claude 로그인 (3분)

```bash
claude
```

처음 실행하면 질문이 순서대로 나옵니다. **화살표 키(↑↓)로 고르고 Enter** 입니다.

## 질문 ① 화면 색상
```
Choose the text style that looks best with your terminal:
❯ Dark mode
  Light mode
```
→ 아무거나 골라도 됩니다. 그냥 **Enter**.

## 질문 ② 로그인 방법 ⭐ 여기가 중요
```
Select login method:
❯ 1. Claude account with subscription
  2. Anthropic Console account
```
→ **1번 (Claude account with subscription)** 선택 후 Enter.

> ⚠️ 2번은 쓴 만큼 요금이 청구되는 방식입니다. 구독(Pro/Max)을 쓸 거면 **반드시 1번**.

## 질문 ③ 브라우저 인증
브라우저가 자동으로 열립니다 → Claude 계정 로그인 → **Authorize** 클릭
→ 터미널로 자동으로 돌아옵니다.

> 계정이 없으면 https://claude.ai 에서 가입하고 **Pro 구독**을 먼저 하세요.
> 구독 없이는 Claude Code가 안 돌아갑니다.

## 질문 ④ 폴더 신뢰
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

## 🎉 지금 바로 써보세요

`>` 뒤에 한국어로 아무거나 쳐도 됩니다.

```
> 안녕! 지금 내가 있는 폴더가 어디야?
```

```
> 맥 터미널에서 제일 자주 쓰는 명령어 5개만 알려줘
```

**나가는 법:** `/exit` 입력 후 Enter (또는 `Ctrl+C` 를 두 번)

---

# 3단계. 레포 받기 (2분)

가이드와 팀 스킬이 들어있는 폴더를 내 맥으로 가져옵니다.
**공개 레포라서 로그인이 필요 없습니다.**

클로드 안이면 `/exit` 로 나온 뒤, 먼저 `git` 이 있는지 5초만 확인합니다:

```bash
git --version
```

- **`git version 2.51.0`** 처럼 나오면 → **이미 있습니다.** 바로 아래로 넘어가세요.
- **팝업이 뜨면** → **[설치]** → **[동의]** → 5~10분 기다렸다가 아래로.

> 별도로 뭘 다운로드할 필요 없습니다. 맥이 알아서 깔아줍니다.

이제 받습니다:

```bash
cd ~
git clone https://github.com/jihunx-collab/TY_AI.git
cd TY_AI
```

**▶ 이렇게 나오면 성공**
```
Cloning into 'TY_AI'...
remote: Enumerating objects: 20, done.
Receiving objects: 100% (20/20), done.
```

## 이제 여기서 클로드 실행

```bash
claude
```

```
> 이 레포 구조랑 README 읽고 뭘 하는 곳인지 설명해줘
```

## 🎉 설치 끝!

**다음은 [README의 "첫날 실습"](../README.md#-설치-끝났으면-첫날-실습-30분) 으로 가세요.**
가짜 회사로 보고서를 하나 뽑아보는 30분짜리 연습입니다. 여기까지 해야 감이 잡힙니다.

> 앞으로 작업을 시작할 때는 항상 이 두 줄입니다:
> ```bash
> cd ~/TY_AI
> claude
> ```

---

# 전체 점검

```bash
echo "── 설치 점검 ──"
claude --version
git --version
ls ~/TY_AI/README.md && echo "레포 OK"
echo "──────────────"
```

**▶ 이렇게 나오면 완료**
```
── 설치 점검 ──
2.0.14 (Claude Code)
git version 2.51.0
/Users/내이름/TY_AI/README.md
레포 OK
──────────────
```

---

# 문제 해결

| 화면에 나온 것 | 뜻 | 해결 |
|---|---|---|
| `command not found: claude` | 경로 등록 안 됨 | 터미널 `⌘+Q` 후 재실행 → 그래도 안 되면 [1단계](#1단계-claude-code-설치-2분) 아래 `export PATH` 두 줄 |
| git 설치 팝업이 뜸 | git이 없음 | **[설치]** 클릭 후 10분 기다렸다가 다시 |
| `Invalid API key` / 로그인 실패 | 로그인 방법을 잘못 고름 | `claude` → `/login` → **1번** 다시 선택 |
| 로그인했는데 사용량 부족이라고 나옴 | 구독이 없음 | https://claude.ai 에서 Pro 구독 확인 |
| `Permission denied` | 권한 부족 | 명령 맨 앞에 `sudo ` 를 붙여 재실행 |
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
claude "claude --version 쳤더니 command not found 나와. 방금 설치했는데 왜 그래?"
```

---

# 부록. 나중에 필요해지면

**지금은 전부 건너뛰어도 됩니다.** 필요해질 때 그때 하세요.
아래 대부분은 **Homebrew**(맥용 앱스토어 같은 것)가 있으면 한 줄로 끝납니다.

<details>
<summary><b>Homebrew 설치</b> — 아래 것들을 한 줄로 깔게 해주는 도구</summary>

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

중간에 `Press RETURN` → Enter, `Password:` → 맥 비번(안 보이는 게 정상).

설치가 끝나면 아래 3줄을 통째로 붙여넣어 등록합니다 (M칩/인텔 자동 처리):

```bash
if [ -x /opt/homebrew/bin/brew ]; then BREWPATH=/opt/homebrew/bin/brew; else BREWPATH=/usr/local/bin/brew; fi
echo "eval \"\$($BREWPATH shellenv)\"" >> ~/.zprofile
eval "$($BREWPATH shellenv)"
```

확인: `brew --version` → `Homebrew 4.6.0` 같은 게 나오면 성공.
</details>

<details>
<summary><b>VS Code 연동</b> — 클로드가 고친 내용을 나란히 보기</summary>

VS Code가 없으면 https://code.visualstudio.com 에서 받아 **응용 프로그램** 폴더로 드래그.

연동:
1. VS Code 실행 → `⌘ + Shift + P` → `shell command` 입력
   → **Shell Command: Install 'code' command in PATH** 선택
2. 터미널에서: `code --install-extension anthropic.claude-code`

이후 VS Code 안에서 터미널(`Ctrl` + `` ` ``)을 열고 `claude` 를 실행하면,
클로드가 파일을 고칠 때마다 **변경 전/후를 나란히** 보여줍니다.
</details>

<details>
<summary><b>내가 만든 스킬을 팀에 공유하기</b> — GitHub 계정 + gh 필요</summary>

여기까지 올 필요는 스킬을 **다른 사람에게 나눠줄 때** 생깁니다.

1. GitHub 가입: https://github.com/signup
2. 레포 주인에게 **collaborator 초대**를 요청하고 수락
3. gh 설치: `brew install gh`
4. 로그인:
```bash
gh auth login --hostname github.com --git-protocol https --web
```
   → 8자리 코드 복사 → Enter → 브라우저에서 붙여넣기 → **Authorize**
5. 내 정보 등록 (따옴표 안을 본인 것으로):
```bash
git config --global user.name "홍길동"
git config --global user.email "hong@example.com"
```
6. 올리기 — 클로드한테 `> 방금 만든 스킬 커밋해서 push 해줘` 라고 하면 됩니다.
</details>

<details>
<summary><b>보고서를 Word / PDF 로 변환</b></summary>

```bash
brew install pandoc
brew install --cask libreoffice
```

```bash
pandoc 투자심의보고서.md -o 투자심의보고서.docx     # 마크다운 → 워드
soffice --headless --convert-to pdf 투자심의보고서.docx  # 워드 → PDF
```

외울 필요 없습니다. 클로드한테 시키면 됩니다: `> 방금 만든 보고서 워드로 변환해줘`
</details>

<details>
<summary><b>Claude Code 업데이트</b> — 한 달에 한 번쯤</summary>

```bash
claude update
```
</details>
