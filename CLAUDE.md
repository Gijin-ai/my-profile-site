# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 프로젝트 개요

Gijin Kim의 개인 영문 포트폴리오 사이트. 빌드 시스템 없이 `index.html` 단일 파일로 구성된 정적 사이트.

## 실행 방법

빌드/컴파일 단계 없음. 브라우저에서 `index.html`을 직접 열거나, VS Code Live Server 확장으로 로컬 서버 실행.

## 아키텍처

`index.html` 한 파일에 HTML, CSS, JS가 모두 포함됨:

- **`<style>`**: CSS 커스텀 프로퍼티(`:root` 변수), 섹션별 스타일 순서대로 정의
- **`<body>`**: 섹션 순서 — `#hero` → `#about` → `#experience` → `#education` → `#certifications` → `#awards` → `#skills` → `#personality` → `#contact`
- **`<script>`**: 파일 하단에 위치, EmailJS 설정 → 폼 이벤트 → 버거 메뉴 → 스크롤 fade-in → 활성 nav 링크 추적

## 외부 의존성 (CDN)

| 라이브러리 | 용도 |
|-----------|------|
| Google Fonts (Inter, JetBrains Mono) | 본문/코드 폰트 |
| Font Awesome 6.5 | 아이콘 |
| EmailJS Browser SDK v4 | 연락처 폼 이메일 전송 |

## EmailJS 설정

연락처 폼은 EmailJS를 사용. 키 값은 `index.html` 하단 `<script>` 블록에 직접 정의:

```js
const EMAILJS_PUBLIC_KEY  = '...';  // Account > Public Key
const EMAILJS_SERVICE_ID  = '...';  // Email Services > Service ID
const EMAILJS_TEMPLATE_ID = '...';  // Email Templates > Template ID
```

템플릿 변수: `{{subject}}`, `{{from_email}}`, `{{phone}}`, `{{message}}`

## CSS 규칙

- 색상은 반드시 `:root` 변수 사용 (`--blue`, `--red`, `--green` 등)
- 스크롤 fade-in 대상 요소에 `.fi` 클래스 적용 (JS의 IntersectionObserver가 `.vis` 추가)
- 반응형 분기점: `@media (max-width: 768px)` — 모바일 nav, 그리드 1열 전환
