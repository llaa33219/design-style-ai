# BLP CLI Design Language Specification
## 버전 1.0.0 | 2026-05-13

> **핵심 철학**: 난해함(Obscurity), 몽환적(Dreamlike), 유동성(Fluidity)  
> **정체성**: 디자인 중심 CLI. 텍스트만이 아닌 아스키 아트, 블록 유니코드, 캐릭터 애니메이션으로 시각적 충격을 만드는 터미널 중심 디자인 언어.

---

## 1. 철학 및 정체성

BLP CLI는 "터미널의 한계를 디자인으로 돌파한다"는 전제로 시작한다. 단순히 정보를 나열하는 CLI가 아니라, **복합적 미학**과 **몽환적인 깊이감**, **유동적인 변화**를 텍스트 캔버스 위에 구현한다.

- **난해함**: **다양한 특징들의 혼합된 공존**. 단일한 스타일이 아닌, 복수의 시각적 언어(고전적 Box Drawing, 고밀도 Braille, Nerd Font 심볼, ASCII 아트, Truecolor 블록)가 동일 공간 내에서 조화롭게 공존. 각 요소는 자신의 규칙을 유지하며 동시에 전체 맥락을 구성. "개판"이 아닌 **통제된 복합성(Controlled Complexity)**.
- **몽환적**: `#000309`의 심해 같은 배경 위 `#2fc2ff`의 유령 같은 액센트. 현실과 비현실의 경계에 서 있는 인터페이스. 명확한 구분선이 모호해지는 지점의 미학.
- **유동성**: 상태 변화가 캐릭터 단위로 흐른다. 애니메이션은 프레임이 아닌 **글자**를 통해 전개. 고정된 형태에서 새로운 형태로의 변형이 자연스럽게 녹아든다.

---

## 2. 색상 시스템 (Color System)

### 2.1 기반 팔레트 (Base Palette)

| 토큰 | Hex | 용도 |
|------|-----|------|
| `bg-primary` | `#000309` | 전역 배경, 심해 |
| `fg-primary` | `#fafcff` | 기본 텍스트, 고대비 읽기 요소 |
| `cursor` | `#fafcff` | 캐럿, 현재 위치 표시 |
| `selection` | `#0026a3` | 드래그 선택, 하이라이트 배경 |
| `accent` | `#2fc2ff` | 상호작용, 포커스, 브랜드 아이덴티티 |

### 2.2 ANSI 색상 (16 Colors)

```json
{
  "black": "#000309",        "bright_black": "#1e2b3d",
  "red": "#ff7f7f",          "bright_red": "#ffdbdb",
  "green": "#6bd67b",        "bright_green": "#ccffd4",
  "yellow": "#ffeb7f",       "bright_yellow": "#fff9bd",
  "blue": "#7f9bff",         "bright_blue": "#dbe3ff",
  "magenta": "#d67fff",      "bright_magenta": "#f4dbff",
  "cyan": "#7fbcff",         "bright_cyan": "#dbedff",
  "white": "#f7eaff",        "bright_white": "#ffffff"
}
```

### 2.3 시맨틱 토큰 (Semantic Tokens)

| 토큰 | Hex | 설명 |
|------|-----|------|
| `surface-00` | `#000309` | 최하위 배경 (바닥) |
| `surface-01` | `#1e2b3d` | 상위 표면 (패널, 카드), `bright_black` |
| `surface-02` | `#0a1628` | 중간 표면 (호버, 활성 탭 배경) |
| `surface-danger` | `#ff7f7f` | 오류, 삭제, 경고 |
| `surface-success` | `#6bd67b` | 성공, 완료, 실행 |
| `surface-warn` | `#ffeb7f` | 주의, 대기 |
| `surface-info` | `#7f9bff` | 정보, 링크 |
| `surface-danger-tint` | `#ff7f7f` 10% | 오류 상태 배경 틴트 |
| `surface-warn-tint` | `#ffeb7f` 10% | 경고 상태 배경 틴트 |
| `surface-success-tint` | `#6bd67b` 10% | 성공 상태 배경 틴트 |
| `dimmed` | `#1e2b3d` | 비활성, 비활성화, 힌트 텍스트 |
| `border` | `#1e2b3d` | 구분선 (보조, 2차) |
| `border-focus` | `#2fc2ff` | 포커스 테두리 |
| `border-error` | `#ff7f7f` | 유효성 오류 테두리 |

> **라이트 모드**: 현재 스펙에서는 정의하지 않으며, v1.1 이후 `surface` 계열 반전으로 대응 예정.

---

## 3. 타이포그래피 (Typography)

### 3.1 기본 서체: Goorm Sans Code

**코딩/CLI 환경 최적화 한글 모노스페이스 서체.** 한글과 영문의 자폭이 코드 내에서 일관되게 적용되어 효과적인 시각적 구분을 제공한다.

#### @font-face 추출 정보

```css
@font-face {
  font-family: 'Goorm Sans Code';
  src: url('https://statics.goorm.io/fonts/GoormSansCode/v1.0.1/goorm-sans-code.eot');
  src: url('https://statics.goorm.io/fonts/GoormSansCode/v1.0.1/goorm-sans-code.eot?#iefix') format('embedded-opentype'),
       url('https://statics.goorm.io/fonts/GoormSansCode/v1.0.1/goorm-sans-code.woff2') format('woff2'),
       url('https://statics.goorm.io/fonts/GoormSansCode/v1.0.1/goorm-sans-code.woff') format('woff'),
       url('https://statics.goorm.io/fonts/GoormSansCode/v1.0.1/goorm-sans-code.svg#GoormSans') format('svg');
  font-style: normal;
  font-display: swap;
}
```

