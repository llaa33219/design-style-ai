# BLP Minimal Infinite Tile

> 무한한 타일. 무한한 작업 공간.

---

## 0. 설계 원칙

1. **Tile 위주** — 모든 정보는 Tile 안에. Tile 바깥 요소 금지.
2. **Infinite Workspace** — Workspace들의 연속.
3. **단순한 반응** — 그림자 크기 변화 = element Y 변화 (X는 안 건드림).
4. **크게** — 정확한 px 수치 (아래 §2 참조). typical 웹 디자인 기준 1.5배.
5. **중앙** — Tile 안 요소 상하좌우 중앙정렬 (입력칸 제외).
6. **전체화면 tile 기본** — 한 가지 정보면 Fullscreen Tile.
7. **Tiling** — 둘 이상이면 Normal Tile로 viewport 채움. workspace padding 4px + gap 4px.
8. **Normal Tile 둥글게** — default radius = md (8px).
9. **No nesting** — Normal Tile 안에 Normal Tile 금지.
10. **All-in-DOM (웹)** — 모든 워크스페이스와 거의 모든 요소가 처음부터 HTML에 존재. 워크스페이스 이동은 `transform: translate()`만 사용. CDP/Playwright로 비현재 워크스페이스의 요소에도 직접 접근·상호작용 가능.
11. **Media = shadow O, 비-상호작용 기본** — image/video 등 media는 기본 그림자만 있고 :hover/:active 없음. 클릭 가능(hyperlink 등)한 경우만 .media-link로 hover/active 추가.

> 모든 표면은 **BLP WHITE**. 색은 강조/상태에만.
> **Normal Tile은 border만, 자체 그림자 0.**
> **그림자 변화 = Y 변화만** (X 절대 안 건드림).
> **Media(image/table/chart/diagram/video) 자체 border 0, 기본 shadow O, 기본 비-상호작용.**

---

## 1. 컬러

| 토큰 | HEX | 용도 |
|---|---|---|
| `BLP WHITE` | `#fefeff` | 모든 표면 |
| `BLP DEEP WHITE` | `#FAFCFF` | 보조 표면 |
| `BLP BG BLUE` | `#EEF5FC` | 옅은 강조 |
| `BLP BG GRAY` | `#F5F5F5` | 비활성 |
| `BLP BLUE` | `#007BFF` | Main 기본 |
| `BLP DEEP BLUE` | `#005BDD` | Main hover |
| `BLP ULTRA DEEP BLUE` | `#0026A3` | Main active / 강조 텍스트 배경 |
| `BLP DEEP DARK` | `#000a19` | 모든 그림자 (light) / Surface (dark) |
| `BLP ULTRA DEEP DARK` | `#000309` | 기본 텍스트 (light) / 가장 어두운 dark surface |
| `BLP SUB DARK` | `#3e4d5f` | 보조 텍스트 (light) / Shadow (dark) / Disabled (dark) |
| `BLP LIGHT DARK` | `#d4dce8` | 비활성/구분선 (light) / 보조 텍스트 (dark) |
| `BLP DARK` | `#00193D` | dark accent surface |

### 1.7 Dark Mode 토큰

Light mode를 BLP PDF의 dark 계열 토큰으로 invert.

| 토큰 | Light | Dark |
|---|---|---|
| Surface (primary, workspace/tile bg) | `BLP WHITE` `#fefeff` | **`BLP DEEP DARK` `#000a19`** |
| Surface (secondary) | `BLP DEEP WHITE` `#FAFCFF` | **`BLP DARK` `#00193D`** |
| Surface (accent, 옅은 강조) | `BLP BG BLUE` `#EEF5FC` | **`BLP DARK` `#00193D`** |
| Divider | `BLP LIGHT DARK` `#d4dce8` | **`BLP SUB DARK` `#3e4d5f`** |
| Text (primary) | `BLP ULTRA DEEP DARK` `#000309` | **`BLP WHITE` `#fefeff`** |
| Text (sub) | `BLP SUB DARK` `#3e4d5f` | **`BLP LIGHT DARK` `#d4dce8`** |
| Text (disabled) | `BLP LIGHT DARK` `#d4dce8` | **`BLP SUB DARK` `#3e4d5f`** |
| Shadow color | `BLP DEEP DARK` `#000a19` | **`BLP SUB DARK` `#3e4d5f`** |
| Main BLUE | `BLP BLUE` `#007BFF` | 동일 |
| Main DEEP BLUE | `BLP DEEP BLUE` `#005BDD` | 동일 |
| Main ULTRA DEEP BLUE | `BLP ULTRA DEEP BLUE` `#0026A3` | 동일 |

**CSS 적용 (의미 변수 이름)**:

```css
:root {
  /* light mode default */
  --blp-surface:    #fefeff;
  --blp-surface-2:  #FAFCFF;
  --blp-surface-3:  #EEF5FC;
  --blp-text:       #000309;
  --blp-text-sub:   #3e4d5f;
  --blp-shadow-color: #000a19;
}

:root[data-theme="dark"] {
  --blp-surface:    #000a19;   /* BLP DEEP DARK */
  --blp-surface-2:  #00193D;   /* BLP DARK */
  --blp-surface-3:  #00193D;   /* BLP DARK */
  --blp-text:       #fefeff;   /* BLP WHITE */
  --blp-text-sub:   #d4dce8;   /* BLP LIGHT DARK */
  --blp-shadow-color: #3e4d5f; /* BLP SUB DARK — dark surface에서 보이게 */
  /* Main BLUE 계열은 동일 */
}
```

**테마 토글** (HTML):
```html
<button onclick="document.documentElement.dataset.theme =
  document.documentElement.dataset.theme === 'dark' ? '' : 'dark'">
  Toggle
</button>
```

