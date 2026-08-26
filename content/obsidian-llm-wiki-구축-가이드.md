---
title: Obsidian LLM 위키 구축 가이드
tags: type/tool, status/done
created: 2026-08-26
category: Obsidian, Quartz, GitHub Pages
---

# Obsidian LLM 위키 구축 가이드

Obsidian을 이용해 LLM 관련 지식(리서치·프롬프트·도구·용어집)을 정리하고, Quartz + GitHub Pages로 공개 발행까지 마친 전체 과정을 정리한 문서입니다. 다음에 동일한 셋팅을 할 때 이 문서만 보고 따라 할 수 있도록 구성했습니다.

> [!info] 전체 흐름
> 1. Vault 구조 설계 → 2. 핵심 플러그인 설치 → 3. 콘텐츠 템플릿 제작 → 4. MOC·태그 체계 구축 → 5. 초기 콘텐츠 작성 → 6. 공개 발행(Quartz + GitHub Pages) → 7. 유지·활용 루틴 → 8. 웹 스크랩 자동화(Web Clipper)

---

## 1단계. Vault 구조 설계

콘텐츠 유형(리서치/프롬프트/도구/용어집)을 폴더로 나눌지, 태그로 나눌지 정합니다.

**최종 채택: 단일 폴더 + 태그 분류 방식** — 크로스 카테고리 노트(예: "RAG 프롬프트 튜닝 리서치")에 유연하게 대응하기 위함.

```
LLM-Wiki/
├── Notes/              ← 모든 노트 (리서치/프롬프트/도구/용어집 통합)
├── MOC/                ← 허브 노트 (유형별 자동 목록)
├── Templates/          ← Templater 템플릿 4종
├── Attachments/         ← 이미지·첨부파일
└── _Publish/            ← 공개 발행용 필터링 폴더
```

### 태그 체계
| 태그 | 용도 |
|---|---|
| `#type/research` | 논문·모델 리서치 요약 |
| `#type/prompt` | 프롬프트·사용 팁 |
| `#type/tool` | 도구·API 비교/설정 |
| `#type/glossary` | 용어집 |
| `#status/draft` `#status/done` | 작성 진행 상태 |

### 노트 네이밍 규칙
- 날짜 없이 **주제명만** 사용 (예: `claude-opus-review.md`) — 발행 시 URL을 깔끔한 슬러그로 유지하기 위함

---

## 2단계. 핵심 플러그인 설치

Obsidian 설정 → 커뮤니티 플러그인 → 제한 모드 끄기 → 찾아보기에서 아래 2개 설치·활성화:

- **Dataview** — 태그 기반 동적 목록·대시보드 생성. "Enable JavaScript Queries" 켜두기
- **Templater** — 템플릿 자동 삽입. 설정에서 "Template folder location"을 `Templates`로 지정

---

## 3단계. 콘텐츠 템플릿 4종 제작

`Templates` 폴더 생성 후, 아래 4개 파일을 그 안에 만듭니다.

> [!warning] 파일명 주의
> Obsidian에서 새 노트를 만들 때 이름에 `.md`를 직접 입력하면 `파일명.md.md`처럼 확장자가 중복될 수 있습니다. 파일명은 확장자 없이 이름만 입력하세요 (예: `template-research`).

### `Templates/template-research.md`
```markdown
---
title: <% tp.file.title %>
tags: type/research, status/draft
created: <% tp.date.now("YYYY-MM-DD") %>
source_url: 
authors: 
publish_date: 
---

# <% tp.file.title %>

## 한 줄 요약

## 핵심 내용
- 

## 방법론 / 아키텍처

## 결과 / 시사점

## 관련 노트
- 
```

### `Templates/template-prompt.md`
```markdown
---
title: <% tp.file.title %>
tags: type/prompt, status/draft
created: <% tp.date.now("YYYY-MM-DD") %>
model: 
use_case: 
---

# <% tp.file.title %>

## 상황 / 목적

## 프롬프트
\`\`\`
여기에 프롬프트 작성
\`\`\`

## 결과 / 효과

## 팁 & 주의사항
```

### `Templates/template-tool.md`
```markdown
---
title: <% tp.file.title %>
tags: type/tool, status/draft
created: <% tp.date.now("YYYY-MM-DD") %>
category: 
pricing: 
---

# <% tp.file.title %>

## 개요

## 설정 방법

## 장단점
- 장점: 
- 단점: 

## 대안 도구와 비교
```

### `Templates/template-glossary.md`
```markdown
---
title: <% tp.file.title %>
tags: type/glossary, status/draft
created: <% tp.date.now("YYYY-MM-DD") %>
---

# <% tp.file.title %>

## 정의

## 예시

## 관련 용어
- 
```