| 속성 | 값 |
|------|-----|
| **Font Family** | `Goorm Sans Code` |
| **Version** | v1.0.1 |
| **License** | SIL Open Font License |
| **Weight** | Regular (400) only — 코딩용 단일 웨이트 |
| **Style** | Normal (Italic 미지원) |
| **Features** | 한글/영문/숫자/특수문자 전체 지원, 일관된 CJK/Latin 폭 |
| **CDN CSS** | `https://statics.goorm.io/fonts/GoormSansCode/v1.0.1/GoormSansCode.min.css` |
| **Formats** | EOT, WOFF2, WOFF, SVG |
| **Nerd Font** | `GoormSansCodeNerdFont` (NerdFont 3.2.1 패치 버전 존재) |

### 3.2 서체 계층 (Type Scale)

터미널/CLI에서는 물리적 픽셀 크기보다 **셀 단위 배수**와 **스타일 속성**으로 계층을 구분한다.

| 토큰 | 셀 높이 배수 | 속성 | 용도 |
|------|-------------|------|------|
| `text-xs` | 0.75 | dimmed | 타임스탬프, 메타정보 |
| `text-sm` | 0.875 | normal | 보조 설명, 힌트 |
| `text-base` | 1 | normal | 본문, 리스트, 입력값 |
| `text-lg` | 1.25 | bold | 섹션 제목, 강조 |
| `text-xl` | 1.5 | bold+accent | 대시보드 수치, 헤더 |
| `text-2xl` | 2 | bold+accent+uppercase | ASCII 아트 타이틀, 스플래시 |

> **굵기 처리**: Goorm Sans Code는 400 단일 웨이트이므로, 터미널에서는 **Reverse Video** 또는 **Bright Color**로 굵기를 대체 표현한다. Web 환경에서는 `font-weight: 400` 고정 + `text-shadow` 또는 `color` 변환으로 시뮬레이션.

### 3.3 줄 간격 및 패딩

- **행 간격(Line Height)**: 셀 단위 고정 `1.2` (1행당 1.2셀 높이). 터미널에서는 기본적으로 `1`을 권장하나, BLP CLI에서는 정보 밀도와 호흡을 위해 `1.2` 허용.
- **패딩**: 셀 단위 `ch`/`em` 기준. 내부 여백은 최소 `0.5ch` ~ `1ch`.

---

## 4. 레이아웃 및 그리드

### 4.1 셀 기반 반응형 그리드

- **기준 단위**: 1셀 = 1문자 폭 × 1문자 높이. 모든 크기는 `ch` / `em` 단위로 환산 가능해야 함.
- **반응형**: 터미널 창 크기(열×행) 변화에 따라 패널 너비/높이가 셀 단위로 재조정. 최소 보장 영역은 `80×24` (클래식 터미널).
- **정렬**: 좌측 기반. BLP CLI는 다양한 시각적 요소의 공존을 전제로 하므로, 중앙 정렬은 특정 요소(ASCII 타이틀, 모달)에만 제한적으로 사용. 각 요소는 자신의 정렬 규칙을 가지며, 이것이 공간 내에서 복합적으로 중첩된다. |

### 4.2 테두리 (Border) — 보조 구분 수단

BLP CLI는 **배경색(`surface`)을 통한 구분을 1차**, 테두리를 **2차(보조)** 구분 수단으로 사용한다. 테두리는 공간의 경계를 암시하는 "희미한 선"이지, 강한 구분선이 아니다.

- **스타일**: 굵게(Heavy), 직각(Radius 0). 라운드는 존재하지 않음.
- **Unicode Box Drawing**: `┏━┓`, `┃`, `┗━┛` (U+250F ~ U+251B, Heavy Box Drawing) 사용.
- **Fallback**: ASCII `+--+, |` (Web/TUI 모두 대응).
- **색상**: 기본 `border` (`#1e2b3d`) — 거의 배경과 유사하여 눈에 띄지 않음. 포커스/액티브 시에만 `border-focus` (`#2fc2ff`)로 미세하게 강조.
- **권장**: 패널 간 구분은 `surface-01`(`#1e2b3d`) 또는 `surface-02`(`#0a1628`) 배경색 차이로 처리. 테두리는 최소한으로만 사용.
- **구현 가이드**: 
  - 기본 상태: 테두리 색상을 `border`(`#1e2b3d`)로 설정하여 배경(`surface-00`)과 거의 구분되지 않게 처리.
  - 포커스 상태: `border-focus`(`#2fc2ff`)로 1픽셀 heavy line만 추가.

---

## 5. 컴포넌트 프리미티브

### 5.1 공통 상태 정의

| 상태 | 전략 | 설명 |
|------|------|------|
| **Default** | `fg-primary` on `surface-00` | 기본 |
| **Hover** | `accent` 색상으로 전환 또는 `surface-02` 배경 전환 | 마우스/키보스트 커서 오버 |
| **Focus** | `surface-02` 배경 전환 + `accent` 텍스트 + 미세 `border-focus` 테두리 | 현재 상호작용 대상 |
| **Active** | `surface-02` 배경 + `bright_white` 텍스트 | 눌림/선택 완료 |
| **Disabled** | `dimmed` 색상 + strikethrough 또는 흐림 처리 | 비활성 |
| **Dimmed** | `bright_black` (`#1e2b3d`) 전체 적용 | 배경화면, 비활성 패널 |