> **규칙**: 그림자 색은 항상 dark surface에서 보이는 색. Light mode는 BLP DEEP DARK, dark mode는 BLP SUB DARK.

---

## 2. 사이즈 (정확한 px)

### 2.1 Base 단위

- **base = 4px** (모든 gap/border의 기본 단위)
- 모든 사이즈는 4px의 배수 또는 명확한 px 값

### 2.2 타이포

| 토큰 | font-size | line-height | font-weight | letter-spacing | 비고 |
|---|---|---|---|---|---|
| `display` | **64px** | 1.15 | 700 | -0.02em | 워크스페이스 타이틀 |
| `h1` | **48px** | 1.2 | 700 | -0.015em | Tile 타이틀 |
| `h2` | **36px** | 1.25 | 700 | -0.01em | 섹션 |
| `h3` | **28px** | 1.3 | 600 | -0.005em | 서브 섹션 |
| `body` | **20px** | 1.5 | 400 | -0.005em | 본문 |
| `caption` | **16px** | 1.5 | 400 | -0.005em | 보조 텍스트 |
| `label` | **14px** | 1.5 | 600 | -0.005em | 입력 라벨 |
| `em` (강조) | inherit | 1 | 700 | inherit | padding 4px 10px, radius 4px |

### 2.3 요소 사이즈 (component)

#### 버튼 (Main / Sub)

| 속성 | 값 |
|---|---|
| padding | **18px 32px** |
| font-size | **20px** |
| font-weight | **700** |
| border | **0** (Main) / **2px BLP BLUE** (Sub) |
| border-radius (default) | **0px** (none) |
| gap (Row 안 버튼 사이) | **16px** |

#### 카드 (card-main / card-sub)

| 속성 | 값 |
|---|---|
| padding | **32px** |
| border | **0** (main) / **2px BLP BLUE** (sub) |
| border-radius (default) | **8px** (md) |
| shadow (main default) | **6px 6px 0** BLP DEEP DARK |
| shadow (sub default) | **0** |

#### 입력칸 (field)

| 속성 | 값 |
|---|---|
| padding | **22px 24px 10px** |
| border | **2px BLP BLUE** |
| border-radius | **8px** (md) |
| input font-size | **20px** |
| label font-size | **16px** (focus 시 14px = scale(0.85)) |
| label 이동량 | **translateY(-18px)** |

#### 강조 텍스트 (em)

| 속성 | 값 |
|---|---|
| padding | **4px 10px** |
| border-radius | **4px** (sm) |
| font-weight | **700** |

#### 코드 인라인 (code)

| 속성 | 값 |
|---|---|
| padding | **2px 8px** |
| font-size | **16px** |
| border-radius | **4px** (sm) |
| background | `BLP BG BLUE` |

#### Bar (차트 막대)

| 속성 | 값 |
|---|---|
| height | **18px** |
| shadow | **2px 2px 0** BLP DEEP DARK |

#### Spec Row (label + value)

| 속성 | 값 |
|---|---|
| grid-template-columns | **140px 1fr** |
| gap | **24px** |
| padding | **16px 0** |
| border-bottom | **1px solid BLP LIGHT DARK** |
| max-width | **800px** |

### 2.4 Tile 사이즈

| Tile 종류 | padding | gap | border | border-radius (default) | shadow |
|---|---|---|---|---|---|
| **Fullscreen content-host** | **64px** | 40px (내부 stack) | 0 | 0 | 0 |
| **Fullscreen tiling-host** | **4px** (= workspace outer gap) | **4px** (tile 사이) | 0 | 0 | 0 |
| **Normal Tile** | **32px** | — | **2px BLP BLUE** | **8px** (md) | **0** (자체 그림자 금지) |

### 2.5 Workspace 구조 사이즈

```
[viewport 100vw × 100vh]
  └─ [.ws] section (no padding, no margin)
      └─ [.tile.fullscreen]
          └─ content or tiling-host
              └─ [.tile.normal] × N
```

| 위치 | 값 |
|---|---|
| Workspace outer gap (viewport → tiling-host) | **4px** (workspace padding) |
| Tiling-host inner gap (tile 사이) | **4px** (grid gap) |
| Fullscreen content-host padding | **64px** |

### 2.6 Element Spacing (gap)

| 사용처 | gap 값 |
|---|---|
| `.stack` (column flex) | **24px** |
| `.row` (row flex, wrap) | **16px** |
| Fullscreen 내부 section 사이 | **40px** |
| Spec row (label + value) | **24px** |
| Bar row (label + bar + value) | **12px** |
| List items (stack 내부) | **6px** |

### 2.7 Focus Outline

| 속성 | 값 |
|---|---|
| outline | **3px solid BLP BLUE** |
| outline-offset | **4px** |
| 트리거 | `:focus-visible`만 |

---

## 3. 워크스페이스

- 크기 = 화면.
- 위치 = 자유.
- 배경 = BLP WHITE.
- **모든 워크스페이스는 Fullscreen Tile wrapper를 가진다** (border rule 적용을 위해).

### 3.1 Fullscreen Tile 2가지 모드

| 모드 | padding | 용도 |
|---|---|---|
| `content-host` | **64px** | 단일 컨텐츠 (텍스트, 폼, 데모 등) |
| `tiling-host` | **4px** (= workspace outer gap) | Normal Tile tiling 컨테이너 |

`tiling-host`는 `display: grid; gap: 4px;` 로 viewport 채움.

### 3.2 Tiling 규칙

```
[viewport]
  └─ [workspace section] (no padding)
      └─ [.tile.fullscreen.tiling-host] (padding 4px = outer gap, gap 4px = tile 사이)
          └─ [.tile.normal] × N (남은 모든 영역 채움)
```

