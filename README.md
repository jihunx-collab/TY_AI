# TY_AI — 클로드 코드 시작 가이드

투자심의보고서 같은 **금융 보고서를 클로드 코드로 자동화**하기 위한 세팅 + 작업 플로우.
맥북 기준. 순서대로 따라가면 됨.

---

## 용어 30초

- **클로드 코드(Claude Code)** — 터미널에서 돌아가는 AI 에이전트. 파일 읽고 쓰고 명령 실행함.
- **스킬(Skill)** — "이런 요청이 오면 이 절차로, 이 양식으로 만들어라"를 적어둔 폴더.
  한 번 만들어두면 `투심보고서 초안 잡아줘` 한 줄로 매번 같은 품질이 나옴. **우리 목표가 이것.**

---

## 전체 플로우

```
[1] 계정 만들기          Anthropic + GitHub
        ↓
[2] 프로그램 설치         Homebrew → git/gh/VS Code → Claude Code
        ↓
[3] 레포 클론 & 실행      git clone → cd TY_AI → claude
        ↓
[4] 양식 정하기          기존에 잘 쓴 보고서를 클로드에게 읽힌다
        ↓
[5] 스킬 만들기          /skill-creator 로 대화하며 SKILL.md 생성
        ↓
[6] 돌려보고 고치기       실제 요청 → 결과 확인 → "이 부분 이렇게 고쳐" 반복
        ↓
[7] 커밋 & 푸시          팀 전원이 같은 스킬을 쓰게 됨
        ↓
      (4~7 반복 — 보고서 종류마다 스킬 하나씩)
```

| 단계 | 문서 |
|---|---|
| [1]~[3] 설치 | **[docs/01-mac-setup.md](docs/01-mac-setup.md)** — 명령어 전부 복붙용 |
| [4]~[7] 스킬 | **[docs/02-skill-guide.md](docs/02-skill-guide.md)** — 스킬 만들고 다듬는 법 |

---

## [1] 필요한 계정

| 계정 | 필수 | 용도 |
|---|---|---|
| **Anthropic (Claude)** | 필수 | 클로드 코드 로그인. **Pro($20) 이상**, 많이 쓸 거면 Max — https://claude.ai |
| **GitHub** | 필수 | 레포 클론 / 스킬·보고서 공유 — https://github.com/signup |

> 결제는 Anthropic 한 곳만. API 키 따로 안 사도 됨 (구독으로 그대로 쓰임).
> 이 레포는 **Private** 이라 초대받은 계정으로 로그인해야 클론됨.

## [2] 필요한 프로그램

| 프로그램 | 필수 | 왜 |
|---|---|---|
| **Homebrew** | 필수 | 맥용 설치 관리자. 나머지 전부 이걸로 깜 |
| **Git + GitHub CLI(`gh`)** | 필수 | 레포 받기 / 푸시. `gh` 쓰면 토큰 안 만들어도 됨 |
| **Claude Code** | 필수 | 본체 |
| **VS Code** | 추천 | 보고서 편집 + 클로드가 고친 내용 diff로 확인 |
| cmux | 선택 | 클로드 여러 개 병렬로 굴릴 때. 나중에 |
| Pandoc / LibreOffice | 선택 | md → Word/PDF 자동 변환할 때 |

→ 설치 명령어: **[docs/01-mac-setup.md](docs/01-mac-setup.md)**

---

## [3] 첫 실행

```bash
cd ~
git clone https://github.com/jihunx-collab/TY_AI.git
cd TY_AI
claude
```

클로드가 뜨면 한국어로 그냥 치면 됨.

```
> 이 레포 구조 설명해줘
> 무슨 스킬 있어?
```

---

## [4]~[6] 스킬 만드는 흐름 (요약)

```bash
cd ~/TY_AI && claude
```

**① 양식 먼저 확보** — 백지에서 만들지 말고, 기존에 잘 쓴 보고서를 읽힌다.

```
> @reports/샘플/A투심보고서.md @reports/샘플/B투심보고서.md
  이 두 개 읽고 공통 목차랑 톤 뽑아줘
```

**② 스킬로 굳히기**

```
> /skill-creator
```

클로드가 질문함 → 답만 하면 `.claude/skills/○○/SKILL.md` 가 생김.

**③ 실제로 돌려보기** — 스킬 이름 말하지 말고 **평소 말투로.**

```
> ○○테크 시리즈A 30억 투자 건 심의보고서 초안 잡아줘
```

**④ 그 자리에서 고치기**

```
> Exit 시나리오가 너무 얕아. Base/Bull/Bear 3개를 표로 강제하게 스킬 고쳐줘
```

**⑤ 만족하면 공유**

```bash
git add .claude/skills && git commit -m "투심 스킬 추가" && git push
```

→ 자세히: **[docs/02-skill-guide.md](docs/02-skill-guide.md)**

---

## 자주 쓰는 명령 (클로드 코드 안에서)

| 입력 | 하는 일 |
|---|---|
| `/help` | 전체 명령 목록 |
| `/skill-creator` | 새 스킬 만들기 (대화형) |
| `/init` | 이 프로젝트 규칙(CLAUDE.md) 자동 생성 |
| `/clear` | 대화 초기화 (보고서 하나 끝났을 때 꼭) |
| `/model` | 모델 변경 (Opus / Sonnet) |
| `@파일명` | 파일 첨부해서 질문 |
| `!명령어` | 셸 명령 바로 실행 (예: `!ls`) |
| `Esc` | 하던 일 중단 |
| `Shift+Tab` | 자동 승인 모드 토글 |

---

## 레포 구조

```
TY_AI/
├── README.md              ← 지금 이 문서
├── docs/                  ← 설치 · 스킬 가이드
├── .claude/skills/        ← 팀 공용 스킬. 여기 넣고 push 하면 전원 공유
└── reports/               ← 산출물. 회사별 폴더로
```

> 이 레포는 **Private**. 그래도 실제 딜 자료(NDA 대상)를 올릴지는 한 번 더 생각할 것.
> `.gitignore` 로 xlsx/pptx/docx/pdf 는 커밋 안 되게 막아뒀지만 `.md` 는 안 막힘.