### 5.2 핵심 컴포넌트 목록

#### Button
- **기본**: `surface-01` 배경, `fg-primary` 텍스트.
- **호버**: `surface-02` 배경 + `accent` 텍스트.
- **포커스**: `surface-02` 배경 + `accent` 텍스트 + 미세 `border-focus`(`#2fc2ff`) 테두리.
- **구분 전략**: 배경색(`surface-01` → `surface-02`) 전환이 1차. 테두리는 포커스 상태에서만 보조적으로 1px heavy line으로 표현.

#### Input
- **구분 전략**: 입력 영역은 `surface-01` 배경으로 표시. 테두리 없음.
- **프롬프트 기호**: `▶` (`accent` 색) 표준.
- **커서**: Block 스타일 또는 밑줄, `cursor` 색상.
- **텍스트**: 입력값은 `fg-primary`, 힌트는 `dimmed`.

#### Select / Dropdown
- **구분 전략**: 테두리 없이 선택된 항목만 `surface-02` 배경 + `accent` 텍스트. 드롭다운 영역 전체는 `surface-01` 배경으로 공간 분리.
- **선택 항목**: `accent` 텍스트 + `surface-02` 배경.
- **비선택**: `dimmed` 텍스트.
- **호버**: `surface-01` 배경 전환.

#### Table
- **구분 전략**: 테두리 없이 **배경색**과 **밑줄**로 구분. 헤더는 `accent` 밑줄(`─`)로 분리.
- **정렬**: 숫자 우측, 문자열 좌측.
- **행 호버**: 전체 행 `surface-02` 배경 전환.
- **포커스**: 선택된 행에만 미세 `border-focus` 좌측 세로바 추가.
- **헤더**: `text-lg` + `accent` 밑줄.

#### Tree
```
▶ 📁 project
  ▶ 📁 src
    ├─ ○ main.py
    └─ ○ config.json
```
- Nerd Font 아이콘 사용 (`nf-fa-folder`, `nf-fa-file` 등).
- 브랜치: `├─`, `└─`, `│` (Light Box Drawing, 정보 밀도 높을 때).

#### Tab
- **구분 전략**: 탭은 `│` 문자로 미세 구분. 액티브 탭은 `surface-02` 배경 + `accent` 텍스트 + 하단 밑줄.
- **인액티브**: `dimmed` 텍스트.
- **콘텐츠 영역**: `surface-01` 배경으로 공간 분리. 테두리는 최소화.

#### Progress Bar
- **구분 전략**: 테두리 없이 `surface-02` 배경 영역 내에서 블록으로 표현.
- **블록 문자**: `█`, `▓`, `▒`, `░` (Block Elements, U+2580~U+259F).
- **채움 색상**: `accent`. 빈칸: `dimmed`.
- **애니메이션**: `Block Fill` — 블록이 좌→우로 캐릭터 단위 채워짐.

#### Modal / Overlay
- **본체**: `surface-02` (`#0a1628`) 배경으로 공간 분리. 테두리는 `surface-01`(`#1e2b3d`) 수준의 희미한 선만 사용.
- **헤더**: `bright_yellow` + Nerd Font 아이콘 (`nf-fa-warning`).
- **포커스**: 버튼/요소에만 `border-focus`(`#2fc2ff`)를 미세하게 적용.
- **뒷 배경**: 원본 화면을 `dimmed`(`#1e2b3d`) 처리하여 깊이감 생성.

#### Toast / Notification
- **구분 전략**: 테두리 없이 `surface-01` 배경 + 좌측 `accent` 세로바(`▌`)로 공간 분리.
- **위치**: 우측 상단 또는 하단 고정.
- **아이콘**: Nerd Font 상태 아이콘 (`nf-fa-check` 등).
- **자동 소멸**: 캐릭터 단위 페이드아웃 (`Fade Char` 애니메이션).

#### Log Viewer
- **구분 전략**: 테두리 없이 행 단위 배경색 틴트로 로그 레벨 구분.
- **타임스탬프**: `text-xs` + `dimmed`.
- **로그 레벨 아이콘**: Nerd Font (`nf-fa-check`, `nf-fa-warning`, `nf-fa-bolt`).
- **색상**: 
  - Info: `cyan`
  - Warn: `yellow` + `surface-warn-tint`
  - Error: `red` + `surface-danger-tint`
  - Success: `green` + `surface-success-tint`

---

## 6. 모션 및 애니메이션

### 6.1 원칙: CLI 정체성 유지

BLP CLI의 애니메이션은 **프레임 기반 그래픽이 아닌 캐릭터(글자) 기반**으로 전개된다. 모든 모션은 다음 제약 내에서 구현한다:

- **단위**: 개별 문자, 문자열 블록, 라인.
- **금지**: CSS `transform`, `opacity`를 통한 블러/스케일 (Web에서조차). 대신 **색상 전환**, **Reverse Video**, **블록 문자 교체**로 표현.
- **OLED 친화**: `#000309` 배경에서 깜빡임 최소화. 애니메이션은 어둠 속에서 빛나는 형태로.