- workspace padding **4px** (outer gap)
- tiling-host 내부 gap **4px**
- Normal Tile들이 viewport의 모든 영역을 채움
- **Normal Tile 안에 Normal Tile 금지** (겹침 금지)
- **Normal Tile 내부 빈 공간 금지** (4px gap과 모서리 제외)

### 3.3 전환

- 속도: `ease-out 0.5s`

### 3.4 1px Border — 모든 Fullscreen Tile 워크스페이스간

| 이동 방향 | W1 (current) 보더 | W2 (target) 보더 |
|---|---|---|
| 우측 | W1 우측 | W2 좌측 |
| 좌측 | W1 좌측 | W2 우측 |
| 아래 | W1 아래 | W2 위 |
| 위 | W1 위 | W2 아래 |

- 색: BLP BLUE
- 등장: 0.2s ease
- 지속: ~1.2s (transition + 약간 유지)
- 사이즈: **1px**

### 3.5 네비게이션

- **방향키** `←` `→` `↑` `↓` — 인접 워크스페이스
- **마우스 휠** — 세로/가로 스크롤
- **Nav 워크스페이스 버튼** — 모든 워크스페이스로 직접 이동 (전용)

**규칙**: 워크스페이스 내비게이션 표기는 **Nav 워크스페이스에만**. 다른 워크스페이스 tile 아래에 nav button 두기 **금지.** Minimal 원칙 위반.

| 위치 | 허용 |
|---|---|
| Home | Nav 버튼만 (다른 workspace nav 금지) |
| Nav 워크스페이스 | 모든 워크스페이스 버튼 (전용) |
| 그 외 워크스페이스 | nav button **절대 금지** (tile 아래에 두지 않음) |

> 문서/예시처럼 의도된 nav 표기 외에는 일절 두지 않는다.

### 3.6 All-in-DOM (Automation-Friendly)

> **영상은 상관없지만, 웹페이지에서는 모든 워크스페이스와 거의 모든 요소가 처음부터 HTML에 존재해야 한다.** CDP / Playwright / Puppeteer 등으로 자동화 테스트/스크래핑할 때, 현재 화면에 보이지 않는 워크스페이스의 요소에도 직접 접근·상호작용할 수 있어야 한다.

**규칙**:
- 모든 `<section class="ws">`는 **페이지 로드 시점에 DOM에 존재** (lazy load / 동적 생성 금지)
- 워크스페이스 간 전환은 `display: none/visibility: hidden` 사용 **금지**
- 화면 이동은 **CSS `transform: translate()`** 만 사용
- 모든 input / button / link / form 요소는 **모든 워크스페이스에서 즉시 접근 가능**

**금지**:
```html
<!-- ❌ display: none으로 숨기기 -->
<section class="ws" style="display:none;">...</section>

<!-- ❌ 동적 로드 -->
<script>
  fetch('/workspace/sim').then(html => insertAdjacentHTML(...));
</script>

<!-- ❌ iframe 안에 분리 -->
<iframe src="/workspace/sim"></iframe>
```

**올바른 방식**:
```html
<!-- ✅ 모든 ws가 처음부터 DOM에 존재 -->
<section class="ws" data-row="0" data-col="0" data-id="home">...</section>
<section class="ws" data-row="0" data-col="1" data-id="ws">...</section>
<section class="ws" data-row="2" data-col="0" data-id="sim">...</section>
<!-- ... 14개 전부 존재 ... -->

<style>
  #grid { transition: transform 0.5s ease-out; }
  /* 이동은 transform만 */
</style>
```

**CDP / Playwright 예시**:

```js
// 현재 화면에 보이지 않는 워크스페이스의 버튼도 클릭 가능
await page.click('[data-id="sim"] button[data-go="home"]');
// → 시뮬레이션 워크스페이스(현재 화면 X)의 Home 버튼 클릭
// → 워크스페이스 이동 + home 워크스페이스 도착

// 모든 워크스페이스의 input에 직접 fill 가능
await page.fill('[data-id="elements"] #ex-input', 'hello');
// → elements 워크스페이스(현재 화면 X)의 input에 입력

// Nav 워크스페이스 버튼 클릭으로 다른 워크스페이스로 이동
await page.click('[data-id="nav"] button[data-go="typo"]');
```

**장점**:
- **스크래핑**: 한 페이지에 모든 워크스페이스의 텍스트/속성 추출 가능 (curl / fetch)
- **테스트 자동화**: 워크스페이스 이동 없이 요소 테스트
- **SEO**: 모든 워크스페이스의 컨텐츠가 HTML에 존재 (검색 엔진이 읽을 수 있음)
- **접근성**: 스크린 리더가 모든 워크스페이스 콘텐츠를 읽을 수 있음

**주의**:
- 모든 `<button>`, `<input>`, `<a>` 등은 페이지 로드 시점에 활성화 상태
- `display: none` / `visibility: hidden` 사용 시 자동화 도구가 접근 불가 → **금지**
- `transform` / `position` 이동은 자동화 도구 접근에 영향 없음
- `pointer-events: none`도 자동화 도구 접근 불가 (CSS 클릭 X). 시각 효과로만 사용할 것

**검증 (curl/fetch)**:
```bash
$ curl http://localhost/index.html | grep -c '<section class="ws"'
14   # ← 14개 워크스페이스 전부 응답에 포함

$ curl http://localhost/index.html | grep -c '<button'
40+  # ← 모든 워크스페이스의 버튼 전부 응답에 포함

$ curl http://localhost/index.html | grep -c '<input'
8    # ← 모든 워크스페이스의 input 전부 응답에 포함
```

---

## 4. 타일

### 4.1 두 종류

