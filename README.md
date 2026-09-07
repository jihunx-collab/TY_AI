# TY_AI — 클로드 코드 온보딩 가이드

투자심의보고서 등 **금융 보고서 작성/자동화**를 클로드 코드(Claude Code)로 하기 위한 세팅 가이드.
맥북 기준. 순서대로 따라가면 됨.

---

## 0. 전체 그림 (10분)

```
계정 만들기 → 프로그램 설치 → 클로드 코드 설치 → 레포 클론 → 스킬 사용
   (1장)        (2장)          (3장)           (4장)      (5장)
```

- **클로드 코드**: 터미널에서 돌아가는 AI 에이전트. 파일 읽고/쓰고/명령 실행함.
- **스킬(Skill)**: "이런 요청이 오면 이런 절차로, 이런 양식으로 만들어라"를 적어둔 폴더.
  한 번 만들어두면 `투자심의보고서 써줘` 한마디로 매번 같은 품질이 나옴. ← 우리가 하려는 게 이거.

| 문서 | 내용 |
|---|---|
| [docs/01-mac-setup.md](docs/01-mac-setup.md) | 계정 + 프로그램 + 클로드 코드 설치 (명령어 전부) |
| [docs/02-skill-guide.md](docs/02-skill-guide.md) | 스킬 만드는 법 (`/skill-creator` 포함) |
| [.claude/skills/investment-memo/](.claude/skills/investment-memo/SKILL.md) | 바로 쓸 수 있는 투자심의보고서 스킬 |

---

## 1. 필요한 계정

| 계정 | 필수 | 용도 | 가입 |
|---|---|---|---|
| **Anthropic (Claude)** | 필수 | 클로드 코드 로그인. **Pro($20) 이상 권장, Max($100) 는 넉넉** | https://claude.ai |
| **GitHub** | 필수 | 이 레포 클론 / 보고서 버전관리 / 팀 공유 | https://github.com/signup |
| Google 계정 | 선택 | GitHub·Anthropic 소셜 로그인용 | - |

> 결제는 Anthropic 한 곳만 하면 됨. API 키는 따로 안 사도 됨 (Pro/Max 구독으로 클로드 코드 그대로 쓰임).

## 2. 필요한 프로그램

| 프로그램 | 필수 | 왜 |
|---|---|---|
| **Homebrew** | 필수 | 맥용 설치 관리자. 나머지 전부 이걸로 깜 |
| **Git** | 필수 | 레포 받기 / 변경 이력 |
| **Claude Code** | 필수 | 본체 |
| **VS Code** | 강력추천 | 보고서 md 편집 + 클로드 코드 확장 연동 |
| **GitHub CLI (`gh`)** | 추천 | 터미널에서 GitHub 로그인/푸시 (토큰 안 만들어도 됨) |
| **cmux** | 선택 | 클로드 코드 여러 개 동시에 굴릴 때. 나중에 |
| **LibreOffice** | 선택 | md → PDF/PPTX 변환 자동화 할 때 |

설치 명령어는 → [docs/01-mac-setup.md](docs/01-mac-setup.md)

---

## 3. 설치 다 했으면 (첫 실행)

```bash
git clone https://github.com/jihunx-collab/TY_AI.git
cd TY_AI
claude
```

클로드가 뜨면 그냥 한국어로 치면 됨:

```
> 스킬 목록 보여줘
> 투자심의보고서 스킬로 초안 하나 잡아줘. 대상은 ○○테크, 시리즈A 30억 투자 검토야.
```

`.claude/skills/` 안에 있는 스킬은 **이 폴더에서 클로드 코드를 켜면 자동으로 인식**됨. 별도 설치 없음.

---

## 4. 자주 쓰는 명령 (클로드 코드 안에서)

| 입력 | 하는 일 |
|---|---|
| `/help` | 전체 명령 목록 |
| `/skill-creator` | 새 스킬 만들기 (대화형) |
| `/init` | 이 프로젝트 규칙(CLAUDE.md) 자동 생성 |
| `/clear` | 대화 초기화 (보고서 하나 끝났을 때) |
| `/model` | 모델 변경 (Opus / Sonnet) |
| `Esc` | 하던 일 중단 |
| `Shift+Tab` | 자동 승인 모드 토글 |
| `!명령어` | 셸 명령 바로 실행 (예: `!ls`) |
| `@파일명` | 파일 첨부해서 질문 |

---

## 5. 이 레포 쓰는 방식

```
TY_AI/
├── README.md                 ← 지금 이 문서
├── docs/                     ← 설치·스킬 가이드
├── .claude/skills/           ← 팀 공용 스킬 (여기 추가하면 전원 공유)
│   └── investment-memo/
└── reports/                  ← 실제 산출물 (보고서). 회사별 폴더로
```

스킬을 고치거나 새로 만들면 **커밋해서 푸시** → 팀원 전체가 `git pull` 하면 바로 같은 스킬 사용.

```bash
git add .claude/skills
git commit -m "투자심의보고서 스킬 목차 수정"
git push
```

> ⚠️ `reports/` 에 실제 딜 자료 올릴 거면 **레포가 Private 인지 먼저 확인.**
> Public 이면 절대 올리지 말 것. NDA 자료는 로컬에만.