### 6.2 애니메이션 카탈로그

| 이름 | 기법 | 설명 |
|------|------|------|
| **Type Reveal** | 문자 순차 출력 | `setInterval` / `asyncio.sleep`로 15~30ms 간격 문자 출력. 타이핑 소리 대신 커서 깜빡임.
| **Scanline** | 라인 단위 Reverse Video 스캔 | 포커스 이동 시 라인 전체가 한 번씩 Reverse Video로 번쩍이며 지나감. "몽환적" 효과.
| **Glitch** | 문자 교체 + 색상 왜곡 | 잠시동안 랜덤 문자(`!@#$%`)가 나타났다가 원문 복구. 난해함 철학의 핵심. 빈도는 절제.
| **Block Fill** | 블록 문자 누적 | 프로그레스 바, 차트. `░` → `▒` → `▓` → `█` 순서로 단계적 채움.
| **Fade Char** | Bright → Normal → Dimmed | 문자의 색상 단계를 `bright_*` → `fg-primary` → `dimmed`로 전환하여 "흐려짐" 표현.
| **Panel Draw** | 테두리 라인 순차 생성 | `┏` → `━` → `┓` → `┃` → ... 순서로 테두리를 그려나가며 등장.
| **ASCII Morph** | 아스키 아트 프레임 교체 | 3~5 프레임의 아스키 아트를 교체하여 간단한 "이미지" 애니메이션. 예: 회전하는 큐브.
| **Pulse** | Accent 색상 토글 | `accent` ↔ `bright_cyan` 또는 `accent` ↔ `white`를 500ms 간격으로 교체. 상태 표시등.

### 6.3 타이밍 가이드

| 상황 | 지연/속도 |
|------|----------|
| 문자 출력 (Type Reveal) | 15~40ms/char |
| 스캔라인 | 50ms/line |
| 패널 드로잉 | 10ms/char (배경색 채움 우선) |
| 펄스 | 500ms~1000ms 주기 |
| ~~글리치~~ | ~~사용 금지~~ |

---

## 7. 아이콘 및 심볼 시스템

### 7.1 이모지 금지 정책 (Strict No-Emoji)

- **금지 범위**: Unicode Emoji Range (U+1F300 ~ U+1FAD6, U+2600 ~ U+26FF 등) **전면 사용 금지**.
- **대안**: Nerd Font Private Use Area (PUA) + Box Drawing + 기호 문자.
- **이유**: 이모지는 플랫폼/터미널마다 렌더링이 제각각이며, BLP CLI가 추구하는 **통제된 복합성**을 해친다. 이모지는 규격화된 감정 기호일 뿐, 다층적 시각 언어의 공존이 아니다.

### 7.2 Nerd Font 사용 가이드

Goorm Sans Code에 NerdFont 3.2.1을 패치한 `GoormSansCodeNerdFont`를 기본으로 사용한다.

| 카테고리 | 접두사 | 예시 | 용도 |
|----------|--------|------|------|
| 파일/폴더 | `nf-fa-` / `nf-dev-` | `\uf07b` (folder), `\uf15b` (file) | 트리, 파일 매니저 |
| 상태 | `nf-fa-` | `\uf00c` (check), `\uf071` (warning) | 알림, 검증 |
| 하드웨어 | `nf-fa-` / `nf-oct-` | `\uf2db` (microchip), `\uf0a0` (hdd) | 시스템 모니터링 |
| UI | `nf-fa-` | `\uf054` (chevron-right), `\uf0d7` (caret-down) | 네비게이션 |
| 사용자 | `nf-fa-` | `\uf007` (user), `\uf233` (server) | 대시보드 |

> **Web 환경**: Nerd Font 웹폰트를 별도 로드. TUI 환경: 터미널이 Nerd Font를 렌더링할 수 있어야 함.

### 7.3 순수 Unicode 기호 (Nerd Font 미지원 환경 Fallback)

| 의미 | 문자 | Unicode |
|------|------|---------|
| 화살표/포인터 | `▶`, `◀`, `▼`, `▲` | U+25B6, U+25C0, U+25BC, U+25B2 |
| 체크/엑스 | `✓`, `✗` | U+2713, U+2717 |
| 경고 | `⚠`, `‼` | U+26A0, U+203C |
| 구분/장식 | `❯`, `❮`, `│`, `─` | U+276F, U+276E, U+2502, U+2500 |
| 블록 | `█`, `▓`, `▒`, `░` | U+2588~U+2591 |
| 원/도형 | `●`, `○`, `◐`, `◑` | U+25CF, U+25CB, U+25D0, U+25D1 |

---

## 8. 데이터 시각화

### 8.1 블록 기반 차트

블록 유니코드(`▄▅▆▇█`)와 박스 드로잉으로 모든 차트를 구성한다.

#### Bar Chart (Vertical)
- **구성**: Y축 눈금(`┤`, `┼`) + `█` 블록 바 + X축 레이블.
- **블록**: `█`(`accent`)로 값 표현, 빈 공간은 `░`(`dimmed`).
- **레이아웃**: 좌측에 `text-xs` 눈금, 하단에 중앙 정렬 레이블(의도적 이상 현상으로만).