| 종류 | padding | Gap | Border | Shadow | Radius (default) | Transform |
|---|---|---|---|---|---|---|
| **Fullscreen Tile** | 64px (content) / 4px (tiling) | 0 | 0 | 0 | 0 | 0 |
| **Normal Tile** | 32px | 4px (외부 grid) | **2px BLP BLUE** | **0** | **8px (md)** | **0** (자체) |

### 4.2 Normal Tile 둥글기

Normal Tile은 default로 `border-radius: 8px (md)` 적용. 의도에 따라 0/4/8/12/16 변경 가능.

### 4.3 Tiling 위반 금지

Normal Tile 안에는 **빈 공간을 만들지 않는다.** 다음만 허용:
- 4px gap (tile 사이)
- 모서리 (border-radius에 의한 코너)

이 외의 영역에서 workspace 배경이 보이는 빈 공간은 **절대 금지.** 모든 tile은 content로 가득 차 있어야 한다.

### 4.4 정렬

- Tile과 그 안 요소 = **상하좌우 중앙정렬**
- 입력칸 = 좌측 정렬

---

## 5. 타일 내부 요소

### 5.1 Main — 그림자 변화 = Y 변화 (절대 규칙, X는 안 건드림)

| 상태 | Shadow Y | Element Y (translateY) | Background |
|---|---|---|---|
| default | 6 | **translateY(0)** | BLP BLUE |
| hover | 2 | **translateY(4px)** (그림자 -4 = Y +4) | BLP DEEP BLUE |
| active | 0 | **translateY(6px)** (그림자 -6 = Y +6) | BLP ULTRA DEEP BLUE |
| focus-visible | (default) | (default) | (default) + outline |

> **규칙**: shadow Y가 변하면 element의 Y(translateY)도 동일량 변화. **X는 절대 안 건드림.** `translate(x, y)` 금지, `translateY`만.

### 5.2 Sub

| 상태 | Shadow Y | Element Y (translateY) |
|---|---|---|
| default | 0 | translateY(0) |
| hover | 6 | **translateY(-6px)** (그림자 +6 = Y -6) |
| active | 2 | **translateY(-2px)** (그림자 -4 = Y +4) |
| focus-visible | (default) | (default) + outline |

### 5.3 active vs focus — 분리

- **active** (`:active`): 마우스/터치 down. shadow 0/0, background ULTRA DEEP, translateY(6px).
- **focus-visible** (`:focus-visible`): 키보드 focus. shadow/background/transform 변화 없음. outline만.

### 5.4 입력칸

- hover 반응 없음
- focus 시 floating label `translateY(-18px) scale(0.85)` 이동
- 보더 2px BLP BLUE 고정
- 그림자 변화 없음

### 5.5 강조 텍스트 (em)

padding **4px 10px**, border-radius **4px**, font-weight **700**, BLP WHITE on BLP BLUE.

### 5.6 Media (이미지 + 자막)

이미지를 큼지막하게 중앙에 배치하고, 아래에 자막을 두는 컴포넌트.

> **규칙**: media(image/table/chart/diagram/video)는 **border 없음. 기본적으로 그림자 있음, 호버/active 상호작용 없음.** 클릭 상호작용이 있는 경우 (예: hyperlink) hover/active 애니메이션 + 그림자 추가.

```
┌─────────────────────────────┐
│                             │
│       ┌─────────────┐       │  ← max-width 720px (image)
│       │             │       │
│       │   IMAGE     │       │  ← aspect-ratio 16:9, border 0, shadow md
│       │             │       │
│       └─────────────┘       │
│                             │
│       자막 1줄               │  ← max-width 720px, text-align center
│       자막 2줄               │
│       자막 3줄까지 가능       │
│                             │
└─────────────────────────────┘
```

| 속성 | 값 |
|---|---|
| image width | **100%** (max-width **720px**) |
| image aspect-ratio | **16:9** |
| image border | **0** (없음) |
| image border-radius | **md (8px)** |
| **image shadow (default)** | **md (6px 6px 0)** — 항상 |
| image :hover | **없음** (media는 기본 비-상호작용) |
| image :active | **없음** |
| image background | `BLP BG BLUE` (light) / `BLP DARK` (dark) |
| caption width | **max-width 720px**, centered |
| caption font-size | **20px** (body) |
| caption line-height | **1.5** |
| caption color | `BLP SUB DARK` (light) / `BLP LIGHT DARK` (dark) |
| caption max 줄 수 | **3줄** |

**기본 (비-상호작용) CSS**:
```css
.media-image {
  width: 100%; aspect-ratio: 16 / 9;
  background: var(--blp-bg-blue);
  border: 0;
  border-radius: var(--blp-radius-md);
  box-shadow: var(--blp-shadow-md);   /* ← 항상 그림자 */
  display: flex; align-items: center; justify-content: center;
  /* :hover / :active 없음 */
}
.media-caption {
  text-align: center;
  font-size: 20px; line-height: 1.5;
  color: var(--blp-text-sub);
}
```

**클릭 가능 (hyperlink 등) CSS** — `.media-link` 클래스 추가:
```css
.media-image.media-link {
  cursor: pointer;
  transition: box-shadow var(--blp-base) ease-in-out,
              transform    var(--blp-base) ease-in-out;
}
.media-image.media-link:hover  { box-shadow: var(--blp-shadow-hover); transform: translateY(4px); }
.media-image.media-link:active { box-shadow: 0 0 0;                  transform: translateY(6px); }
```

> 클릭 가능 media는 Main 패턴 (shadow-md → shadow-hover → 0, translateY 0 → 4 → 6). **X는 안 건드림. 그림자 변화 → translateY만.**

**HTML**:
```html
<div class="media-block">
  <div class="media-image">[IMAGE]</div>
  <div class="media-caption">자막 한 줄<br/>자막 두 줄<br/>자막 세 줄까지</div>
</div>
```

