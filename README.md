# cc-layouts — CodeCompose Hugo Theme Module

Hugo Module로 제공되는 독립 커스텀 테마입니다. Congo 등 외부 테마 없이 단독으로 동작합니다.

## v0.2.0 변경 사항

- Congo 테마 의존 완전 제거 — 독립 커스텀 테마로 전환
- 단일 CSS (`assets/css/main.css`) — CSS custom properties, 자동 다크모드
- 폰트: AstaSans (헤딩) + Pretendard (본문), 모두 CDN
- 아이콘: Tabler Icons (CDN)
- 네비게이션: 고정 blur 네비 + 모바일 햄버거 + 언어 전환
- 코스 카드, 블로그 카드, 카테고리 필터, 페이지네이션, TOC 등 자체 구현

## 요구사항

- Hugo extended v0.145+
- Go 1.23+

## 사이트에서 사용하기

### 1. go.mod 설정

```bash
hugo mod init github.com/you/your-site
```

### 2. hugo.toml에 모듈 import

```toml
[module]
  [[module.imports]]
    path = "github.com/CodeCompose7/cc-layouts"
```

Congo나 다른 테마를 import할 필요 없습니다.

### 3. 로컬 개발 시 (cc-layouts를 로컬에서 수정할 때)

`go.mod`에 replace 추가:

```
replace github.com/CodeCompose7/cc-layouts => ../cc-layouts
```

## 사이트 설정 (hugo.toml)

### 필수 파라미터

```toml
[params]
  email = "your@email.com"
  github = "https://github.com/your-org"

  [params.business]
    name = "회사명"
    # ... 사업자 정보

  [params.homepage]
    showRecent = true
    showRecentFolders = ["blog"]
    recentLimit = 5
```

### 언어별 파라미터

```toml
[languages.ko.params]
  dateFormat = "2006년 1월 2일"
  footer_courses = "강의"
  footer_blog = "블로그"
  footer_about = "소개"
  footer_contact = "연락처"
  footer_company = "회사명"
  footer_business = "사업자 정보 HTML"

  [languages.ko.params.author]
    name = "이름"
    image = "img/profile.png"
    headline = "소개 문구"
```

### 메뉴

```toml
[[languages.ko.menu.main]]
  name = "홈"
  pageRef = "/"
  weight = 1
[[languages.ko.menu.main]]
  name = "강의"
  pageRef = "courses"
  weight = 2
# ...
```

## 콘텐츠 구조

```
content/
├── _index.ko.md          # 홈페이지
├── courses/
│   ├── _index.ko.md      # 강의 목록 (sortBy, sortOrder 지원)
│   ├── _categories/      # 카테고리별 필터 페이지
│   └── course-name/
│       └── index.ko.md   # 개별 강의 (level, hours, version 지원)
├── blog/
│   ├── _index.ko.md      # 블로그 목록 (sidebarImage, pagerSize 지원)
│   ├── _categories/
│   └── post-name/
│       └── index.ko.md
├── about/
│   └── _index.ko.md      # 소개 (staff 배열 지원)
└── tags/
```

### 강의 front matter

```yaml
title: "강의 제목"
level: 3        # 난이도 1-5 (별점 표시)
hours: "2:30"   # 수강시간 H:MM
version: 2      # 버전 (1이면 미표시)
weight: "2601"  # 정렬 가중치
categories: ["fundamentals"]
tags: ["Python", "AI"]
```

## 제공 레이아웃

| 파일                   | 설명                                             |
| ---------------------- | ------------------------------------------------ |
| `_default/baseof.html` | 기본 HTML 구조 (CSS pipeline, meta, nav, footer) |
| `_default/single.html` | 글/강의 상세 (TOC, breadcrumbs, 메타)            |
| `_default/list.html`   | 기본 목록                                        |
| `_default/term.html`   | 태그/카테고리 term                               |
| `index.html`           | 홈페이지 (프로필, 최근 글)                       |
| `courses/list.html`    | 강의 목록 (정렬/필터)                            |
| `blog/list.html`       | 블로그 목록 (사이드바/페이지네이션)              |
| `about/list.html`      | 소개 (프로필 카드)                               |
| `taxonomy.html`        | 택소노미 그리드                                  |
| `404.html`             | 404 에러                                         |

### 숏코드

- `{{</* lead */>}}` — 강조 문단
- `{{</* mermaid */>}}` — Mermaid 다이어그램
- `{{</* bookmark url="" title="" */>}}` — 북마크 카드
- `{{</* reflangtitle path="" */>}}` — 다국어 페이지 참조 링크

## 로컬 테스트

```bash
# Docker
docker compose up

# 또는 직접 실행
hugo server -D --bind 0.0.0.0 --port 1313
```
