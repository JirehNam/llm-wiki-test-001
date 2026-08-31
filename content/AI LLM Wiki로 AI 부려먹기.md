---
title: "🤖 [AI] LLM Wiki로 AI 부려먹기"
tags:
  - "type/research"
  - "status/draft"
created: 2026-08-31
source_url: "https://velog.io/@silverclean091/AI-LLM-Wiki%EB%A1%9C-AI-%EB%B6%80%EB%A0%A4%EB%A8%B9%EA%B8%B0"
authors:
publish_date:
---
# [AI] LLM Wiki로 AI 부려먹기

## 한 줄 요약


## 핵심 내용
> ⚠️ **주의!! 이번 글도 정말 깁니다...**  
> **필요한 곳만 골라 읽으셔도 무방하나, 이왕 열심히 썼으니 다 읽어주시면 제가 기분이 좋습니다.**

## 🤔 LLM Wiki란 무엇인가?

![](https://velog.velcdn.com/images/silverclean091/post/1ab489b2-e185-407c-bccb-5c61766e9c44/image.png)

**LLM Wiki(위키).** 이는 안드레 카파시(Andrej Karpathy)가 2026년 4월에 제안한 따끈따끈한 **지식 관리 패턴** 으로, **사용자의 파편화된 원본 문서를 AI가 직접 읽고 분석** 하여 사용자와 상호작용하며 정보를 전달하는 **'살아있는 지식 베이스'** 를 의미한다.

AI를 똑똑한 질문 답변기로만 쓰지 말고 **시간이 지날수록 더 똑똑해지는 지식 시스템으로 사용하자** 는 이 방안! 등장한지 얼마 되지 않았음에도 불구하고 벌써부터 많은 개발자들이 프로젝트 등을 관리하는데 사용하고 있다고 한다.

이러한 LLM Wiki는 어떤 구조로 작동하고, 어떻게 사용할 수 있는걸까? 본 포스팅에서는 **LLM Wiki의 원리 및 구조와 간단한 구축 방법** 을 소개한다.

## 🌟 LLM Wiki의 등장

기존에는 회의록이나 메모, 기사, 논문, 자료 등을 Notion이나 Obsidian 등의 **별도의 노트 애플리케이션에 저장** 하고, **AI에게 이러한 내용을 복사하여 질문** 하거나 혹은 애플리케이션에 내장되어있는 기능을 사용하여 질문을 했다.

그러나! 사용해본 대부분의 사람들이 아마 느꼈을듯이... 이러한 기존의 노트와 AI 조합에는 몇 가지 문제가 존재했다.  

![](https://velog.velcdn.com/images/silverclean091/post/b93607e3-2475-434b-9c27-476932807232/image.png)

첫 번째는 **툴을 통합할 수 없고 자료를 왔다갔다 옮겨야 하기에 작업 과정이 상당히 귀찮고 번거롭다** 는 점이었고, 두 번째로 가장 큰 문제는 **"AI에게 기억이 쌓이지 않는다"** 는 점이었다.

물론 GPT나 Gemini, Claude 모두 **'프로젝트'** 라는 기능을 이용하여 데이터를 첨부해두고 사용할 수는 있다. 다만 이 경우에도 마찬가지로 새로운 노트를 작성하면 AI 툴에도 똑같이 프로젝트 내에 파일을 첨부해야한다는 번거로움이 존재했고, 암만 프로젝트 기능을 사용한다고 한들 계속해서 대화를 하다보면 **이전에 주고받은 맥락들이 휘발된다** 는게 가장 곤란한 문제였다.

또한 **Notion이나 Obsidian을 통한 노트 관리** 의 경우, 물론 안 그런 사람들도 있지만... 많은 경우 **작심삼일** 로 끝나거나, 혹은 갈수록 작성 퀄리티가 떨어지거나 사용 빈도가 낮아지는 등 **중간에 탈주하게 되는 경우** 가 빈번하게 존재했다.

물론 여기에도 많은 원인이 있겠지만, 아마 매번 데이터를 수기로 정리하고 작업하고, 연결하고...하는 과정이 귀찮고 **많은 에너지가 소모** 되었기 때문이 아닐까?  

**우리의 카파시 형님** 은 이러한 점에서 불편함을 캐치하고, 이를 해결하기 위한 방안을 하나 제안하였다.

바로, **노트 애플리케이션과 LLM을 연동하여 자료 정리를 자동화하고, AI에게도 쉽고 빠르게 질문하며 계속해서 지식의 선순환 구조를 구축하자** 는 것!

그렇다, 이것이 바로 **LLM Wiki** 이다.

<iframe frameborder="0" src="https://f7e29d32c702043c2852cd2c02aafacb.safeframe.googlesyndication.com/safeframe/1-0-45/html/container.html" title="서드 파티 광고 콘텐츠" width="728" height="90" sandbox="allow-forms allow-popups allow-popups-to-escape-sandbox allow-same-origin allow-scripts allow-top-navigation-by-user-activation" allow="private-state-token-redemption" aria-label="광고"></iframe>

## 🧬 LLM Wiki의 구조

LLM Wiki는 크게 **`원본`, `위키`, `규칙`** 세 개의 구조로 정의할 수 있다.

*(여기에서의 세 구조는 wikidocs를 참고하여 작성되였다. 보다 자세한 원본 문서를 원한다면 [이쪽](https://wikidocs.net/353382) 으로!)*

### 1️⃣ 첫 번째 구조: 원본

![](https://velog.velcdn.com/images/silverclean091/post/74a4ad7b-d591-4672-8bdf-a9fc1a603775/image.png)

첫 번째 구조인 `원본` 은 `raw` 폴더에 보관되며, 말 그대로 회의록 원문, 웹 문서 저장본, PDF 추출 텍스트, 조사한 자료 등의 **원본 데이터** 를 보관하는 공간이다.

원본 폴더를 별도로 관리하여야 **LLM이 정보를 찾기에도 용이** 하며, 추후 사람이 찾아볼 때도 이것이 **요약본인지 혹은 원본인지에 대하여 명확하게 구분** 할 수 있다. 또한 LLM이 참조한 원본 문서를 **출처로 인용** 하기 위해서는 이러한 원본 파일을 저장하는 공간이 별도로 존재해야 한다.

**따라서 이러한 `raw` 폴더에는 해석이나 요약본을 함께 저장하여선 안 된다.** 요약이나 판단은 두 번째 구조인 ' `위키` ' 항목에 저장하여야 함!

### 2️⃣ 두 번째 구조: 위키

두 번째 구조인 `위키` 는 `wiki` 폴더에 보관되며, 말 그대로 **LLM이 읽고 요약하고 정리해준 결과물** 을 보관하는 공간이다. 사용자는 당연히 `raw` 폴더보다는 **`wiki` 폴더에 더욱 자주 접근** 하게 된다.

![](https://velog.velcdn.com/images/silverclean091/post/490c5e21-82d7-44ed-a71d-0a18a3d80c4b/image.png)

`wiki` 폴더에서는 `raw` 폴더의 원본 문서를 기반으로, 반복되는 개념을 묶고 관련 문서끼리 연결하여 읽기 쉬운 형태로 정리한다. 따라서 **원본보다 짧고 구조적인 형태!** 보통 `wiki` 폴더의 내부는 프로젝트 주제나 큰 단위 별로 폴더가 한 번 더 나뉘게 되며, 저장되는 파일의 형태는 `마크다운(md)` 이다.

여기에서 주의할 점은, LLM이 정리한 형태이므로 어쩔 수 없이 **Hallucination(환각)** 현상이 일어날 수도 있다는 것. 따라서 좋은 `wiki` 의 경우, 핵심 주장 옆에 **출처나 참고한 원본의 위치** 등을 함께 기재하여 남기니 참고하면 좋다.

### 3️⃣ 세 번째 구조: 규칙

세 번째 구조인 `규칙` 은 **`CLAUDE.md` 또는 `AGENTS.md`** 라는 하나의 파일로 저장된다.

![](https://velog.velcdn.com/images/silverclean091/post/26e34de4-5e41-411f-b6c8-233bcd09fddc/image.png)

이 파일은 말 그대로 **Claude 등의 LLM이 어떤 규칙으로 작동하고, 어떤 규칙으로 파일에 접근해야 하는지 등에 대해 명시** 되어 있는 파일이다. **사람의 입장에서는 운영 규칙** 이, **LLM에게는 작업 지시서** 가 되는 매우 중요한 파일!

참고로! 해당 파일은 **사용하는 LLM 도구마다 파일명을 다르게 명시** 해야 한다. 예를 들어 OpenAI의 Codex는 `AGENTS.md` 라는 이름으로, Claude Code의 경우에는 `CLAUDE.md` 라는 이름으로 규칙을 정의한다.

규칙 파일에는 **폴더의 의미, 원본 보존 원칙, 출처 표기 방식, 확인 필요 표시 방법, 금지 사항 등** 을 기재해둔다. 규칙 파일이 없으면 LLM은 매번 대화에서 즉석으로 판단하여 작업을 수행하므로, 결과물의 일관성이 현저히 떨어질 뿐더러 Hallucination의 확률도 증가한다.

따라서 **LLM Wiki의 성능은 이러한 규칙 파일을 얼마나 명확하고 자세하게 작성하느냐에 달려있다** 고 봐도 무방하다. 어떻게 보면 셋 중 가장 중요한 구조!

## 📚 LLM Wiki의 작업

이러한 세 가지 구조를 기반으로 LLM Wiki는 몇 가지 작업을 수행하는데, 여기에서는 각각 **`Ingest` 와 `Query`, `Lint`** 로 정의한다.  

![](https://velog.velcdn.com/images/silverclean091/post/4ad404fe-911b-4e39-b170-fce43ad774f0/image.png)

먼저 **`Ingest` 는 새로 들어온 자료를 원본 자료에 넣고, LLM을 통해 기존 위키에 통합하는 작업** 을 의미한다.

핵심 내용에 대한 논의, 요약 페이지 작성 등... 추가된 원본 문서를 기반으로 **요약화되거나 혹은 더 구조화된 문서를 생성** 하는 작업이며, 자료 하나가 새로 추가되었을 경우 하나의 요약 파일만 생성될 수도, 혹은 이 자료와 연관된 나머지 기존 페이지들까지 함께 수정될 수도 있다.

![](https://velog.velcdn.com/images/silverclean091/post/d8a976f4-6086-4314-821f-49a181969ec7/image.png)

두 번째로 **`Query` 는 사용자와 LLM이 질의응답을 주고받는 과정** 을 의미한다.

사용자가 질문을 하면 LLM은 그에 맞는 wiki 페이지를 탐색하여 알맞은 답변을 제공한다. 답변의 형식은 **표, 슬라이드, 차트 등 다양한 형태** 를 가질 수 있으며, 여기에서 중요한 점은 이러한 **답변 또한 추가로 wiki에 적재** 하여 지식 관리 패턴으로 사용할 수 있다는 것!

![](https://velog.velcdn.com/images/silverclean091/post/12a123cf-f9b6-4104-9a53-e9bc9126f3df/image.png)

마지막으로 **`Lint` 는, LLM Wiki가 수행하는 '자가 건강검진'** 에 해당한다. 주기적으로 wiki 내에서 **상충되는 이야기** 를 하고 있지는 않은지, 새로 들어온 자료 때문에 **옛 페이지와 어긋나는 부분** 이 있는지, **관계가 누락** 되어 있진 않은지 등에 대해 점검하고 이를 수정한다.

이러한 자가 점검 기능 덕분에, wiki가 점점 확장되더라도 자료가 엉망으로 꼬이지 않고 일관되게 유지할 수 있는 것! **여타 LLM과 확실하게 차별화되는 부분** 이라 할 수 있다.

## 🧱 LLM Wiki 구축하기

LLM Wiki의 개념과 구조를 알아봤으니, 이제는 본격적으로 LLM Wiki를 가볍게 한 번 **구축** 해볼 차례다!

본 섹션은 **환경 구축 및 폴더 구축, LLM 연동, 지침 파일 생성, 원본 데이터 적재 및 활용** 단계로 진행된다. 상세한 내용 및 과정들은 다른 블로그나 자료와 쪼~끔 다를 수 있으나, 대략적인 과정만 참고한다면 아마 **간단한 LLM Wiki** 정도는 구축할 수 있을 것이다!

### 💜 1단계: Obsidian 다운로드 및 환경 구축하기

먼저 환경 구축을 위해 필요한 **메모용 프로그램** 을 다운로드해야 한다. 여기에서는 `마크다운(md)` 파일을 활용한 구조화된 문서 작성 및 문서간의 관계 그래프 사용을 위하여 **`Obsidian`** 이라는 프로그램을 사용하였다.

![](https://velog.velcdn.com/images/silverclean091/post/c047dc53-302b-45bc-a3a2-cf51957b6f13/image.png)

`Obsidian` 은 **`마크다운(md)` 문법으로 작성할 수 있는 크로스 플랫폼 노트 애플리케이션** 이다. 단순한 메모보다는 구조화된 기록을 남기는 데 특화되어 있으며, 특히 **그래프 뷰(Graph View)** 라는 기능을 통해 문서관의 연계성을 시각적으로 표현하고 지식을 구조화할 수 있어 많은 사람들이 사용하고 있다.

mac과 Windows 모두 다음 사이트에 접속하여 **다운로드** 받을 수 있다:  
**[https://obsidian.md/download](https://obsidian.md/download)**

![](https://velog.velcdn.com/images/silverclean091/post/39ee82e7-2bc6-4534-b585-6d8866c9413a/image.png)

`Obsidian` 을 다운로드받은 후에는, **파일을 저장하고 읽어들이기 위한 `보관함`** 의 위치를 생성 및 지정해야한다. 기본 위치는 `Users/사용자명/Documents` 의 하단에 **보관함의 이름** 으로 폴더가 생성되며, 그 외에도 본인이 지정하고 싶은 폴더의 위치가 있다면 자유롭게 설정할 수 있다.

또한 **유료 구독기능** 을 사용할 경우, 이미지 최하단에 있는 `Obsidian Sync` 라는 원격 보관함을 사용할 수도 있지만...

![](https://velog.velcdn.com/images/silverclean091/post/999c0071-8282-4c68-8424-5b333d5507c0/image.png)

저는 돈이 없으므로 **로컬 보관함**...을 사용하겠습니다.

보관함의 위치와 이름은 자유롭게 지정할 것!

### 🩵 2단계: 폴더 구조 구축하기

보관함을 생성했다면, 다음으로는 LLM Wiki의 구조에 맞춰 폴더 구조를 구축할 차례다. 앞서 말했듯 폴더는 크게 **`raw` 와 `wiki`** 로 나뉘어진다.

따라서 마찬가지로 폴더 또한 최상단 폴더 아래 바로 `raw` 폴더와 `wiki` 폴더를 생성하면 되며, **필요에 따라 하위 폴더를 카테고리화** 하여 생성하면 된다!

![](https://velog.velcdn.com/images/silverclean091/post/2561e8ff-d9be-4a57-aac7-6778643a1530/image.png)

이 포스팅에서는 가장 쉬운 접근성을 고려하여, **프로젝트의 회의록과 일정을 관리하는 LLM Wiki** 를 구축해볼 예정이다.

따라서 위 이미지와 같이 먼저 `raw/meetings` 와 `raw/plannings` 폴더를 생성했다. 그리고 `raw` 폴더에서부터 추출한 프로젝트 결정 사안 정리를 위한 `wiki/decisions`, 프로젝트 내에서 사용되는 단어들의 정의 정리를 위한 `wiki/definitions` 폴더를 추가로 생성하였다.

이처럼 **경우에 따라 필요한 구조대로 폴더를 생성** 하면 됨! `raw` 는 원본 파일들의 카테고리를, `wiki` 는 정리 및 요약될 파일들의 카테고리를 정의한다고 생각하면 편하다.

여기까지 하면 1차 폴더 구조 구축이 완료된다.

### 💛 3단계: Claude.md 지침파일 생성하기

폴더 구축을 완료하였으니, 이제는 본격적으로 'LLM' Wiki를 활용하기 위하여 **LLM 지침 가이드** 를 작성할 예정이다. 본 포스팅에서는 **`Claude Code`** 를 연동하는 기준으로 작성하였다.

지침 가이드 작성을 위해, 먼저 최상단 루트 폴더에 **`Claude.md`** 파일을 하나 생성한다. (Obsidian의 경우 기본 저장자가.md이므로 파일명을 그냥 `Claude` 로 해두어도 무방하다)

![](https://velog.velcdn.com/images/silverclean091/post/a7760d21-aac8-4558-bf7a-695160bdef89/image.png)

파일을 생성하였으면, 여기에 Claude Code의 작동을 위한 지침을 작성한다.

들어가야 하는 필수 항목으로는 보통 **`폴더 구조`, `규칙`, `워크플로우`, `지식 적재 명령어`, `스마트 라벨링 명령어`, `자가 검진 명령어`** 등이 존재한다.

대략적인 내용을 템플릿화하면 다음과 같다.

각 상세 내용은 위에서 설명했던 폴더 구조 및 LLM Wiki의 작업 방식과 동일하며, 아래의 내용을 기반으로 **본인의 의도나 원하는 작업 내용에 따라 편하게 수정** 하면 됨! 아예 **새로운 스킬이나 작업 명령을 추가** 하는 것도 가능하니, 정말 자유롭게 작성하면 된다.

참고로 이게 Velog에서 그냥 보기엔 조금 드러워보여도 md파일로 저장하면 깔끔하게 **구조화** 되어 예쁘게 잘 바뀐다...

> 💬 **CLAUDE.md 파일 작성 가이드**  
> 
> ```
> ## 📁 폴더 구조
> 
> \`\`\`
> /
> ├── raw/
> │   ├── meetings/      # 회의록 원본 (수정 금지)
> │   └── plannings/     # 기획/일정 원본 (수정 금지)
> └── wiki/
>     ├── decisions/     # raw에서 추출한 프로젝트 결정 사안
>     └── definitions/   # 프로젝트 용어 정의
> 
> \`\`\`
> 
> * \`raw\`: 원본 파일 보관용. 절대 가공하지 않는다.
> * \`wiki\`: \`raw\`를 기반으로 정리·요약된 결과물. 항상 출처(원본 파일명, 날짜)를 함께 남긴다.
> * 새로운 성격의 자료가 생기면 \`raw/{카테고리}\`, 필요 시 \`wiki/{카테고리}\`를 추가로 만든다.
> 
> ## 🔄 핵심 동작 원리
> LLM Wiki는 세 가지 동작으로 지식을 관리한다.
> 
> * Ingest: 새로 들어온 원본 자료를 읽고 기존 위키에 통합하는 작업. 새 요약 문서 하나만 생기는 경우도 있고, 연관된 기존 \`wiki\` 문서까지 함께 갱신되는 경우도 있다.
> * Query: 사용자와 LLM이 주고받는 질의응답. 표·슬라이드·차트 등 다양한 형태로 답할 수 있으며, 재사용 가치가 있는 답변은 다시 \`wiki\`에 적재한다.
> * Lint: 주기적인 자가 건강검진. 상충되는 내용, 옛 페이지와의 불일치, 누락된 관계를 점검하고 수정한다.
> 
> ## 📏 기본 규칙
> 
> 1. \`raw\` 폴더의 파일은 읽기 전용으로 취급하고 절대 수정·삭제하지 않는다.
> 2. \`wiki\` 문서를 새로 쓰거나 수정할 때는 반드시 근거가 된 \`raw\` 파일 경로와 날짜를 각주나 하단에 명시한다.
> 3. 기존 \`wiki\` 문서와 상충하는 정보를 발견하면 임의로 덮어쓰지 말고 먼저 사용자에게 확인한다.
> 4. 하나의 결정/정의는 하나의 항목으로 관리하고, 변경 이력은 삭제하지 않고 하단에 누적한다.
> 
> ## 🔁 워크플로우
> 
> 1. \`raw/meetings\` 또는 \`raw/plannings\`에 새 파일이 추가되면 전체 내용을 읽는다.
> 2. 결정 사안이 있으면 \`wiki/decisions\`에 새 항목을 추가하거나 기존 항목을 갱신한다.
> 3. 새로운 용어·약어가 등장하면 \`wiki/definitions\`에 정의를 추가한다.
> 4. 정리가 끝나면 원본 파일명을 참조 목록에 기록해, 어떤 raw 파일까지 반영됐는지 추적 가능하게 한다.
> 5. 사용자 질문에 답변할 때는 관련 \`wiki\` 문서를 우선 탐색해 근거로 삼는다. 답변 내용이 이후에도 재사용할 가치가 있다면, 별도 문서로 정리해 \`wiki\`에 적재한다.
> 
> ## 🧠 1. 지식 소화 명령어 — \`/ingest\`
> 
> * 타겟: \`raw/\` 폴더 내의 문서
> * 작업: 단순 요약 금지. 문서를 꼼꼼히 읽고 핵심 인물, 프로젝트, 기술 개념(Entity)을 추출한다. 기존 \`wiki\` 지식과 연결 고리가 있으면 명시한다.
> * 신뢰도 부여 및 승격: 정보의 출처와 교차 검증 여부를 판단해 신뢰도 점수(Confidence score)를 부여하고, 쓸모 있는 지식만 \`wiki/\` 폴더로 승격시킨다.
> * 완료 처리(중복 방지): 원본 문서 상단 Front matter에 \`ingested: - [x]\` 체크박스를 추가해, 이미 처리한 문서가 반복 요약되어 쓰레기가 쌓이는 것을 막는다.
> 
> ## 🏷️ 2. 스마트 라벨링 및 관계 맺기 명령어 — \`/tag\`
> 
> * 타겟: 파일 위치 및 본문 내용은 수정하지 않는다.
> * 자동 분류: 문서의 맥락을 파악해 어떤 주제에 관한 것인지 스스로 판단하고, 적절한 분류 태그(Tag)를 메타데이터에 자동으로 추가한다.
> * 입체적 관계망 형성: 단순 꼬리표를 넘어 "A가 B에 의존한다", "A 프로젝트 담당자는 B이다"와 같은 지식 간의 관계(Relationship)를 메타데이터 속성에 명시해, 훗날 필요한 정보 뭉치를 즉시 꺼내올 수 있게 한다.
> 
> ## 🩺 3. 지식 창고 자가 치유 명령어 — \`/lint\`
> 
> * 타겟: 볼트 전체. 단, \`raw/\` 폴더의 원본 데이터는 절대 수정하지 않는다.
> * 검진: 고아(Orphan) 페이지, 누락된 태그, 깨진 링크, 누락된 관계(Relationship)를 식별해 리포트한다.
> * 자가 치유(Self-healing): 깨진 링크는 스스로 올바른 경로로 자동 복구한다.
> * 충돌 해결: 서로 다른 문서에서 상충되는 정보(Contradiction)가 발견되면, 더 최신이거나 신뢰도 높은 정보로 병합/덮어쓸지 사용자에게 제안한다.
> ```

### 🧡 4단계: Claude Code 연동하기

지침 작성까지 완료하였으니, 이제는 본격적으로 'LLM' Wiki를 활용하기 위하여 **LLM을 연동** 할 예정이다. 앞서 설명했듯 본 포스팅에서는 **`Claude Code`** 를 연동한다!

![](https://velog.velcdn.com/images/silverclean091/post/36e44e12-4363-4457-be7a-a69465b774f6/image.png)

터미널에 Claude Code를 설치하기 위해서는 먼저 `Node.js` 의 설치가 선행되어 있어야 한다. 본 포스팅에서는 **이미 설치가 되어있다고 가정** 한 뒤 진행한다.

설치가 안 되어있을 경우에는 이쪽으로!: **[https://nodejs.org/ko](https://nodejs.org/ko)**

`Node.js` 의 설치가 완료되었다면, Claude Code 설치를 위해 **터미널** 에 다음과 같이 입력한다.

```bash
npm install -g @anthropic-ai/claude-code
```

이후 `cd` 명령어로 작업 폴더의 위치로 이동한 뒤, **`claude` 라는 단어 하나만 명령어로 입력** 하면 실행 준비 끝!

`claude` 를 입력하고 나면 본격적으로 **Claude Code에 연결하기 위한 몇 가지 절차** 가 진행되는데, 보통 다음과 같이 진행하면 된다.

1. **폴더 신뢰 여부**: `1. Yes, I trust this folder` 선택
2. **스타일 옵션 선택**: `Dark` 혹은 `Light` 등 원하는 모드 선택
3. **로그인 방식 선택**: API 방식 활용을 위한 `2. Anthropic Console account` 선택

![](https://velog.velcdn.com/images/silverclean091/post/68a3052e-b5d6-4311-9cfc-f9ade9720255/image.png)

이후 **브라우저** 가 열렸을 때 본인의 계정과 연동하면, 성공적으로 **Claude Code 연결 완료!** 참고로 해당 방식은 토큰 사용량에 따라 요금이 부과될 수 있으니 과도한 비용 발생을 꼭 조심해야 한다...

### 💚 5단계: 지식 데이터 적재하기

LLM 연동까지 모두 완료되었으면, 최종적으로 LLM Wiki를 사용해보기 위하여 임시 데이터의 삽입이 필요하다.

![](https://velog.velcdn.com/images/silverclean091/post/993adc39-0263-4527-8878-7b6b71dd8ea2/image.png)

본 포스팅에서는 **"한 번 구축해보기~" 수준** 으로 위키를 구축하였기에 '무조건 넣어야 한다'는 데이터는 없음! 따라서 **회의록 데이터와 WBS 계획 등을 Claude나 GPT로부터 임의로 뽑아내어 첨부** 하였다.

사용한 **프롬프트** 는 아래와 같으며, 이후 LLM이 던져준 데이터를 각각 `raw` 폴더 내에 그대로 저장하였다.

> 💬 **임시 데이터 생성용 예시 프롬프트**
> 
> ```md
> '프로젝트 회의록과 일정을 관리하는 LLM Wiki'를 간단하게 구축해볼 예정이야. 따라서 raw 폴더 내에 들어갈 파일을 생성해주었으면 해.
> 
> 1. 주제는 '신규 앱 기획 및 개발'이며, 폴더 구조는 아래와 같아.
> /
> ├── raw/
> │   ├── meetings/      # 회의록 원본 (수정 금지)
> │   └── plannings/     # 기획/일정 원본 (수정 금지)
> └── wiki/
>     ├── decisions/     # raw에서 추출한 프로젝트 결정 사안
>     └── definitions/   # 프로젝트 용어 정의
> 2. 생성하고자 하는 파일은 총 6개야: 회의록 파일 4개, 일정 파일 2개
> 3. 이 파일들은 원문의 형태여도 상관없으며, 추후 decisions와 definitions 폴더에 지식을 적재하기 용이한 내용으로 만들어줬으면 해.
> 4. 각 파일의 형태는 md 확장자로 만들어줘.
> ```

![](https://velog.velcdn.com/images/silverclean091/post/ec7d7920-aa24-41c3-b79c-b31e4082af6c/image.png)

## 🤖 LLM Wiki 사용해보기

### 1️⃣ Ingest: 새로운 자료 기반의 wiki 작성

새로운 raw 파일을 6개 추가했으니, 이제 **본격적으로 LLM Wiki를 사용** 해볼 차례다.

첫 번째로 수행할 작업은 바로 **`Ingest`! 추가한 자료를 요약 및 관계도를 연결하여 말 그대로의 'wiki'를 생성하는 작업** 이다. 현재 wiki 폴더에는 아무 파일도 존재하지 않으므로, **wiki를 본격적으로 사용하기 위한 첫 출발점** 이 되는 셈!

![](https://velog.velcdn.com/images/silverclean091/post/1266b9c7-b466-4c63-81dc-6b5910361e28/image.png)

이를 위해서는 Claude Code 터미널에 `Ingest` 라는 명령어를 입력하면 된다.

Claude Code의 특성상 **세부 작업 하나하나마다 수락을 받아 작업** 을 진행하게 되므로, 선택지가 나타난다면 작업 내용을 확인하고 `1번` 을 체크해주면 된다.

![](https://velog.velcdn.com/images/silverclean091/post/97df3178-0661-48d3-97f9-30c20e6979a3/image.png)

작업이 완료될 경우, Obsidian으로 돌아가보면 다음과 같이 **회의록과 일정 기반으로 핵심 내용이 요약된 wiki 항목들이 생성된 것** 을 확인할 수 있다!

### 2️⃣ Query: wiki 내용 기반의 질의응답

이제 사용자와 LLM이 참고할 수 있는 wiki 항목들이 생성되었으니, 이를 기반으로 **질의응답** 을 주고받을 차례다.

해당 섹션은 별도의 명령어 키워드가 존재하지 않는다. 그냥 문서를 읽다가 생기는 궁금한 점, 혹은 찾고싶은 안건의 회의 일자 등... **프로젝트의 내용과 관련하여 궁금한 사항을 자연어로 질문** 만 한다면 **LLM이 wiki와 원본 파일들을 검색하여 지식 기반의 답변을 제공** 해준다.

여기에서는 가벼운 질문 두 가지를 던져보았다.

![](https://velog.velcdn.com/images/silverclean091/post/44c00f95-3984-4217-ba98-0a23abcd6e8a/image.png)

첫 번째로 `현재 일자 기준으로 가장 급한 업무가 뭐야? 우선순위별로 나눠서 알려줘.`라는 질문을 던져보았다.

LLM은 wiki 내 문서를 검색하여 **우선순위를 매겨 업무를 리스트업** 해준다. 또한 raw 폴더 내의 최신 회의록은 6월 25일 일자이나, 작성일 기준 현재 일자는 7월 28일이기에 마지막 코멘트로 **wiki 내 일자와 현재 일자의 간극을 언급하며 변경사항이 있을 수 있음을 주의** 하라고 알려주고 있다!

![](https://velog.velcdn.com/images/silverclean091/post/3e64517d-96dc-4acd-a809-6df10ddb44b0/image.png)

두 번째로는 `현재 개발이 어느정도 진행되었는지 알려줘.`라는 질문을 던져보았다.

마찬가지로 LLM은 wiki 정보를 바탕으로 **현재의 개발 진행 상황을 분석** 한다. 또한 추가로 요구하지 않았음에도 알아서 **표의 형태로 가독성을 높여 제공** 해주는 것을 알 수 있다!

내용이 길어서 스크린샷 내에는 생략되었으나, 전체 진도를 제외하고도 `MVP 4대 기능별 상태`, `주요 일정 현황`, `진행 예정 구간`, `개발 과정의 이슈 이력`, `팀별 개발 진행 사항`, `현황 요약` 까지 여러 항목을 추가적으로 진행해주었다.

어떤 모델을 사용하느냐에 조금씩 따라 다를 수 있겠으나... **참으로 똘똘한 녀석이다!!**

### 3️⃣ Lint: LLM Wiki 자가 진단

마지막으로 시험해볼 기능은 **LLM Wiki 자가진단 기능** 이다.

해당 기능을 사용하기 위해서는 LLM에게 단순히 `Lint` 라고 입력해도 괜찮고, **`위키 자가 진단을 수행해줘` 등의 자연어** 로 입력해도 괜찮다.

![](https://velog.velcdn.com/images/silverclean091/post/2873f9f5-33af-4a52-832b-a58a710f05dd/image.png)

명령어를 입력하면 LLM은 즉시 **wiki 자가 진단을 시작** 한다.

진단은 **지침에 작성한대로** 고아 페이지 확인, 깨진 링크, 상충 정보, 누락된 관계 등에 대해 진행하며 이 밖에도 파일명이 일관되지 않게 저장되어 있다거나 양식이 충돌하는 등의 오류도 알아서 고쳐준다.

![](https://velog.velcdn.com/images/silverclean091/post/c61e4ee0-637a-45ee-a2e2-42dae3557c86/image.png)

이후 결과적으로는 다음과 같이 **진단 보고서** 까지 작성해준다. 이는 프로젝트 최상단 루트파일 내에 `md` 파일 형태로 저장되며, 마찬가지로 **폴더 구조를 추가로 구축하여 관리하거나 생성** 할 수 있다.

여기까지 하면 드디어! **LLM Wiki의 핵심 기능 체험** 이 끝이 난다. 야호!

## 💡 (번외) 알아두면 상당히 도움이 되는 정보들!

아래 내용들은 알아두면 상당히 도움이 되는... 유용한 정보 몇 가지에 대해 작성한다.

사실 Github는 몰라도 `Index` 파일과 `Log` 파일은 **거의 필수** 라고 봐도 좋음... **사실 내가 따로 정의해두지 않아도 LLM이 높은 확률로 임의로 생성해버린다(ㅋㅋ).** 이렇게 생성된 파일을 기반으로 응용하면 상당히 도움이 되니 잘 응용해볼 것!

본 섹션에서는 용도와 기능 등에 대해서만 간단하게만 짚고 넘어갈 예정!

### 🏷️ INDEX.md과 LOG.md 파일

`INDEX.md` 파일은 **`Ingest` 명령을 처음 실행하면 `wiki` 폴더 내에 자동으로 생성되는 파일** (이 경우 이름은 그냥 `INDEX.md` 일 수도, `WIKI_INDEX.md` 일 수도... 다른 형태일 수도 있다! 어쨌든 용도는 같음)로, **위키에 있는 모든 페이지를 모아두는 카탈로그 역** 을 한다.

![](https://velog.velcdn.com/images/silverclean091/post/107bdb59-7c1e-425c-82da-a3393f13ea30/image.png)

즉, 이 페이지가 어떤 페이지고, 며칠에 생성됐으며, 자료는 어느 정도의 크기인지 등... **자료의 정보와 메타 데이터에 대해 요약해둔 파일** 이다.

따라서 특정 파일을 찾고싶다면 이러한 `INDEX.md` 파일을 참고하여 찾으면 큰 도움이 되며, **LLM 또한 답변을 할 때 이 `INDEX.md` 파일을 참고** 하여 접근하고자 하는 특정 문서를 판단한다. 이후 링크를 타고 들어가 상세 페이지의 내용을 참고하여 답변을 생성하는 방식!

![](https://velog.velcdn.com/images/silverclean091/post/81a78653-e91b-472b-ae3a-7107856d02e0/image.png)

`LOG.md` 파일은 말 그대로 **LLM의 wiki 작업 내용에 대한 로그** 를 남겨두는 파일이다.

이 파일의 경우 별도로 지침으로 작성해두지 않는 이상 **자동으로 생성되지 않거나**, 혹은 `INGEST_REPORT` 등의 이름으로 **매번 작업에 대한 파일을 생성 혹은 업데이트하는 식** 으로 작동한다.

따라서 로그 기능의 경우 **미리 지침으로 입력해두면 큰 도움이 된다.** 작업이 어긋났을 때 어디에서부터 어긋났는지 쉽게 찾아볼 수 있고, 이에 따라 **버전 관리** 가 훨씬 용이해지기 때문!

`INDEX.md` 과 `LOG.md` 파일의 경우, `CLAUDE.md` 파일 내 `Ingest` 부분에 아래와 같은 **간단한 지침을 몇 줄 추가하는 걸로 손쉽게 관리 및 사용** 이 가능하다.

> 💬 **INDEX 파일과 LOG 파일 관리를 위한 지침 추가**
> 
> ```
> - **인덱스 갱신**: \`wiki/index.md\`를 갱신한다. (새 페이지를 해당 카테고리 아래에 추가).
> - **작업 로그 관리**: \`wiki/log.md\`에 한 줄 기록한다.
>     - \`log.md\` 항목 형식: \`## [YYYY-MM-DD] ingest|query|lint — 제목\`
> ```

### 🐈⬛ Github 플러그인 연동하기

Github 플러그인 연동의 경우... 사실상 필수는 아니나, 본인 스스로 **백업이 필요하다** 고 느끼거나 혹은 **협업이 필요할 경우** 유용하게 사용할 수 있기에 추가적으로 하나의 섹션으로 간단하게 소개하기로 했다.

따라서 본 섹션에서는 **Git 명령어 하나하나까지는 구체적으로 다루지 않는다.**

![](https://velog.velcdn.com/images/silverclean091/post/30f350bd-e099-4320-94bd-7273a52b91f3/image.png)

Github 연동을 위해서는 먼저 **플러그인 활성화** 가 필요하다.

Obsidian에서는 여러가지 플러그인을 활용할 수 있는데, 이를 위해서는 별도로 설정에서 **'플러그인 활성화'** 를 켜주는 것이 필요하다.

이는 `설정` > `커뮤니티 플러그인` 으로 접근하여 우측 최하단의 **`커뮤니티 플러그인 사용` 버튼** 을 클릭하면 된다.

![](https://velog.velcdn.com/images/silverclean091/post/bc504fe8-a814-4836-90de-0b8781c7cc7b/image.png)

사용 버튼을 클릭한 이후라면, 같은 설정창에서 **`커뮤니티 플러그인 탐색` 버튼** 을 클릭하고 **`Git` 이라는 단어를 검색** 한다.

이후 바로 첫 번째에 뜨는, **개발자가 `Vinzent` 행님이라고 적혀있는 플러그인을 클릭하여 설치** 하면 1차 환경 세팅이 끝난다. 상단에 보라색으로 `설치` 라고 적혀있는 버튼이 **`활성화` 라고 바뀌면** 플러그인 설치가 완료된 것!

해당 플러그인은 **Git 자동화 플러그인** 이며, **`pull` 이나 `push` 등의 명령을 자동으로 수행** 해준다. 다만 `push` 의 경우... 개인용도로 사용할게 아니라면 **인간의 충분한 판단을 거친 이후 수동으로 하는 것을 추천.**

여기에서는 **`pull` 자동화** 에 대해서만 다룬다. 자동화를 하기 위해서는 당연히 **Git Repo를 파서 첫 커밋** 을 해둬야 하며... 앞서 말했듯 이 과정은 생략!

필요할 경우 아래 명령어를 참고하여 순차적으로 입력하면 도움이 될 것이다.

> 💬 **Repository 연동 및 첫 커밋을 위한 git 명령어**
> 
> ```
> git init
> git add .
> git commit -m "first commit"
> git branch -M main
> git remote add origin [본인의 Repository URL]
> git push -u origin main
> ```

이후로는 매우 간단하다!

![](https://velog.velcdn.com/images/silverclean091/post/e2cd6431-2904-4f81-b1e1-d51c3420237c/image.png)

먼저 아까의 플러그인 화면으로 들어가서 마찬가지로 **Git 플러그인 창** 을 오픈하고, **`활성화` 버튼** 을 누른 뒤 나타나는 **`옵션` 버튼** 을 클릭한다.

![](https://velog.velcdn.com/images/silverclean091/post/4065e446-ea63-414b-b50b-8ca3877935ed/image.png)

그리고는 쭉쭉쭉쭉... 스크롤을 내려 **`pull` 카테고리** 의, **`Pull on startup` 항목을 활성화** 하면 끝! 해당 기능을 활성화해두면 **Obsidian을 켤 때마다 자동으로 pull 명령어를 수행** 하게 된다.

충돌 확률을 크게 줄여주므로 매우 편리한 기능!

## 🐹 포스팅 마무리!

이렇게... 정말 길고길고길고길고 긴 LLM Wiki 포스팅이 끝이 났다. 어째 글을 쓰면 쓸 수록 점점 길어지고 있는 것 같은 느낌...

카더라 통신에 의하면 이미 몇몇 기업들은 LLM Wiki를 실무에 도입하고 있다고 한다. 본격적으로 등장한지 얼마 안 된 개념인만큼 잘 사용하며 디벨롭하다보면 **나중에는 훨씬 도움이 되는 형태로 발전할지도?** 여러모로 미래가 기대되는 녀석.

나도 이번에 프로젝트를 하나 진행하게 되며 처음 알게된 개념인데, 사용법도 간단한데다 Notion과 Claude를 이중으로 사용하는 것보다 훨씬 간편한 것 같아서 **앞으로도 야무지게 사용해볼 예정** 이다.

기회가 된다면 다른 포스트에서 또 다룰 수 있을지도!

![](https://velog.velcdn.com/images/silverclean091/post/c098bdd9-6f2b-4365-9d37-316725da7c62/image.png)

어쨌든 오늘의 포스팅은 여기서 마무리! 읽어주셔서 감사함니다.

> 🩷 **좋아요를 눌러주심 저에게 큰 힘이 댑니다... 압도적 감사!!**

## 📚 참고 자료

1. [\[wikidocs\] LLMd위키 완벽 가이드](https://wikidocs.net/353379)
2. [\[BOOTTENT\] 안드레 카파시의 LLM Wiki란? 완벽한 AI 지식 체계 w. 클로드코드 & 옵시디언](https://boottent.com/community/article/20260602110859)
3. [\[Velog\] 내 머리를 대신할 AI 지식 비서, LLM 위키 만들기 완전 가이드 | CHAN LIM](https://velog.io/@chan9708/%EB%82%B4-%EB%A8%B8%EB%A6%AC%EB%A5%BC-%EB%8C%80%EC%8B%A0%ED%95%A0-AI-%EC%A7%80%EC%8B%9D-%EB%B9%84%EC%84%9C-LLM-%EC%9C%84%ED%82%A4-%EB%A7%8C%EB%93%A4%EA%B8%B0-%EC%99%84%EC%A0%84-%EA%B0%80%EC%9D%B4%EB%93%9C)
4. [\[tistory\] LLM Wiki란 무엇인가? | Toritol](https://dslyh01.tistory.com/92)
5. [\[Publish Obsidian\] Claude Code 설치 가이드 | 데이터웨이브](https://publish.obsidian.md/datawave/%ED%81%B4%EB%A1%9C%EB%93%9C+%ED%81%B4%EB%9E%98%EC%8A%A4/Claude+Code+%EC%84%A4%EC%B9%98+%EA%B0%80%EC%9D%B4%EB%93%9C)

[![profile](https://velog.velcdn.com/images/silverclean091/profile/c6e6d94c-862f-4447-87d2-6a7e26a6339d/image.jpeg)](https://velog.io/@silverclean091/posts)

우리집 기술블로그 정상영업합니다... 😇

이전 포스트

[![Powered by GraphCDN, the GraphQL CDN](https://i.imgur.com/BMhDSUt.png)](https://graphcdn.io/?ref=powered-by)

<iframe sandbox="allow-forms allow-popups allow-popups-to-escape-sandbox allow-same-origin allow-scripts allow-top-navigation-by-user-activation" frameborder="0" allow="run-ad-auction" src="https://googleads.g.doubleclick.net/pagead/ads?client=ca-pub-5574866530496701&amp;output=html&amp;adk=1812271804&amp;adf=3025194257&amp;abgtt=6&amp;lmt=1788140362&amp;plaf=1%3A2%2C2%3A2%2C7%3A2&amp;plat=1%3A128%2C2%3A128%2C3%3A128%2C4%3A128%2C8%3A128%2C9%3A32776%2C16%3A8388608%2C17%3A32%2C24%3A32%2C25%3A32%2C30%3A1081344%2C32%3A32%2C41%3A32%2C42%3A32%2C43%3A32%2C44%3A32&amp;format=0x0&amp;url=https%3A%2F%2Fvelog.io%2F%40silverclean091%2FAI-LLM-Wiki%25EB%25A1%259C-AI-%25EB%25B6%2580%25EB%25A0%25A4%25EB%25A8%25B9%25EA%25B8%25B0&amp;pra=5&amp;asro=0&amp;aimartd=4&amp;aieuf=1&amp;aicrs=1&amp;uach=WyJXaW5kb3dzIiwiMTkuMC4wIiwieDg2IiwiIiwiMTUyLjAuNzk3Ny42NCIsbnVsbCwwLG51bGwsIjY0IixbWyJDaHJvbWl1bSIsIjE1Mi4wLjc5NzcuNjQiXSxbIk5vdD9BX0JyYW5kIiwiMjQuMC4wLjAiXSxbIkdvb2dsZSBDaHJvbWUiLCIxNTIuMC43OTc3LjY0Il1dLDBd&amp;dt=1788140361976&amp;bpp=2&amp;bdt=1030&amp;idt=178&amp;shv=r20260825&amp;mjsv=m202608250101&amp;ptt=9&amp;saldr=aa&amp;abxe=1&amp;cookie=ID%3D110b5b4069eed1c1%3AT%3D1760332166%3ART%3D1787807582%3AS%3DALNI_MZOV6LuBPMiq48qlbqc1RootzeH4w&amp;gpic=UID%3D0000129d6686ed76%3AT%3D1760332166%3ART%3D1787807582%3AS%3DALNI_MYJ83L8GPGKwOH3hFPbqZ1kzdkyqw&amp;eo_id_str=ID%3Dc93d1eb0db821cad%3AT%3D1772785189%3ART%3D1787807583%3AS%3DAA-Afja1XV94IqbrNoMKtmt7OIEo&amp;nras=1&amp;correlator=4646742792336&amp;frm=20&amp;pv=2&amp;u_tz=540&amp;u_his=1&amp;u_h=1080&amp;u_w=1920&amp;u_ah=1032&amp;u_aw=1920&amp;u_cd=24&amp;u_sd=1&amp;dmc=32&amp;adx=-12245933&amp;ady=-12245933&amp;biw=1905&amp;bih=911&amp;scr_x=0&amp;scr_y=0&amp;eid=95388157%2C95399629%2C95373848&amp;oid=2&amp;pvsid=4086812017903154&amp;tmod=634198163&amp;uas=0&amp;nvt=1&amp;fsapi=1&amp;ref=https%3A%2F%2Fwww.google.com%2F&amp;fc=1920&amp;brdim=1920%2C0%2C1920%2C0%2C1920%2C0%2C1920%2C1032%2C1920%2C911&amp;vis=1&amp;rsz=%7C%7Cs%7C&amp;abl=NS&amp;fu=32768&amp;bc=31&amp;bz=1&amp;pgls=CAk.&amp;ifi=1&amp;uci=a!1&amp;fsb=1&amp;dtd=192" title="Advertisement" aria-label="Advertisement"></iframe>

## 방법론 / 아키텍처


## 결과 / 시사점


## 관련 노트
-