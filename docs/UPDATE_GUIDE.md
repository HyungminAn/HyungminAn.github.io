# 홈페이지 업데이트 가이드

Beautiful Jekyll 테마 기반 개인 홈페이지(`HyungminAn.github.io`)를 수정하는 방법을 정리한 문서입니다.
같은 내용의 HTML 버전은 [`update-guide.html`](update-guide.html) 에 있습니다.

> `docs/` 폴더는 `_config.yml` 의 `exclude` 에 들어 있어서 실제 홈페이지에는 노출되지 않습니다.

---

## 1. 사이트 구성 한눈에 보기

| 메뉴 | URL | 수정할 파일 |
|---|---|---|
| 홈 (최근 글) | `/` | `index.html` (제목/부제만) |
| About Me (자기소개) | `/aboutme` | `aboutme.md` |
| Contact (연락처) | `/contact` | `contact.md`, `_config.yml` 의 `social-network-links` |
| Board (게시판 전체) | `/board` | `board.html` (보통 수정할 필요 없음) |
| Board › 토픽별 | `/board/<토픽id>/` | `board/<토픽id>.md` |
| 글 | `/YYYY-MM-DD-제목/` | `_posts/YYYY-MM-DD-제목.md` |

```
.
├── _config.yml          # 사이트 전체 설정 (제목, 메뉴, 소셜 링크, 색상 …)
├── _data/topics.yml     # 게시판 토픽 목록
├── _layouts/topic.html  # 토픽별 게시판 레이아웃
├── _includes/post-list.html  # 게시판 글 목록 조각
├── _posts/              # 글 (Markdown)
├── board.html           # 게시판 전체 페이지
├── board/               # 토픽별 게시판 페이지 (research.md, dev.md, daily.md)
├── aboutme.md           # 자기소개
├── contact.md           # 연락처
├── index.html           # 홈 (최근 글 목록)
└── assets/img/          # 이미지
```

---

## 2. 자기소개 수정 — `aboutme.md`

파일 위쪽 `---` 사이(front matter)는 페이지 제목/부제이고, 그 아래가 본문입니다.

```markdown
---
layout: page
title: About Me
subtitle: 자기소개
---

안녕하세요, **HyungminAn** 입니다. ...

### 관심 분야
- ...
```

- `<!-- TODO ... -->` 로 표시된 부분을 실제 내용으로 바꾸세요.
- 프로필 사진을 바꾸려면 `assets/img/avatar-icon.png` 를 교체하거나, `_config.yml` 의 `avatar:` 경로를 바꿉니다.

---

## 3. 연락처 수정 — `contact.md` + `_config.yml`

### 3-1. Contact 페이지 본문 (`contact.md`)

```markdown
- <i class="fas fa-envelope"></i> **Email**: [me@example.com](mailto:me@example.com)
- <i class="fab fa-github"></i> **GitHub**: [github.com/HyungminAn](https://github.com/HyungminAn)
```

