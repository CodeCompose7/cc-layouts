# 변경 이력

이 프로젝트의 모든 주요 변경사항은 이 파일에 기록됩니다.

형식은 [Keep a Changelog](https://keepachangelog.com/ko/1.0.0/)를 따르며,
이 프로젝트는 [Semantic Versioning](https://semver.org/lang/ko/)을 준수합니다.

## 0.3.6 - 2026-04-09

### 변경됨 0.3.6

- 인증 가드 비활성화 옵션 추가 — `site.Params.disableAuth = true` 설정 시 `auth` front matter가 있어도 인증 없이 콘텐츠 표시 (로컬 개발 모드 지원)

## 0.3.5 - 2026-04-05

### 수정됨 0.3.5

- 인증 가드 콘텐츠 숨김 방식 개선 — `display:none` 대신 `visibility:hidden; height:0; overflow:hidden` 사용으로 인증 통과 후 레이아웃 복원 안정화

## 0.3.4 - 2026-04-04

### 추가됨 0.3.4

- **인증 가드 (Auth Guard)** — front matter에 `auth: paid` / `auth: admin` 설정 시 Firebase 기반 Google 로그인 인증 후 콘텐츠 접근 제어
  - `layouts/partials/auth-guard.html` 추가
  - 티어별 접근 제한 (free / paid / admin)
  - 인증 실패 시 로그인 유도 UI 표시
  - `baseof.html`에 인증 필요 페이지 분기 처리 추가

## 0.3.3 - 2026-03-27

### 수정됨 0.3.3

- `iframe` 숏코드 URL 처리 로직 개선 — `absURL` 대신 `Site.BaseURL` 직접 조합 방식으로 변경하여 서브디렉토리 배포 환경에서 경로 오류 수정

## 0.3.2 - 2026-03-27

### 변경됨 0.3.2

- `iframe` 숏코드 URL 처리 방식 변경 — 외부 URL(`http`로 시작)은 그대로 사용, 내부 경로는 `absURL` 적용

## 0.3.1 - 2026-03-27

### 수정됨 0.3.1

- `iframe` 숏코드 내부 경로 URL 처리 누락 수정 — `src` 파라미터에 `relURL` 적용

## 0.3.0 - 2026-03-27

### 개선됨 0.3.0

- 본문 이미지 중앙 정렬 (`margin: 16px auto; display: block`)
- Mermaid 다이어그램 중앙 정렬 (`display: flex; justify-content: center`)

## 0.2.9 - 2026-03-27

### 추가됨 0.2.9

- 카드 태그 목록 2줄 초과 시 말줄임(`···`) 처리 — article/course 카드의 태그가 3줄 이상이면 초과 태그 숨김 및 `···` pill 표시

### 개선됨 0.2.9

- 카드 태그 목록 높이 고정 (`height: 56px`) — 카드 높이 일관성 유지

## 0.2.8 - 2026-03-27

### 추가됨 0.2.8

- `math` 숏코드 추가 — 인라인/블록 수식 렌더링 지원 (`inline="true"` 파라미터)
- markup 설정에 TOC 레벨 설정 추가 (`startLevel = 2`, `endLevel = 3`)

## 0.2.7 - 2026-03-27

### 추가됨 0.2.7

- `iframe` 숏코드 추가 — 외부 콘텐츠 임베드, 자동 높이 조절 옵션(`autoresize`) 지원
- `katex` 숏코드 추가 — 페이지 단위 KaTeX 수식 렌더링 지원
- markup 설정 파일 추가 (`config/_default/markup.toml`) — 코드 하이라이트(monokai), 줄 번호, Goldmark passthrough 수식 구분자 설정

## 0.2.6 - 2026-03-24

### 수정됨 0.2.6

- 하드코딩된 절대 경로(`/ko/`, `/en/` 등)를 Hugo `relLangURL` / `relURL` 함수로 교체 — 서브디렉토리 배포 및 비표준 base URL 환경 지원
  - `nav.html`: 로고 링크, 로고 이미지
  - `footer.html`: 강의·블로그·소개·태그·로고 링크 및 이미지
  - `breadcrumbs.html`: 홈 링크
  - `404.html`: 홈 버튼 링크
  - `baseof.html`: favicon, apple-touch-icon 경로

## 0.2.5 - 2026-03-24

### 개선됨 0.2.5

- 네비게이션 로고 텍스트 자간 조정 (`letter-spacing: -0.02em`)

## 0.2.4 - 2026-03-24

### 제거됨 0.2.4

- `static/` 디렉토리의 불필요한 파일 제거 — 404 리다이렉트 HTML, favicon 파일들, Android/iOS 아이콘, `site.webmanifest` (Hugo 빌드 산출물로 대체)

## 0.2.3 - 2026-03-23

### 변경됨 0.2.3

- 폰트 스택 변경 — 헤딩/본문 모두 `AstaSans`를 우선 적용하고 `Pretendard`를 fallback으로 조정
- 네비게이션 로고 텍스트 font-weight `700` → `800`으로 강화

## 0.2.2 - 2026-03-23

### 수정됨 0.2.2

- favicon 링크 정리 — `favicon-16x16.png` 중복 링크 제거, `logo.png`를 favicon으로 사용하도록 통합

## 0.2.1 - 2026-03-23

### 수정됨 0.2.1

- 홈 화면 프로필 이미지 로드 방식 수정 — `absURL` 대신 `resources.Get`으로 Hugo asset pipeline을 통해 이미지 처리 (자산 경로 오류 방지)

## 0.2.0 - 2026-03-23

### 추가됨 0.2.0

- **독립 커스텀 테마로 전환** — Congo 등 외부 테마 의존성 완전 제거
- 단일 CSS 파일 (`assets/css/main.css`) — CSS custom properties, 자동 다크모드 지원
- 폰트: AstaSans (헤딩) + Pretendard (본문), CDN 로드
- 아이콘: Tabler Icons CDN
- 네비게이션: 고정 blur 네비바 + 모바일 햄버거 메뉴 + 언어 전환
- `layouts/_default/baseof.html` — 기본 HTML 구조 (CSS pipeline, meta, nav, footer)
- `layouts/_default/list.html` — 기본 목록 레이아웃
- `layouts/index.html` — 홈페이지 (프로필, 최근 글)
- `layouts/partials/nav.html` — 네비게이션 바
- `layouts/partials/footer.html` — 푸터
- `layouts/partials/breadcrumbs.html` — 브레드크럼
- `layouts/partials/pagination.html` — 페이지네이션
- `layouts/shortcodes/lead.html` — 강조 문단 숏코드
- `layouts/shortcodes/mermaid.html` — Mermaid 다이어그램 숏코드
- i18n 날짜 포맷 헬퍼 (`layouts/partials/functions/date.html`)

### 변경됨 0.2.0

- 기존 `layouts/_partials/` 구조를 Hugo 표준 `layouts/partials/`로 마이그레이션
- 코스/블로그/소개 레이아웃 전면 재작성 (독립 테마 기준)

## 0.1.3 - 2026-01-03

### 추가됨 0.1.3

- `reflangtitle` 인라인 숏코드 추가 — 다국어 페이지 간 참조 링크 지원 (`layouts/shortcodes/reflangtitle.inline.html`)

## 0.1.2 - 2026-01-02

### 변경됨 0.1.2

- 강의 목록 정렬 순서 변경 — 최신 글이 목록 상단에 오도록 article 정렬 기준 수정

## 0.1.1 - 2025-12-31

### 개선됨 0.1.1

- 스크롤바 스타일 개선 — 커스텀 스크롤바 CSS 추가 (webkit 기반)

## 0.1.0 - 2025-12-07

### 추가됨 0.1.0

- **초기 레이아웃 모듈 공개** — Hugo Module로 제공되는 공유 레이아웃 시스템
- `layouts/_default/single.html` — 글/강의 상세 (TOC, breadcrumbs, 메타)
- `layouts/_default/term.html` — 태그/카테고리 term 페이지
- `layouts/courses/list.html` — 강의 목록 (카테고리 필터, 정렬)
- `layouts/blog/list.html` — 블로그 목록 (사이드바, 페이지네이션)
- `layouts/about/list.html` — 소개 페이지 (프로필 카드)
- `layouts/taxonomy.html` — 택소노미 그리드
- `layouts/shortcodes/bookmark.html` — 북마크 카드 숏코드
- CSS 컴포넌트 분리: article-card, course-card, bookmark, tag-card, common-card, about-profile-card
- 배너 이미지 에셋 (banner1~10)
- Pretendard / MaruBuri 웹폰트 로컬 제공
- `go.mod` Hugo Module 설정 (`github.com/CodeCompose7/cc-layouts`)