### 사용법
1. `Notes` 폴더에서 **새 빈 노트**를 먼저 생성
2. 노트 **본문을 클릭**해서 커서를 안에 위치시킴 (제목이나 파일 탐색기 클릭 상태면 안 됨)
3. `Ctrl/Cmd + P` → "Templater: Insert Template" → 원하는 템플릿 선택

> [!warning] "No active editor, can't append templates" 에러
> 에디터 본문에 커서가 없거나(다른 패널 클릭 상태), 읽기 모드(Reading view)에서 실행하면 이 에러가 납니다.
> - 대상 노트가 열려 있는지 확인
> - 본문을 직접 클릭해 커서를 위치시킴
> - `Ctrl/Cmd + E`로 편집 모드인지 확인 후 재시도
>
> **핵심 개념**: Templater는 "노트를 생성"하는 도구가 아니라, **이미 만들어진 빈 노트에 템플릿 내용을 삽입**하는 도구입니다. 노트 생성은 사용자가 직접 해야 합니다.

---

## 4단계. MOC·태그 체계 구축

`MOC` 폴더를 만들고 Dataview 쿼리로 유형별 노트를 자동 나열하는 허브 노트들을 만듭니다.

### `MOC/MOC-Research.md`
````markdown
# 📚 Research MOC

## 전체 목록
```dataview
TABLE authors as "저자", publish_date as "발행일", status as "상태"
FROM #type/research
SORT file.ctime DESC
```

## 작성 중인 노트
```dataview
LIST
FROM #type/research AND #status/draft
```
````

### `MOC/MOC-Prompts.md`
````markdown
# 💬 Prompts MOC

```dataview
TABLE model as "모델", use_case as "용도"
FROM #type/prompt
SORT file.ctime DESC
```
````

### `MOC/MOC-Tools.md`
````markdown
# 🛠️ Tools MOC

```dataview
TABLE category as "카테고리", pricing as "가격"
FROM #type/tool
SORT file.name ASC
```
````

### `MOC/MOC-Glossary.md`
````markdown
# 📖 Glossary MOC

```dataview
LIST
FROM #type/glossary
SORT file.name ASC
```
````

### `MOC/MOC-Home.md`
```markdown
# 🏠 LLM Wiki Home

- [[MOC-Research]]
- [[MOC-Prompts]]
- [[MOC-Tools]]
- [[MOC-Glossary]]

## 최근 수정된 노트
```dataview
TABLE file.mtime as "수정일"
FROM "Notes"
SORT file.mtime DESC
LIMIT 10
```
```

Dataview 쿼리는 **읽기 모드**에서만 렌더링됩니다 (`Ctrl/Cmd + E`로 전환). 노트가 없을 때는 빈 테이블/목록이 보이는 것이 정상입니다.

---

## 5단계. 초기 콘텐츠 작성

`Notes` 폴더에서 템플릿을 삽입해 실제 노트 5~10개를 채우며 구조를 검증하는 단계입니다. 완성도보다 구조가 실제로 도는지 확인하는 것이 목적입니다. 작성 완료된 노트는 `status/draft` → `status/done`으로 태그를 변경합니다.

---

## 6단계. 공개 발행 (Quartz + GitHub Pages)

### 사전 결정 사항
- **발행 방식**: Quartz (무료, GitHub Pages 배포, 코드 커스터마이징 자유도 높음) — Obsidian Publish(유료)보다 개발자에게 적합
- **repo 공개 범위**: **Public 필수**

> [!warning] GitHub Free 플랜은 Private repo에서 GitHub Pages 미지원
> Private repo를 유지하며 배포하려면 GitHub Pro(유료) 또는 Cloudflare Pages/Vercel/Netlify 같은 외부 배포 서비스를 사용해야 합니다. 소스코드 공개가 괜찮다면 Public repo + GitHub Pages가 가장 간단합니다.

### 6-1. Quartz 프로젝트 생성
Obsidian Vault와는 별도 프로젝트 폴더로 관리합니다.

```bash
git clone https://github.com/jackyzha0/quartz.git llm-wiki-site
cd llm-wiki-site
npm i
npx quartz create
```

`npx quartz create` 마법사에서 순서대로 선택:
1. 템플릿 → **`obsidian`** (위키링크·백링크 등 Obsidian 문법 호환)
2. content 폴더 채우는 방식 → `new` / `copy` / **`symlink`** 중 선택

> [!warning] Windows에서는 symlink 대신 파일 복사(robocopy) 권장
> Windows symlink는 로컬에서는 정상 작동하지만, **git commit 시 실제 파일이 아니라 "링크 경로 정보"만 저장**됩니다. GitHub Actions(리눅스 환경)에서 clone하면 로컬 전용 경로(`C:\Users\...`)를 찾지 못해 `content` 폴더가 빈 상태로 빌드됩니다. 결과적으로 사이트에 홈페이지 대신 빈 RSS 피드(`index.xml`)만 노출되는 문제로 이어졌습니다.
>
> **해결책**: symlink 대신 `robocopy`로 실제 파일을 복사합니다.
> ```powershell
> Remove-Item content -Force
> mkdir content
> robocopy "<_Publish의 절대경로>" content /MIR
> ```
> 노트를 업데이트할 때마다 push 전에 이 명령을 다시 실행해야 합니다.