### 5.7 Simulation (3D / 물리엔진) Pattern

Normal Tile tiling-host 안에 **Settings 패널 + 시뮬레이션 viz** 배치.

```
┌────────────────────────────────────────────┐
│ Settings          │                         │
│ ┌──────────────┐  │    ┌─────────────┐    │
│ │ mass         │  │    │             │    │
│ └──────────────┘  │    │   3D Scene  │    │  ← viz tile (larger)
│ ┌──────────────┐  │    │             │    │
│ │ gravity      │  │    │             │    │
│ └──────────────┘  │    └─────────────┘    │
│ ┌──────────────┐  │                         │
│ │ friction     │  │                         │
│ └──────────────┘  │                         │
│ ┌──────────────┐  │                         │
│ │ Run          │  │                         │
│ └──────────────┘  │                         │
└───────────────────┴─────────────────────────┘
   (2fr)                  (3fr)
```

**규칙**:
- tiling-host `grid-template-columns: 2fr 3fr` (settings 작게, viz 크게 — 정확히 반반일 필요 없음)
- viz가 더 클 수 있음 (시뮬레이션이 시각적으로 중요)
- 모든 Normal Tile 내부 content로 가득 채움 (Tiling 원칙 준수)

**CSS**:
```css
.ws.tiling-host.ws-grid-sim {
  grid-template-columns: 2fr 3fr;  /* settings 2, simulation 3 */
}
```

---

### 5.8 Table (데이터 표)

데이터 표기는 **각 행이 하나의 tile** 또는 **tile-like 행**으로 구성.

> **규칙**: table 자체 border 없음. 경계는 header bg(BLP BLUE) + row divider(1px BLP LIGHT DARK)만으로 표현.

```
┌────────────────────────────────────────────────────┐
│ ID    │ Name           │ Score   │ Status   │      │  ← header (BLP BLUE bg, border 0)
├───────┼────────────────┼─────────┼──────────┤      │  ← divider (1px BLP LIGHT DARK)
│ 001   │ Alpha          │ 92      │ Active   │      │
├───────┼────────────────┼─────────┼──────────┤      │  ← divider
│ 002   │ Beta           │ 87      │ Pending  │      │
├───────┼────────────────┼─────────┼──────────┤
│ 003   │ Gamma          │ 95      │ Active   │      │
└────────────────────────────────────────────────────┘
```

| 속성 | 값 |
|---|---|
| table border | **0** (없음) |
| header bg | `BLP BLUE` |
| header text | `BLP WHITE` |
| row height | **48px** |
| row padding | **12px 16px** |
| row divider | **1px solid BLP LIGHT DARK** |
| font-size | **16px** (caption) |
| font-weight | 400 (body) / 600 (header) |
| border-radius | **0** (테이블은 각지게 — 데이터 정렬) |
| column gap | **16px** |
| 행 호버 | bg `BLP BG BLUE` (light) / `BLP DARK` (dark) |

> **주의**: Table 자체는 각진 모서리 (Radius none) + border 0. 데이터 정렬이 우선. 단, table을 감싸는 Normal Tile은 둥글게 (md) + border 있음.

---

## 6. Media Notation (시각 자료 표기법)

이 디자인 언어를 **영상/시각 콘텐츠**에 활용할 때의 표기법. 표, 그래프, 다이어그램, Hero 이미지 등 모든 시각 자료는 다음 원칙을 따른다.

### 6.1 적용 범위

**반드시 미디어 표기법을 따라야 하는 경우**:
- Hero 이미지 / 오프닝 타이틀
- 영상 키 비주얼 (KVS)
- 인포그래픽 / 다이어그램
- 데이터 표 / 차트
- 동영상 프레임 / 시퀀스
- 발표 자료 슬라이드
- SNS / 마케팅 비주얼

**적용하지 않아도 되는 경우**:
- 순수 텍스트 콘텐츠 (문서, 코드, 데이터 입력)
- 시스템 UI / 폼 (입력 중심)

### 6.2 핵심 원칙

1. **Tile 위주** — 모든 시각 요소는 tile 안에. floating 절대 금지.
2. **Hard shadow** — blur 그림자 절대 금지. hard offset만.
3. **BLP 컬러** — 강조/상태에만. 배경은 BLP WHITE (light) / BLP DEEP DARK (dark).
4. **Rounded** — 기본 둥근 모서리 (md). Table처럼 정렬이 우선이면 sharp 예외.
5. **1.5x 크기** — 일반 웹의 1.5배 큼직하게.
6. **Center 정렬** — 상하좌우 중앙.
7. **Y-only transform** — 그림자 변화 시 translateY만.
8. **Media는 border 없음** — image / table / chart / video / diagram 자체에는 border X. 경계는 shadow + radius + bg로 표현. (감싸는 Tile은 border O)
9. **Media 기본 = shadow O + 비-상호작용** — image/video 등 media는 기본적으로 그림자만 있고 :hover / :active 없음. 클릭 가능한 경우 (hyperlink 등) 만 .media-link로 hover/active 추가. 그림자 변화 → translateY만 (X 안 건드림)

### 6.3 Hero 이미지 / 오프닝 타이틀

```
┌─────────────────────────────────────┐
│                                     │
│       ┌─────────────────────┐       │
│       │                     │       │
│       │      HERO IMG       │       │  ← max-width 1080px
│       │                     │       │     aspect-ratio 16:9
│       └─────────────────────┘       │
│                                     │
│         ┌───────────────┐           │
│         │   TITLE       │           │  ← display 64px
│         └───────────────┘           │
│         ┌───────────────┐           │
│         │   SUBTITLE    │           │  ← h2 36px
│         └───────────────┘           │
│                                     │
└─────────────────────────────────────┘
```