#### Sparkline
- **구성**: 레이블(`text-sm` + `dimmed`) + `▁▂▃▅▆▇█` 블록 곡선 + 주석.
- **블록**: 값에 따라 `▁`(최소) ~ `█`(최대) 매핑.
- **색상**: 기본 `accent`, 임계값 초과 시 `danger` 또는 `warn` 전환.

#### Heatmap (Cell-based)
- **구성**: 행/열 헤더(`text-xs` + `dimmed`) + `░▒▓█` 블록 셀.
- **밀도**: `░`(0%) < `▒`(33%) < `▓`(66%) < `█`(100%).
- **색상**: `dimmed` → `accent` 그라데이션 (ANSI 16색 또는 Truecolor).

### 8.2 고밀도 비주얼 시스템 (High-Density Visual System)

BLP CLI는 단순 `@#%+=-:. ` 반톤을 넘어, **점자(Braille) 패턴**과 **고밀도 블록 분할 문자**를 적극 활용하여 터미널 캐릭터 하나로 최대 8개의 픽셀 정보를 압축 표현한다. 이는 사진, 영상 프레임, 알범 아트, 텍스처를 터미널 내에서 실제로 "보여주는" 것을 가능하게 한다.

#### 8.2.1 문자셋 아키텍처 (Character Set Architecture)

계층별로 밀도와 용도를 분리하여 사용한다.

| 레벨 | 문자셋 | 유니코드 범위 | 해상도 특성 | 용도 |
|------|--------|--------------|------------|------|
| **L0** | Box Drawing | U+2500~U+257F | 선/프레임 | UI 테두리, 구분선 |
| **L1** | Block Elements | U+2580~U+259F | 1×2, 2×2 분할 | 프로그레스, 히트맵, 대략적 이미지 |
| **L1+** | Quadrants | U+2596~U+259F | 2×2 쿼드 | 4색 인접 셀 표현, 아이콘 |
| **L2** | **Braille Patterns** | **U+2800~U+28FF** | **2×4 도트 매트릭스** | **사진/영상/고밀도 아트** |
| **L3** | Legacy Computing | U+1FB00~U+1FBFF | 1×2~2×3 고급 분할 | 최신 터미널 전용 고해상도 |

> **L2 Braille이 핵심이다.** 나머지는 보조.

#### 8.2.2 브레일(점자) 패턴 상세 사양

**Unicode**: `U+2800` ~ `U+28FF` (256자, 공백 포함)  
**매트릭스**: 2열(가로) × 4행(세로) 도트. 캐릭터 하나로 8비트 정보 표현.  
**비트 매핑 (표준 점자 규격)**:

```
비트 0 (0x01) → 좌상단 (1열 1행)
비트 1 (0x02) → 좌중상 (1열 2행)
비트 2 (0x04) → 좌중하 (1열 3행)
비트 3 (0x08) → 좌하단 (1열 4행)
비트 4 (0x10) → 우상단 (2열 1행)
비트 5 (0x20) → 우중상 (2열 2행)
비트 6 (0x40) → 우중하 (2열 3행)
비트 7 (0x80) → 우하단 (2열 4행)
```

**해상도 환산**:
- 터미널 1 셀 = Braille 1 문자 = 가로 2px × 세로 4px
- 80×24 터미널 기준: **160×96 픽셀**의 이미지를 문자 그리드 하나에 표현 가능
- 160×48 셀 터미널 기준: **320×192 픽셀** — 거의 게임보이 수준

**색상 적용 전략**:
- Braille 문자 하나는 **단색**으로만 칠해진다 (도트별 색상 구분 불가).
- 따라서 **Truecolor ANSI** (`\x1b[38;2;R;G;Bm`) 또는 **팔레트 매핑**으로 문자 단위 색상을 입혀야 한다.
- 인접한 2×2 픽셀 블록의 평균색을 해당 Braille 문자의 전경색으로 사용.
- 배경색(`bg-primary` `#000309`)은 그대로 두고, 도트(전경색)만 색상 입혀서 OLED 심해 느낌 극대화.

**Braille → 픽셀 매핑 규칙**:

| 문자 | 유니코드 | 비트 마스크 | 도트 패턴 (2×4) |
|------|----------|-------------|-----------------|
| `⣿` | U+28FF | 0xFF | 전체 ON |
| `⠃` | U+2803 | 0x03 | 좌측 상단 2×2 ON |
| `⠪` | U+282A | 0x2A | 비트 1,3,5 ON |

- 각 비트는 2열×4행 매트릭스의 특정 도트를 제어한다.
- 비트 ON = 해당 위치에 `accent` 색 도트 표시. 비트 OFF = 배경색(`surface-00`).

#### 8.2.3 보조 고밀도 문자셋 (Block & Quadrants)

**Block Elements (세로 2분할 해상도 2배)**:

| 문자 | 유니코드 | 설명 | 사용 예시 |
|------|----------|------|-----------|
| `▀` | U+2580 | Upper half block | 상단 50% 채움 |
| `▄` | U+2584 | Lower half block | 하단 50% 채움 |
| `█` | U+2588 | Full block | 100% 채움 |
| `▌` | U+258C | Left half block | 좌측 50% 채움 |
| `▐` | U+2590 | Right half block | 우측 50% 채움 |
| `▖` | U+2596 | Quadrant lower left | 2×2 좌하단 |
| `▗` | U+2597 | Quadrant lower right | 2×2 우하단 |
| `▘` | U+2598 | Quadrant upper left | 2×2 좌상단 |
| `▙` | U+2599 | 3-Quadrant fill | 좌상+좌하+우하 |
| `▚` | U+259A | 대각선 | 좌상+우하 |
| `▛` | U+259B | 3-Quadrant fill | 좌상+우상+좌하 |
| `▜` | U+259C | 3-Quadrant fill | 좌상+우상+우하 |
| `▝` | U+259D | Quadrant upper right | 2×2 우상단 |
| `▞` | U+259E | 반대각선 | 우상+좌하 |
| `▟` | U+259F | 3-Quadrant fill | 우상+좌하+우하 |

- **Quadrants 활용**: 2×2 쿼드 분할로 인접한 4개 픽셀을 하나의 문자로 표현. Braille보다 저해상도지만 **도트 간격 문제 없음**.
- **Block + Quadrant 조합**: Braille이 깨지는 터미널에서는 Quadrant + Block으로 폴백.

#### 8.2.4 이미지 → 터미널 변환 파이프라인

```
[원본 이미지]
    ↓
[1. 리사이즈] ──→ 터미널 셀 수 기준 (cols×2, rows×4) 픽셀로 다운스케일
    ↓
[2. 색상 공간 변환] ──→ sRGB → 터미널 Truecolor 또는 BLP 팔레트 매핑
    ↓
[3. 문자셋 선택]
    ├─ 고해상도: Braille (2×4)
    ├─ 중간: Quadrant + Block (2×2, 1×2)
    └─ 저해상도: Halftone (@#%+=-:. )
    ↓
[4. 문자 인코딩] ──→ 픽셀 블록 → Braille 비트 마스크 / Block 문자 매칭
    ↓
[5. ANSI 색상 입히기] ──→ \x1b[38;2;R;G;Bm + 문자 + \x1b[0m
    ↓
[6. 출력] ──→ stdout / TUI 캔버스 / Web pre 태그
```

**BLP CLI 컬러 매핑 규칙**:
- 배경은 무조건 `#000309` (검은 심해). 이미지 변환 시에도 배경색은 투명/검정 처리.
- 이미지의 어두운 영역은 `dimmed`(`#1e2b3d`) 또는 `#000309`와 블렌딩.
- 밝은 하이라이트는 `accent`(`#2fc2ff`)나 `bright_white`로 대체 가능 (의도적 색상 왜곡으로 "몽환적" 효과).

#### 8.2.5 영상(Video) 처리

- **프레임 추출**: FFmpeg로 1초당 N프레임 추출.
- **해상도 제한**: 80×24 터미널 기준 Braille = 160×96. 30fps는 무리. **10~15fps** 권장.
- **인코딩**: 각 프레임을 Braille + Truecolor 문자열로 변환 후, `\r` 또는 전체 화면 리프레시로 출력.
- **BLP 연동**: 영상 재생 중에도 테두리(`border-focus`), 로그 뷰어, 컨트롤 패널은 그대로 유지. 영상은 **패널 내부**에서 재생.
- **오디오**: 별도 처리. BLP CLI는 시각 중심이므로 오디오는 외부 플레이어에 위임.

#### 8.2.6 활용 시나리오

1. **이미지 뷰어**: `blp imgview photo.jpg` — 터미널 전체를 Braille 캔버스로 사용.
2. **웹캠 피드**: 실시간 카메라 영상을 Braille 스트리밍. 보안 모니터링, 스트리머 오버레이.
3. **앨범 아트**: 음악 플레이어 TUI에서 현재 트랙의 커버를 32×32 셀 Braille로 표시.
4. **배경 텍스처**: 대시보드 뒤편에 미세한 Braille 노이즈 패턴을 깔아 "몽환적" 깊이감 추가.
5. **맵/지형**: 게임 TUI에서 필드 지형을 Braille로 표현. 캐릭터는 `▶`, 지형은 `⠿⠶⠛` 등으로.

#### 8.2.7 주의사항 및 폴백

| 문제 | 원인 | 해결책 |
|------|------|--------|
| **Braille 간격 붕괴** | 폰트가 점자 도트 간격을 넓게 렌더링하면 "사각형"이 아닌 "점들"로 보임 | Goorm Sans Code는 모노스페이스라 양호. 문제 시 Quadrant로 폴백 |
| **색상 번짐** | 터미널이 Truecolor 미지원 | 256색 팔레트로 양자화. BLP ANSI 16색 중 가장 가까운 색 매핑 |
| **성능 저하** | Braille 160×96 = 15,360 문자에 Truecolor ANSI = 출력량 큼 | 더티 레クトangling. 변화된 문자만 재출력. 또는 Block으로 해상도 절반 |
| **세로 비율 왜곡** | 터미널 셀이 직사각형(가로:세로 ≈ 1:2) | 이미지 프리프로세싱에서 세로 2배 압축 후 Braille 매핑 |

#### 8.2.8 Python 구현 스니펫 (참고)