3. Base URL → `<GitHub계정명>.github.io/<repo이름>` 형식 (예: `JirehNam.github.io/llm-wiki`)

### 6-2. 발행 대상 폴더 분리
Vault 전체가 아니라 공개하고 싶은 노트만 선별합니다. `_Publish` 폴더에 발행할 노트만 복사해서 관리 (`MOC`, `Templates`, `status/draft` 노트는 보통 제외).

`_Publish` 폴더 루트에는 홈페이지 역할을 할 `index.md`가 반드시 있어야 합니다.

```markdown
---
title: David's LLM Wiki
---

# 👋 Welcome
이곳은 LLM 관련 리서치, 프롬프트, 도구, 용어집을 정리한 개인 위키입니다.
```

> [!warning] index.md 파일명 확인
> Obsidian에서 파일명에 `.md`를 직접 타이핑하면 `index.md.md`로 중복 저장되어 Quartz가 홈페이지로 인식하지 못합니다. 파일명은 `index`로만 입력하세요.

### 6-3. 로컬 미리보기
```bash
npx quartz build --serve
```
`http://localhost:8080`에서 확인합니다.

> [!warning] "Cannot find module '@quartz-themes/default'" 에러
> 테마 패키지가 제대로 설치되지 않은 경우 발생합니다. 해결 순서:
> 1. `npm i @quartz-themes/default` 직접 설치
> 2. 안 되면 완전 재설치: `Remove-Item -Recurse -Force node_modules`, `Remove-Item package-lock.json`, `npm i`

### 6-4. GitHub 연동 및 push

```bash
git remote set-url origin https://github.com/<계정명>/<repo이름>.git
git add .
git commit -m "Initial LLM wiki setup"
git push -u origin v5
```

> [!warning] "Password authentication is not supported" 에러
> GitHub는 비밀번호 로그인을 지원하지 않습니다. **Personal Access Token(PAT)**을 발급해서 password 자리에 입력해야 합니다.
> 1. GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
> 2. Generate new token (classic) → 메모 입력, 만료 기간 설정, **scope는 `repo`만 체크**
> 3. `ghp_`로 시작하는 토큰을 **한 번만 표시되므로 반드시 복사**
> 4. push 시 username에는 계정명, password 자리에 토큰 붙여넣기

### 6-5. GitHub Pages 배포 소스 설정
1. repo → **Settings**(계정 전체 설정이 아닌 **repo 안의** Settings) → **Pages**
2. **Build and deployment → Source**를 **GitHub Actions**로 변경
3. "Add a domain"은 커스텀 도메인 연결용 선택 기능이며 필수 아님, 비워두면 기본 `<계정명>.github.io/<repo이름>` 주소 사용

> [!warning] Quartz 저장소를 그대로 clone하면 내부용 워크플로우까지 딸려옴
> `git clone`으로 Quartz 원본 저장소를 그대로 가져오면, Quartz 팀이 자체적으로 쓰는 CI 워크플로우(`deploy-v5.yaml`, `deploy-preview.yaml`, `docker-build-push.yaml` 등)까지 함께 push됩니다. 이들은 GitHub Pages 배포용이 아니므로 (권한(`permissions`)에 `pages: write`, `id-token: write`가 없음) 실행돼도 David의 사이트는 배포되지 않습니다.
>
> **해결책**: `.github/workflows/` 안에 직접 배포 워크플로우 파일(예: `gh-pages-deploy.yml`)을 새로 추가합니다.
> ```yaml
> name: Deploy Quartz site to GitHub Pages
>
> on:
>   push:
>     branches:
>       - v5
>   workflow_dispatch:
>
> permissions:
>   contents: read
>   pages: write
>   id-token: write
>
> concurrency:
>   group: "pages"
>   cancel-in-progress: false
>
> jobs:
>   build:
>     runs-on: ubuntu-latest
>     steps:
>       - uses: actions/checkout@v4
>         with:
>           fetch-depth: 0
>       - uses: actions/setup-node@v4
>         with:
>           node-version: 22
>       - name: Install Dependencies
>         run: npm ci
>       - name: Install Quartz plugins
>         run: npx quartz plugin install
>       - name: Build Quartz
>         run: npx quartz build
>       - name: Upload artifact
>         uses: actions/upload-pages-artifact@v3
>         with:
>           path: public
>
>   deploy:
>     needs: build
>     environment:
>       name: github-pages
>       url: ${{ steps.deployment.outputs.page_url }}
>     runs-on: ubuntu-latest
>     steps:
>       - name: Deploy to GitHub Pages
>         id: deployment
>         uses: actions/deploy-pages@v4
> ```
> 커밋 후 push하면 Actions 탭에 실제 배포 워크플로우가 새로 나타나 실행됩니다. Docker build, Deploy Preview 등 나머지 워크플로우는 실패해도 무시해도 됩니다.