| 속성 | 값 |
|---|---|
| image max-width | **1080px** |
| image aspect-ratio | **16:9** (또는 21:9 와이드) |
| image border | **0** (없음 — media는 border X) |
| image border-radius | **md (8px)** |
| image shadow | **lg (8px 8px 0)** |
| title | display 64px |
| subtitle | h2 36px |
| caption (옵션) | body 20px |

### 6.4 Chart (막대 / 선)

```
┌────────────────────────────────────┐
│ Title                              │
│                                    │
│  ┌──────┐                          │  ← 18px height bar
│  │ 87   │  ← caption (16px)        │
│  └──────┘                          │
│  ┌──────────┐                      │
│  │ 91       │                      │
│  └──────────┘                      │
│  ┌──────────────┐                  │
│  │ 95           │                  │
│  └──────────────┘                  │
└────────────────────────────────────┘
```

| 속성 | 값 |
|---|---|
| bar background | `BLP BLUE` |
| bar height | **18px** |
| bar shadow | **hover (2px 2px 0)** (기본 비-상호작용 — shadow만 O) |
| bar :hover | **없음** (chart bar 기본 비-상호작용) |
| bar :active | **없음** |
| label | caption 16px |
| value | body 20px |
| grid | 3열 (label / bar / value), gap **12px** |
| 전체 tile border-radius | **md (8px)** |

> Chart bar는 기본 그림자만 있고 비-상호작용. 클릭 가능 (.bar-link) 시 :hover/:active 추가.

### 6.5 Diagram (흐름도 / 계층)

```
┌─────┐  ┌─────┐  ┌─────┐
│  A  │→ │  B  │→ │  C  │     ← boxes (Normal Tile)
└─────┘  └─────┘  └─────┘
   ↓        ↓        ↓
   └────────┴────────┘
        ↓
   ┌─────────────┐
   │     D       │              ← merge (Normal Tile, 더 큼)
   └─────────────┘
```

| 속성 | 값 |
|---|---|
| box | Normal Tile (radius md, border 2px BLP BLUE) — tile 자체 hover/active 규칙 따름 |
| arrow | `BLP BLUE` 2px 또는 4px 두께 선 — 비-상호작용 |
| arrow head | 삼각형 (BLP BLUE) — 비-상호작용 |
| label | caption 16px |
| spacing | **40px** (box 사이) |

### 6.6 Video Frame (KVS / 키 비주얼)

```
┌─────────────────────────────────────────┐
│                                         │
│             ┌─────────────┐             │
│             │   LOGO      │             │  ← top center
│             └─────────────┘             │
│                                         │
│         ████ TITLE ████                │  ← display 64px
│         ────────────────                │
│         Subtitle here                   │  ← h2 36px
│                                         │
│   ┌──────────┐     ┌──────────┐         │
│   │  Visual  │     │  Visual  │         │  ← 좌우 이미지
│   └──────────┘     └──────────┘         │
│                                         │
│              ▼ CTA ▼                    │  ← bottom (옵션)
│                                         │
└─────────────────────────────────────────┘
```

| 속성 | 값 |
|---|---|
| frame background | `BLP WHITE` (light) / `BLP DEEP DARK` (dark) |
| logo | top center, max-width 200px |
| title | display 64px, center |
| subtitle | h2 36px, center |
| visuals | 좌우 Normal Tile (image 박스) — shadow md, 비-상호작용 |
| CTA (옵션) | bottom center, Main 버튼 (CTA는 클릭 가능 → Main 규칙 따름) |
| 전체 padding | **64px** |
| 전체 tile border-radius | **none** (frame은 각지게) |

> Video Frame 안의 visuals(image)는 기본 shadow O + 비-상호작용. CTA 버튼만 클릭 가능 (Main 규칙 따름).

### 6.7 표기법 체크리스트

영상/시각 자료 작성 시 다음을 확인:

- [ ] 모든 요소가 tile 안에 있는가?
- [ ] floating 요소가 없는가?
- [ ] hard shadow만 사용했는가?
- [ ] BLP 컬러만 사용했는가 (외부 컬러 금지)?
- [ ] 둥근 모서리 기본 (Table/Diagram 예외)?
- [ ] 텍스트 크기 1.5배 적용했는가?
- [ ] 상하좌우 중앙 정렬인가?
- [ ] 그림자 변화 시 translateY만 사용했는가?
- [ ] **media 자체에 border 없는가?**
- [ ] **media에 기본 shadow 있는가? :hover / :active 없는가?** (clickable은 .media-link로 예외)

---

## 7. 모서리 (둥글기 기본)

### 7.1 원칙

- **기본 = 둥근 모서리**. 각진 모서리(`none` = 0px)는 의도적으로 필요한 경우만 사용.
- 일반적으로 모든 요소(button, card, input, normal tile)는 `md (8px)` 둥글게.

### 7.2 요소별 default

| 요소 | default radius | 변경 가능 |
|---|---|---|
| **Button (Main/Sub)** | **md (8px)** | none / sm / lg / xl |
| **Card (main/sub)** | **md (8px)** | none / sm / lg / xl |
| **Input (field)** | **md (8px)** | none / sm / lg |
| **Normal Tile** | **md (8px)** | none / sm / lg / xl |
| **Em (강조)** | **sm (4px)** | — |
| **Code** | **sm (4px)** | — |
| **Fullscreen Tile** | **none (0px)** | — (워크스페이스 채움) |
| **Workspace section** | **none (0px)** | — |

### 7.3 스케일

| 토큰 | 값 |
|---|---|
| `none` | **0px** — 각진 모서리. **명시적으로 필요한 경우만.** |
| `sm` | **4px** — 작은 chip, 강조 텍스트, 코드 |
| `md` | **8px** — **default** — 버튼, 카드, 입력칸, Normal Tile |
| `lg` | **12px** — 큰 카드, 모달 |
| `xl` | **16px** — 히어로 카드 |