```python
import numpy as np
from PIL import Image

# Braille 비트 매핑: (row, col) → 비트 위치
BRAILLE_BITS = [
    (0, 0, 0x01), (1, 0, 0x02), (2, 0, 0x04), (3, 0, 0x08),
    (0, 1, 0x10), (1, 1, 0x20), (2, 1, 0x40), (3, 1, 0x80),
]
BRAILLE_OFFSET = 0x2800

def image_to_braille(path, max_cols=80, max_rows=24):
    img = Image.open(path).convert('RGB')
    # 터미널 셀 비율 보정: 셀 1개 = 가로2px, 세로4px. 터미널 셀 세로가 가로의 2배 정도 되므로
    target_w = max_cols * 2
    target_h = max_rows * 4
    img = img.resize((target_w, target_h), Image.Resampling.LANCZOS)
    arr = np.array(img)

    lines = []
    for y in range(0, target_h, 4):
        line_chars = []
        for x in range(0, target_w, 2):
            block = arr[y:y+4, x:x+2]
            if block.shape[0] < 4 or block.shape[1] < 2:
                break
            # 평균색 → Truecolor ANSI
            mean_color = block.mean(axis=(0, 1)).astype(int)
            r, g, b = mean_color

            # 그레이스케일 임계값 → Braille 비트
            gray_block = block.mean(axis=2)
            threshold = gray_block.mean()  # 또는 고정값 128

            bits = 0
            for (br, bc, bitval) in BRAILLE_BITS:
                if br < gray_block.shape[0] and bc < gray_block.shape[1]:
                    if gray_block[br, bc] < threshold:  # 어두우면 도트 ON (전경색 표시)
                        bits |= bitval

            char = chr(BRAILLE_OFFSET + bits)
            # Truecolor ANSI foreground
            ansi = f"\x1b[38;2;{r};{g};{b}m{char}\x1b[0m"
            line_chars.append(ansi)
        lines.append("".join(line_chars))
    return "\n".join(lines)
```

> 위 예시는 단순 참고용. 실제 BLP CLI 구현에서는 `threshold` 적응형 처리, 팔레트 매핑, 더티 리프레시, `surface-02` 오버레이 호환성을 추가해야 한다.

---

## 9. 크로스 플랫폼 토큰 적용

### 9.1 Web (CSS Custom Properties)

```css
:root {
  /* BLP CLI Design Tokens */
  --blp-bg-primary: #000309;
  --blp-fg-primary: #fafcff;
  --blp-accent: #2fc2ff;
  --blp-cursor: #fafcff;
  --blp-selection: #0026a3;

  --blp-surface-00: #000309;
  --blp-surface-01: #1e2b3d;
  --blp-surface-02: #0a1628;

  --blp-border: #1e2b3d;
  --blp-border-focus: #2fc2ff;
  --blp-border-error: #ff7f7f;

  --blp-dimmed: #1e2b3d;
  --blp-danger: #ff7f7f;
  --blp-success: #6bd67b;
  --blp-warn: #ffeb7f;
  --blp-info: #7f9bff;
  --blp-surface-danger-tint: rgba(255, 127, 127, 0.1);
  --blp-surface-warn-tint: rgba(255, 235, 127, 0.1);
  --blp-surface-success-tint: rgba(107, 214, 123, 0.1);

  /* Font */
  --blp-font-mono: 'Goorm Sans Code', 'GoormSansCode Nerd Font', monospace;

  /* Animation Timing */
  --blp-type-speed: 25ms;
  --blp-pulse-speed: 800ms;
}
```

### 9.2 Python TUI (Rich / Textual)

```python
# Rich Style Map
BLP_STYLES = {
    "blp.accent": "bold #2fc2ff",
    "blp.dimmed": "#1e2b3d",
    "blp.surface01": "on #1e2b3d",
    "blp.border": "#1e2b3d",
    "blp.border_focus": "#2fc2ff",
    "blp.danger": "#ff7f7f",
    "blp.success": "#6bd67b",
    "blp.warn": "#ffeb7f",
    "blp.info": "#7f9bff",
    "blp.selection": "on #0026a3 #fafcff",
}

# Textual CSS 예시
BLP_CSS = """
Screen { background: #000309; color: #fafcff; }
Button { border: heavy #1e2b3d; background: #000309; color: #fafcff; }
Button:focus { border: heavy #2fc2ff; color: #2fc2ff; }
DataTable { border: heavy #1e2b3d; }
DataTable > .datatable--cursor { background: #0026a3; color: #fafcff; }
"""
```

### 9.3 JSON Token (Design System Export)