### 6-6. 배포 확인
Actions 탭에서 새로 추가한 워크플로우가 초록 체크(성공)로 완료되면, `https://<계정명>.github.io/<repo이름>/`로 접속해 확인합니다. 강력 새로고침(`Ctrl+Shift+R`)을 권장합니다.

### 이후 발행 흐름 (업데이트 시마다 반복)
```powershell
robocopy "<_Publish의 절대경로>" content /MIR
git add content
git commit -m "Update published notes"
git push
```
push할 때마다 GitHub Actions가 자동으로 빌드·배포합니다.

---

## 7단계. 유지·활용 루틴

`MOC-Home.md`에 작업 대시보드 쿼리를 추가합니다.

````markdown
## ✍️ 작성 중인 노트 (Draft)
```dataview
TABLE file.mtime as "마지막 수정"
FROM "Notes"
WHERE contains(tags, "status/draft")
SORT file.mtime ASC
```

## 📅 이번 주 업데이트된 노트
```dataview
LIST
FROM "Notes"
WHERE file.mtime >= date(today) - dur(7 days)
SORT file.mtime DESC
```
````

### 루틴
| 주기 | 할 일 |
|---|---|
| 매일 (5분) | 새로 배운 내용 즉시 캡처 (완성도 무시, draft로) |
| 주간 (15~20분) | draft 목록 확인 → 1~2개 done으로 완성 |
| 월간 | 카테고리 불균형 점검, 오래된 draft 정리 |
| 발행 전 | done 상태 노트만 `_Publish`로 선별 |

---

## 8단계. 웹 스크랩 자동화 (Web Clipper)

**Obsidian 공식 Web Clipper** 브라우저 확장 프로그램을 사용하면 웹페이지를 클릭 한 번으로 Vault 노트로 저장할 수 있습니다.

### 설정 순서
1. Chrome/Firefox 확장 스토어에서 **"Obsidian Web Clipper"** 설치 (개발자: Obsidian)
2. 확장 아이콘 → 설정 → **Vault**를 LLM-Wiki Vault로 지정, 기본 저장 폴더를 `Notes`로 설정
3. 설정 → **Templates** → 새 템플릿 추가 (예: `LLM-Research`)

> [!warning] frontmatter와 본문을 구분해서 입력해야 함
> Web Clipper 템플릿 화면은 **"템플릿 속성(Properties)"**과 **"노트 내용(Note content)"**이 별도 섹션입니다. `title`, `tags`, `source_url` 같은 frontmatter 항목을 "노트 내용" 칸에 그대로 넣으면 실제 YAML frontmatter로 인식되지 않고 본문에 텍스트로만 찍혀서, Dataview가 태그를 인식하지 못합니다.
>
> - **템플릿 속성**에 "+ 속성 추가하기"로 추가: `title` → `{{title}}`, `tags` → `type/research, status/draft`, `created` → `{{date}}`, `source_url` → `{{url}}`, `authors` → `{{author}}`, `publish_date` → `{{published}}`
> - **노트 내용**에는 본문 구조만 남기기 (`## 핵심 내용` 등)
> - 저장 위치(**노트** 필드)가 기본값 `Clippings`로 되어있을 수 있으니 `Notes`로 변경 확인

4. 아무 웹페이지에서 확장 아이콘 → 템플릿 선택 → Clip
5. 생성된 노트의 frontmatter에 태그가 제대로 들어갔는지, `MOC-Research.md`(읽기 모드)에 자동으로 나타나는지 확인

---

## 전체 체크리스트

- [ ] Vault 폴더 구조(Notes/MOC/Templates/Attachments/_Publish) 생성
- [ ] Dataview, Templater 플러그인 설치
- [ ] 템플릿 4종(`template-research/prompt/tool/glossary`) 제작
- [ ] MOC 5종(`MOC-Research/Prompts/Tools/Glossary/Home`) 및 Dataview 쿼리 작성
- [ ] 초기 노트 5~10개 작성
- [ ] Quartz 프로젝트 생성 및 로컬 미리보기 확인
- [ ] GitHub repo(Public) 생성 및 PAT로 push
- [ ] GitHub Pages 배포 워크플로우 직접 추가 및 Source를 GitHub Actions로 설정
- [ ] 배포된 사이트 정상 접속 확인
- [ ] MOC-Home에 유지 루틴 대시보드 추가
- [ ] Web Clipper 설치 및 템플릿(Properties/Content 분리) 설정