### 7.4 예외 (각진 게 필요한 경우)

다음만 `none`을 의도적으로 사용:
- **Fullscreen Tile** — 워크스페이스 전체를 채우므로 각지게
- **Workspace section** — viewport 컨테이너
- **Table** — §5.8 데이터 정렬 우선
- **Diagram** — §6.5 흐름도 선 정렬 우선
- **Video Frame** — §6.6 프레임 자체는 각지게
- brutalist/architectural 의도의 강조 컴포넌트

이 외에는 모두 둥글게.

---

## 8. 그림자 (hard, BLP DEEP DARK)

| 토큰 | 값 |
|---|---|
| `none` | `0 0 0` |
| `hover` | `2px 2px 0 #000a19` |
| `md` | `6px 6px 0 #000a19` |
| `lg` | `8px 8px 0 #000a19` |
| `xl` | `12px 12px 0 #000a19` |

**규칙**:
- 그림자 변화 = element translateY 변화 (그림자 Y 감소 → element Y 증가, 그림자 Y 증가 → element Y 감소)
- 그림자 X와 Y는 함께 변화 (X-only / Y-only 그림자 금지)
- **Element X는 절대 안 건드림** — `translate(x, y)` 금지, `translateY`만

---

## 9. 애니메이션

| 토큰 | 값 |
|---|---|
| `fast` | `ease-in-out all 0.1s` |
| `base` | `ease-in-out all 0.2s` |
| `slow` | `ease-in-out all 0.3s` |
| `page` | `ease-out 0.5s` |
| `border` | `ease 0.2s` |

---

## 10. Do / Don't

### ✅ Do

- 한 가지 정보 = Fullscreen Tile (content-host, padding 64px)
- 둘 이상 = Fullscreen Tile (tiling-host, padding 4px + grid gap 4px) 안에 Normal Tile들
- 모든 워크스페이스는 Fullscreen Tile wrapper
- **모든 요소(button, card, input, normal tile)는 둥근 모서리 default = md (8px)**
- 그림자 변화 = element translateY 변화 (그림자 감소 = Y 증가)
- :active와 :focus 분리 (focus는 outline만)
- 상하좌우 중앙정렬
- 정확한 px 수치 사용 (body 20px, h1 48px, display 64px)
- **Normal Tile 내부를 content로 가득 채우기** (빈 공간 금지)

### ❌ Don't

- **각진 모서리 (none = 0px) 남용 금지.** Fullscreen Tile, Workspace section, Table/Diagram/Video Frame 외에는 사용하지 않기
- **워크스페이스 tile 아래에 nav button 두기 금지** (Nav 워크스페이스에만 집중)
- **Media(image/table/chart/diagram/video) 자체에 border 두기 금지.** 경계는 shadow + radius + bg로 표현
- **Media 기본 :hover / :active 상호작용 금지.** 그림자만 항상 있고 비-상호작용. 클릭 가능한 경우만 .media-link로 예외.
- **워크스페이스 lazy load / 동적 생성 금지.** 모든 ws가 처음부터 DOM에 존재 (CDP/Playwright 대응)
- **`display: none` / `visibility: hidden`으로 워크스페이스 숨기기 금지** (자동화 도구 접근 불가)
- Floating 요소 금지
- Tile 바깥 텍스트 금지
- **Normal Tile 안에 Normal Tile 금지** (tiling 겹침 금지)
- **Normal Tile 내부 빈 공간 금지** (4px gap과 모서리 제외)
- `translate(x, y)` 금지 (X 건드림). `translateY`만
- :active와 :focus 묶지 않기
- blur/soft shadow 금지
- 그림자 색을 BLUE로 두지 않기
- "1.5배" 같은 모호한 표현 금지 (정확한 px 사용)

---

## 11. CSS 변수

### 11.1 Light Mode (default)

```css
:root {
  /* surface (의미 이름) */
  --blp-surface:    #fefeff;        /* primary: workspace, tile bg */
  --blp-surface-2:  #FAFCFF;        /* secondary */
  --blp-surface-3:  #EEF5FC;        /* accent (옅은 강조) */
  --blp-divider:    #d4dce8;        /* BLP LIGHT DARK */

  /* main */
  --blp-blue:              #007BFF;
  --blp-deep-blue:         #005BDD;
  --blp-ultra-deep-blue:   #0026A3;

  /* text */
  --blp-text:       #000309;        /* BLP ULTRA DEEP DARK */
  --blp-text-sub:   #3e4d5f;        /* BLP SUB DARK */
  --blp-text-on-blue: #fefeff;

  /* shadow */
  --blp-shadow-color: #000a19;      /* BLP DEEP DARK */
  --blp-shadow-hover: 2px 2px 0 var(--blp-shadow-color);
  --blp-shadow-md:   6px 6px 0 var(--blp-shadow-color);
  --blp-shadow-lg:   8px 8px 0 var(--blp-shadow-color);
  --blp-shadow-xl:   12px 12px 0 var(--blp-shadow-color);

  /* radius */
  --blp-radius-none: 0px;
  --blp-radius-sm: 4px;
  --blp-radius-md: 8px;
  --blp-radius-lg: 12px;
  --blp-radius-xl: 16px;

  /* timing */
  --blp-fast: 0.1s;
  --blp-base: 0.2s;
  --blp-slow: 0.3s;
  --blp-page: 0.5s;
  --blp-border: 0.2s;

  /* tile */
  --blp-tile-gap: 4px;
  --blp-tile-border: 2px;

  /* typography size tokens */
  --blp-size-display: 64px;
  --blp-size-h1: 48px;
  --blp-size-h2: 36px;
  --blp-size-h3: 28px;
  --blp-size-body: 20px;
  --blp-size-caption: 16px;
  --blp-size-label: 14px;

  /* tile */
  --blp-tile-gap: 4px;
  --blp-tile-border: 2px;
}
```

