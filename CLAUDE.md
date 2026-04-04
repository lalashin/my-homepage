# CLAUDE.md

이 파일은 이 저장소에서 Claude Code(claude.ai/code)가 작업할 때 따를 지침을 제공합니다.

## 프로젝트 개요

**유형**: 정적 개인 포트폴리오 웹사이트  
**기술 스택**: HTML5, CSS3, Vanilla JavaScript (빌드 프로세스 없음)  
**목적**: 접근성과 깔끔한 코드에 중점을 두는 프론트엔드 개발자 포트폴리오

## 개발 환경 설정

빌드 도구나 의존성이 필요 없습니다. `index.html`을 브라우저에서 열어 미리보기할 수 있습니다.

### 로컬 개발
```bash
# 브라우저에서 보기 (live-server 또는 유사한 HTTP 서버 권장)
# Google Fonts CORS 문제를 피하기 위해 file:// 프로토콜 피하기
python -m http.server 8000  # 또는: npx serve
# 그 후 http://localhost:8000 열기
```

## 절대 수정 금지 사항
- `style.css`의 `:root`에 정의된 컬러 변수 이름은 유지할 것 (값 수정은 가능하나 변수명 변경 금지)
- HTML의 `.skip-link` 구조와 관련 스타일은 접근성을 위해 절대 삭제하거나 수정하지 말 것

## 아키텍처 & 핵심 패턴

### CSS 시스템
- **CSS 변수로 테마 관리** (`style.css` 1-24줄):
  - 색상 팔레트: coral (주요색), cream/blush (배경), 텍스트 음영
  - 그림자: `--shadow-sm`, `--shadow-md`, `--shadow-lg` (깊이 표현)
  - 간격: `--max-width: 720px` (컨테이너 제한), `--header-h: 68px` (고정 헤더 높이)
  - 테두리 반경: `--radius` (22px), `--radius-sm` (16px), `--radius-pill` (999px)
- **CSS 프레임워크 없음** — Grid와 Flexbox 직접 사용
- **반응형 중단점**: 640px (햄버거 메뉴), 600px (관심사 그리드 열), 768px (히어로 레이아웃)

### HTML 구조
- **시맨틱 HTML** (적절한 제목 계층 구조 및 ARIA 레이블 포함)
- **접근성 기능**:
  - 스킵 링크 (`.skip-link`) — 키보드 네비게이션용
  - 네비게이션 토글 버튼의 `aria-expanded`
  - 네비게이션 영역의 `aria-label`
  - 장식용 요소의 `aria-hidden="true"`
  - 랜드마크 영역: `<header>`, `<main>`, `<footer>`, `<section>`

### JavaScript (Vanilla, 프레임워크 없음)
- **IIFE 패턴** (`script.js`): 모든 코드를 자체 실행 함수로 감싸 캡슐화
- **네비게이션 토글**: 클래스 토글(`is-open`)과 aria-expanded 상태 관리
- **자동 생성된 푸터 연도**: 매년 `#year` 요소 업데이트
- **이벤트 위임**: 네비게이션 링크 클릭 시 메뉴 닫기; 프레임워크 없이 동적 상호작용 처리

## 파일 구조

| 파일 | 목적 |
|------|------|
| `index.html` | 히어로, 소개, 관심사, 연락처 섹션이 있는 메인 포트폴리오 페이지 |
| `index1.html` | 추가 페이지 (목적 미문서화) |
| `style.css` | 모든 스타일; CSS 변수로 테마 정의, 외부 CSS 라이브러리 없음 |
| `script.js` | 네비게이션 상호작용 및 푸터 연도 업데이트 |

## 자주 하는 작업

### 새 섹션 추가
1. `index.html`에 섹션 ID를 포함한 HTML 구조 추가
2. 기존 유틸리티 클래스 사용: `.section`, `.container`, `.section-title`
3. 기존 섹션의 색상/그림자 패턴 반영 (CSS 변수 `--shadow-md`, `--coral` 사용)

### 색 구성 업데이트
1. `style.css` 1-24줄 (`:root`)의 CSS 변수 수정
2. 변수 이름 패턴: `--{hue}-{shade}` 또는 `--{semanticname}`
3. 모든 색상은 CSS 변수에서 파생 — 다른 곳에 하드코드된 색상 없음

### 모바일 경험 개선
1. 미디어 쿼리에서 반응형 중단점 확인 (`@media max-width: 640px`, `@media min-width: 768px`)
2. 모바일 우선 접근법: 기본 스타일은 모바일용; 중단점이 큰 화면 레이아웃 확장

### 접근성 감시
- 모든 링크가 설명하는 텍스트 포함 ("여기 클릭" 같은 표현 금지)
- 제목 순서(h1 → h2 → h3) 논리적 확인
- 모든 인터랙티브 요소(버튼, 네비게이션)가 올바른 ARIA 속성 확인
- 키보드 네비게이션(Tab, Shift+Tab, Enter) 테스트

## 향후 개발 주의사항

- **상태 관리 불필요**: 현재 Vanilla JS는 네비게이션 토글에 충분
- **전처리기 없음**: 순수 CSS; 복잡도가 증가하면 CSS Modules 등 고려
- **성능 우수**: 단일 스타일시트, 최소한의 JS, Google Fonts만 외부 의존성
- **연락처 정보는 플레이스홀더**: `hello@example.com`과 `github.com/username`은 실제 값으로 업데이트 필요
- `index1.html` 파일이 있지만 링크되거나 문서화되지 않음 — 변경 전에 목적 명확히 할 것

## 개발 규칙

### 필수 규칙
1. **모든 주석은 한국어로 작성** — HTML, CSS, JavaScript 모든 주석은 한국어 사용
2. **외부 CSS 라이브러리 금지** — Bootstrap, Tailwind, Bulma 등 CSS 프레임워크 사용 금지
   - 필요한 모든 스타일은 `style.css`의 CSS 변수와 순수 CSS로만 구현
3. **한국어로 대화** — Claude Code와 소통할 때 한국어 사용

### Git 커밋 규칙
- **형식**: `type: description` (예: `feat: 소개 섹션 애니메이션 추가`)
- **타입**: feat(기능), fix(버그), style(디자인), docs(문서), chore(설정)