아이콘은 [Font Awesome](https://fontawesome.com/search?ic=free) 이름을 쓰면 됩니다 (`fas fa-...`, `fab fa-...`).

### 3-2. 모든 페이지 하단(footer) 아이콘 (`_config.yml`)

```yaml
social-network-links:
  email: "me@example.com"    # 주석(#)을 지우면 footer 에 표시됨
  rss: true
  github: HyungminAn
#  linkedin: your-id
#  google-scholar: your-id
```

> 이메일은 현재 예시 값(`your.email@example.com`)으로 되어 있고 footer 에서는 주석 처리되어 있습니다. 공개해도 되는 주소로 바꿔 주세요.

---

## 4. 게시판에 새 글 쓰기 — `_posts/`

### 4-1. 파일 만들기

`_posts/` 폴더에 **`YYYY-MM-DD-영문-제목.md`** 형식으로 파일을 만듭니다.

```
_posts/2026-11-01-my-first-paper-review.md
```

- 날짜가 파일명에 꼭 있어야 합니다.
- 파일명의 제목 부분이 URL 이 되므로 영문/숫자/하이픈을 권장합니다.
- **미래 날짜**의 글은 기본적으로 빌드되지 않습니다.

### 4-2. Front matter 작성

```markdown
---
title: 논문 리뷰 - Attention Is All You Need
subtitle: Transformer 정리        # 선택
category: research                # 게시판 토픽 id (필수) — _data/topics.yml 의 id
tags: [paper, nlp]                # 선택 — /tags 페이지에 모임
cover-img: /assets/img/path.jpg   # 선택 — 상단 큰 이미지
thumbnail-img: /assets/img/thumb.png  # 선택 — 목록 썸네일
mathjax: true                     # 선택 — 수식($...$) 사용 시
---

본문은 Markdown 으로 작성합니다.
```

| 키 | 설명 |
|---|---|
| `category` | 어떤 게시판(토픽)에 올라갈지. `research` / `dev` / `daily` 중 하나 |
| `tags` | 토픽과 별개의 키워드. 여러 개 가능 |
| `layout` | 생략 가능 (`_config.yml` 에서 글은 자동으로 `post`) |

### 4-3. 본문 팁

- 이미지: `assets/img/` 에 파일을 넣고 `![설명](/assets/img/파일명.png)`
- 코드 블록: ```` ```python ```` … ```` ``` ````
- 강조 박스: 문단 바로 위에 `{: .box-note}` (`.box-warning`, `.box-error`, `.box-success`)
- 예시 글: `_posts/2026-10-24-markdown-cheatsheet.md`

### 4-4. 글 수정 / 삭제

- 수정: 해당 `.md` 파일을 고치고 push
- 삭제: 해당 `.md` 파일을 지우고 push
- 예시 글 2개(`2026-10-24-markdown-cheatsheet.md`, `2026-10-25-welcome.md`)는 지워도 됩니다.

---

## 5. 게시판 토픽 추가 / 변경

예: **`paper`(논문)** 토픽을 추가하는 경우 — 3군데를 수정합니다.

**① `_data/topics.yml`** 에 항목 추가

```yaml
- id: paper
  name: 논문
  description: 읽은 논문 정리
```

**② `board/paper.md`** 파일 생성

```markdown
---
layout: topic
title: 논문
topic: paper
permalink: /board/paper/
---
```

**③ `_config.yml`** 의 메뉴에 추가

```yaml
navbar-links:
  About Me: "aboutme"
  Contact: "contact"
  Board:
    - 전체: "board"
    - 연구: "board/research"
    - 개발: "board/dev"
    - 일상: "board/daily"
    - 논문: "board/paper"     # 추가
```

이후 글에서 `category: paper` 를 쓰면 해당 게시판에 표시됩니다.

- **이름만 변경**: `topics.yml` 의 `name`, `board/<id>.md` 의 `title`, 메뉴 이름을 바꾸면 됩니다.
- **토픽 삭제**: 위 3군데에서 지우고, 그 토픽을 쓰던 글의 `category` 도 바꿔 주세요.
- `id` 는 영문 소문자로 쓰세요 (글의 `category` 값과 정확히 같아야 합니다).

---

## 6. 사이트 전체 설정 — `_config.yml`

| 항목 | 설명 |
|---|---|
| `title`, `author` | 사이트 이름, footer 이름 |
| `navbar-links` | 상단 메뉴 |
| `avatar` | 상단 프로필 이미지 |
| `social-network-links` | footer 소셜 아이콘 |
| `page-col`, `link-col`, `navbar-col` … | 색상 |
| `date_format` | 날짜 표시 형식 (현재 `%Y-%m-%d`) |
| `timezone`, `language` | `Asia/Seoul`, `ko` |
| `giscus` / `utterances` | 댓글 기능 (주석 해제 후 설정) |

> `_config.yml` 은 `jekyll serve` 실행 중에도 자동 반영되지 않습니다. 수정 후 서버를 재시작하세요.

---

## 7. 로컬에서 미리보기 (선택)

Ruby 3.x 가 설치되어 있어야 합니다.

```bash
bundle install
bundle exec jekyll serve
# → http://localhost:4000 에서 확인
```

---

## 8. 배포

GitHub Pages 가 저장소의 기본 브랜치를 자동으로 빌드합니다.

```bash
git add .
git commit -m "Add new post"
git push
```

- 처음 한 번: GitHub 저장소 **Settings → Pages → Build and deployment** 에서
  Source 를 **Deploy from a branch**, 브랜치를 `master`(또는 `main`) / `/ (root)` 로 지정합니다.
- push 후 1~2분 뒤 `https://hyungminan.github.io` 에 반영됩니다.
- GitHub 웹에서 파일을 직접 편집(연필 아이콘)하고 Commit 해도 똑같이 반영됩니다.

---

## 9. 처음에 채워야 할 체크리스트

- [ ] `aboutme.md` — 소개, 관심 분야, 경력, 학력
- [ ] `contact.md` — 이메일, LinkedIn 등 실제 값
- [ ] `_config.yml` — `social-network-links` 의 `email` 주석 해제 및 값 입력
- [ ] `assets/img/avatar-icon.png` — 프로필 사진 교체
- [ ] `_data/topics.yml` — 원하는 토픽으로 조정 (메뉴, `board/*.md` 도 함께)
- [ ] 예시 글 삭제 후 첫 글 작성