```json
{
  "blp-cli": {
    "version": "1.0.0",
    "theme": {
      "background": "#000309",
      "foreground": "#fafcff",
      "accent": "#2fc2ff",
      "cursor": "#fafcff",
      "selection": "#0026a3"
    },
    "ansi": {
      "black": "#000309", "red": "#ff7f7f", "green": "#6bd67b",
      "yellow": "#ffeb7f", "blue": "#7f9bff", "magenta": "#d67fff",
      "cyan": "#7fbcff", "white": "#f7eaff",
      "brightBlack": "#1e2b3d", "brightRed": "#ffdbdb",
      "brightGreen": "#ccffd4", "brightYellow": "#fff9bd",
      "brightBlue": "#dbe3ff", "brightMagenta": "#f4dbff",
      "brightCyan": "#dbedff", "brightWhite": "#ffffff"
    },
    "semantic": {
      "surface00": "#000309",
      "surface01": "#1e2b3d",
      "surface02": "#0a1628",
      "dimmed": "#1e2b3d",
      "border": "#1e2b3d",
      "borderFocus": "#2fc2ff",
      "borderError": "#ff7f7f",
      "danger": "#ff7f7f",
      "success": "#6bd67b",
      "warn": "#ffeb7f",
      "info": "#7f9bff",
      "surfaceDangerTint": "rgba(255, 127, 127, 0.1)",
      "surfaceWarnTint": "rgba(255, 235, 127, 0.1)",
      "surfaceSuccessTint": "rgba(107, 214, 123, 0.1)"
    },
    "typography": {
      "fontFamily": "Goorm Sans Code",
      "fontFamilyNerd": "GoormSansCode Nerd Font",
      "fallback": "monospace",
      "weights": [400],
      "lineHeight": 1.2,
      "scale": {
        "xs": { "size": "0.75em", "color": "dimmed" },
        "sm": { "size": "0.875em", "color": "foreground" },
        "base": { "size": "1em", "color": "foreground" },
        "lg": { "size": "1.25em", "color": "foreground", "style": "bold" },
        "xl": { "size": "1.5em", "color": "accent", "style": "bold" },
        "2xl": { "size": "2em", "color": "accent", "style": "bold" }
      }
    },
    "motion": {
      "typeRevealMs": 25,
      "scanlineMs": 50,
      "panelDrawMs": 10,
      "pulseMs": 800,
      "glitchMs": 80
    },
    "rules": {
      "emoji": false,
      "borderRadius": 0,
      "borderWeight": "heavy",
      "animationUnit": "character"
    }
  }
}
```

---

## 10. 사용 예시 (Usage Examples)

### 10.1 스플래시 화면 (ASCII Art + Type Reveal)

- **타이틀**: `text-2xl`, `accent`, ASCII 아트 (Braille 또는 Block Elements로 구성된 로고).
- **하단 로그**: `text-sm`, `typeReveal` 애니메이션으로 상태 메시지 순차 출력.
- **구성**: 중앙에 대형 ASCII 아트 로고, 하단에 `▶` 프롬프트 기호와 초기화 로그.
- **배경**: `surface-00`(`#000309`) 단색. 로고는 `accent` 또는 `bright_white`.

### 10.2 시스템 모니터링 대시보드

- **레이아웃**: 좌측 `CPU`/`Load Average` 패널, 우측 `Memory`/`Swap` 패널, 하단 `Network I/O` 패널.
- **패널 구분**: `surface-01` 배경으로 각 패널 영역 분리. 테두리는 희미하게만.
- **CPU/Memory**: `Block Fill` 프로그레스 바 (`█`, `░`) + 수치 `text-xl` + `accent`.
- **Network**: Sparkline (`▁▂▃▅▆▇█`) + RX/TX 수치.
- **LIVE 표시**: `●` (`bright_green`) + `text-sm` + `Pulse` 애니메이션.

### 10.3 에러 상태 (Pulse + Background Alert)

- **모달 본체**: `surface-danger-tint`(`#ff7f7f` 10% 오버레이) 배경으로 전환.
- **헤더**: `bright_red` + `nf-fa-times` 아이콘 + `text-lg`.
- **본문**: `fg-primary`, 에러 메시지 표시.
- **액션 버튼**: `[Retry]`(`accent` 포커스), `[Abort]`(`dimmed`), `[Log]`(`info`).
- **Pulse**: `danger`(`#ff7f7f`)가 800ms 주기로 밝기 변화 (`bright_red` ↔ `red`).
- **테두리**: `border-error`(`#ff7f7f`)를 미세하게만 적용.

---

## 11. 자산 및 참조

### 11.1 Goorm Sans Code CDN

```html
<!-- 최신 버전 (v1.0.1) -->
<link rel="stylesheet" href="https://statics.goorm.io/fonts/GoormSansCode/v1.0.1/GoormSansCode.min.css">

<!-- 또는 @import -->
<style>
  @import url("https://statics.goorm.io/fonts/GoormSansCode/v1.0.1/GoormSansCode.min.css");
</style>
```

### 11.2 Nerd Font 패치 버전

- **Repository**: `https://github.com/soomtong/GoormSansCodeNerdFont` (Community Patch)
- **Version**: NerdFont 3.2.1
- **Usage**: 터미널 에뮬레이터에 직접 설치 후 `GoormSansCode Nerd Font`로 지정.

### 11.3 라이선스

- **Goorm Sans Code**: SIL Open Font License 1.1
- **BLP CLI Spec**: 프로젝트 내부 자유 사용, 외부 배포 시 명시 권장.

---

## 12. 체크리스트 (Adoption Checklist)

- [ ] 터미널/에디터 배경색 `#000309`, 전경색 `#fafcff` 적용
- [ ] Goorm Sans Code (또는 Nerd Font 패치) 폰트 설정
- [ ] Emoji 출력 비활성화 또는 필터링 적용
- [ ] Box Drawing 문자가 깨지지 않는지 확인 (Unicode 지원 터미널 필수)
- [ ] `accent` 색상 `#2fc2ff`를 포커스/커서/링크에 적용
- [ ] 애니메이션은 캐릭터 단위로 구현 (프레임 렌더링 금지)
- [ ] 테두리는 보조 구분 수단으로만 사용, 1차 구분은 배경색(`surface`) 활용
- [ ] Heavy Border(`┏━┓`)는 희미하게 적용, 포커스 시에만 미세 강조
- [ ] Dimmed 상태는 `#1e2b3d`로 통일

---

*End of Specification.*