### 11.2 Dark Mode Override

```css
:root[data-theme="dark"] {
  /* surface — invert */
  --blp-surface:    #000a19;        /* BLP DEEP DARK */
  --blp-surface-2:  #00193D;        /* BLP DARK */
  --blp-surface-3:  #00193D;        /* BLP DARK */
  --blp-divider:    #3e4d5f;        /* BLP SUB DARK */

  /* main — 동일 */
  --blp-blue:              #007BFF;
  --blp-deep-blue:         #005BDD;
  --blp-ultra-deep-blue:   #0026A3;

  /* text — invert */
  --blp-text:       #fefeff;        /* BLP WHITE */
  --blp-text-sub:   #d4dce8;        /* BLP LIGHT DARK */
  --blp-text-on-blue: #fefeff;

  /* shadow — dark surface에서 보이게 */
  --blp-shadow-color: #3e4d5f;      /* BLP SUB DARK */
  /* --blp-shadow-hover/md/lg/xl 자동 재계산됨 (var(--blp-shadow-color)) */
}
```

### 11.3 하위호환 alias (의미 이름 + 예전 이름 둘 다)

```css
:root {
  /* 의미 이름 (preferred) */
  --blp-surface: var(--blp-white);
  --blp-surface-2: var(--blp-deep-white);
  --blp-surface-3: var(--blp-bg-blue);
  --blp-divider: var(--blp-light-dark);
  --blp-text-sub: var(--blp-sub-dark);
}
```

---

## 12. 변경 이력

| 버전 | 변경 |
|---|---|
| 0.1 | 초안 |
| 0.2 | floating 금지, Normal Tile 그림자 제거, 그림자 색 = BLP DEEP DARK |
| 0.3 | tile 상하좌우 중앙정렬, 1.5x 크기, 구석 라벨/페이지 카운터 제거 |
| 0.4 | tiling 규칙, active/focus 분리, transform 제거, Y-only shadow 절대금기, border transition 양쪽 + 0.9s |
| 0.5 | 모든 워크스페이스에 Fullscreen Tile wrapper. Y = 그림자 동기화. Normal Tile default radius = md |
| 0.6 | 그림자 변화 = Y 변화만 (translateY만 사용). X는 절대 안 건드림 |
| 0.7 | Normal Tile 내부 빈 공간 금지 (Tiling 원칙 위반 절대금기) |
| 0.8 | **§2 사이즈 명확화** — "1.5배" 표현 제거, 정확한 px 수치만 사용 |
| 0.9 | **모서리 둥글기 기본 = 둥근 모서리**. Button/Card/Input/Normal Tile 모두 default = md (8px). HTML에서 redundant `radius-md` 58개 제거 |
| 1.0 | **§1.7 Dark Mode 토큰** 추가 (PDF dark 계열로 invert). **§5.6 Media (이미지+자막)** 컴포넌트 추가. **§5.7 Simulation (3D/물리엔진) Pattern** 추가 (2fr 3fr grid). 의미 변수 이름(`--blp-surface`) 도입. **§10.2 Dark Mode Override** |
| 1.1 | **워크스페이스 nav 표기 = Nav 워크스페이스에만.** 다른 모든 워크스페이스 tile 아래 nav button 5개 row 제거. Home menu는 Nav 버튼 1개만. §3.5 네비게이션 표기는 Nav 전용 규칙 추가, §9 Don't에 nav button 금지 추가 |
| 1.2 | **§5.8 Table (데이터 표) 컴포넌트** 추가 — header BLP BLUE, 행 호버 BLP BG BLUE. **§6 Media Notation (시각 자료 표기법)** 섹션 신설 — 6.1 적용 범위 / 6.2 핵심 원칙 / 6.3 Hero 이미지 / 6.4 Chart / 6.5 Diagram / 6.6 Video Frame / 6.7 체크리스트. §7.4 예외에 Table/Diagram/Video Frame 각진 게 허용 케이스 추가. Table 워크스페이스(3,0) 추가, Nav에 Table 버튼 |
| 1.3 | **Media 자체 border 금지** — image/table/chart/diagram/video에 border X. §5.6 image border 0, §5.8 table border 0, §6.2 핵심 원칙 #8, §6.3 Hero image border 0, §6.7 체크리스트에 border 항목 추가, §10 Don't에 media border 금지 추가. HTML .media-image / .data-table border 제거 |
| 1.4 | **All-in-DOM 규칙** — §0 #10 추가, §3.6 All-in-DOM 섹션 신설. 모든 워크스페이스 14개 처음부터 DOM 존재 확인. `display:none` / `visibility:hidden` 사용 금지 (CDP/Playwright 접근성). 워크스페이스 이동은 `transform: translate()`만. curl/fetch/CDP/Playwright 예시 코드 포함. HTML 검증: section.ws 14개, button 40+, input 8개 모두 DOM 존재 |
| 1.5 | **Media 비-상호작용 규칙** — §0 #11 추가, §5.6 Media에 image :hover/:active 없음 명시, .media-link (clickable) 변형 추가 (Main 패턴 — shadow + translateY, X 안 건드림), §6.2 핵심 원칙 #9 추가, §6.4 Chart bar 비-상호작용 명시, §6.5 Diagram arrow 비-상호작용, §6.6 Video visuals 비-상호작용, §6.7 체크리스트에 media shadow/hover 항목, §10 Don't에 media :hover/:active 금지. HTML: .media-link CSS 추가, Media 워크스페이스에 clickable media 예시 추가 |
