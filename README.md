# CodeCompose Hugo Shared Layouts (모듈 안내)

이 파일은 `layouts/`(필요 시 `assets/`, `static/`)를 별도 Hugo Module로 분리해 다른 사이트에서 재사용하는 방법을 요약합니다. 이 저장소는 공용 레이아웃/자산만 포함하고, 각 사이트의 콘텐츠와 설정은 해당 사이트에서 관리합니다.

## 필수 요구사항
- Hugo extended (v0.152+ 권장)
- Go 모듈 활성화 환경

## 모듈 레포 준비(공통 레포에서)
1) 새 폴더에서 초기화:
   ```bash
   hugo mod init github.com/you/cc-layouts
   ```
2) 공용 `layouts/`를 복사하고, 필요하면 공용 `assets/`, `static/`도 복사.
3) 선택: `hugo mod tidy` 실행.
4) Git 커밋 후 원격에 푸시.

## 사이트에서 사용하기
1) 사이트 루트에서(없다면) 모듈 초기화:
   ```bash
   hugo mod init github.com/you/your-site
   ```
2) `hugo.toml`에 모듈 import 추가(커스텀 → 테마 순서 권장):
   ```toml
   [module]
     [[module.imports]]
       path = "github.com/you/cc-layouts"   # 공통 레이아웃 모듈
     [[module.imports]]
       path = "github.com/jpanther/congo"   # 테마
   ```
   우선순위: import 목록 아래로 갈수록 덮어쓰기가 약합니다. 커스텀을 위에 두면 congo 위에 오버레이됩니다. 로컬 파일은 항상 최우선.

3) 필요한 모듈 가져오기:
   ```bash
   hugo mod get github.com/you/cc-layouts
   hugo mod get github.com/jpanther/congo
   hugo mod tidy
   ```

## 설정 키(사이트 쪽에서 맞춰야 하는 값)
- 섹션 슬러그:
  - `params.sections.blog` (예: `"blog"`) — 섹션 폴더명을 바꾸면 여기 값을 맞춥니다.
- 홈 최근 글:
  - `params.homepage.showRecentFolders = ["blog", "courses"]` — 표시할 섹션 배열. 비어 있으면 최근 글 블록 미표시.
  - `params.homepage.recentLimit` — 최대 표시 개수.
- 섹션 front matter(`content/<section>/_index.*`):
  - `sectionKey`: 섹션 루트 슬러그(언어별 경로 찾기에 사용).
  - `categorySection`: 카테고리 필터/term이 참조할 섹션. 보통 `sectionKey`와 동일.
  - `sidebarDefaults`: 사이드바 기본 이미지/텍스트.
- 카테고리 필터/term:
  - 위 `sectionKey`/`categorySection` 없으면 `Site.Params.sections.default` → 기본 `"blog"` 순으로 추론합니다.

## 자산(assets/static) 병합 규칙
- Hugo Modules는 `layouts/assets/static`를 병합합니다. 우선순위: 로컬 > import 순서 아래쪽.
- 충돌을 피하려면 모듈 자산을 네임스페이스 경로(`assets/cc/...`, `static/cc/...`)로 두고, 사이트 고유 자산은 로컬에 배치하세요.
- 필요하면 `module.mounts`로 선택적 마운트 가능:
  ```toml
  [[module.mounts]]
    source = "assets"
    target = "assets/cc"
  [[module.mounts]]
    source = "layouts"
    target = "layouts"
  ```

## 테스트
```bash
hugo server -D
```
오류 시 섹션 슬러그(`params.sections.*`), `showRecentFolders`, 섹션 `_index.*`의 `sectionKey`/`categorySection`을 우선 확인하세요.

## 변경 요약(이 모듈이 제공하는 주요 기능)
- 섹션/카테고리 필터가 하드코딩된 섹션명 대신 설정/프론트매터로 동작
- 홈 “최근 글” 섹션을 `showRecentFolders` 배열로 제어
- 사이드바 기본값을 섹션/페이지 파라미터에서 우선 읽도록 개선

