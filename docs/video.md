# video.md

영상 룩 기준. **16:9 · 1920×1080 · 30fps.**
규칙: 색 · 폰트는 `design.md`에 있는 값만 쓴다. 영상 글자 크기 = Figma 값 × 2.8 (반올림, px).
장면 순서 · 흐름 · 화면 구성은 여기 적지 않는다 (레퍼런스와 비트 시트가 정함). 움직임은 `motion.md`를 따른다.

정한 것 (2026-10-25): 배경 **밝은** · 헤드라인 **단정하게** · 엔드 카드 **어두운**.

---

## 1. 텍스트 최소 크기

| 변수 | px | 근거 |
|---|---|---|
| `video-min` | 31 | `Text/eyebrow` 11 × 2.8 = 30.8 → 31 (프레임 높이의 2.9%) |

- 보는 사람이 **읽어야 하는 글자**는 모두 31px 이상이다.
- 폰 프레임 안 화면 이미지의 글자(Figma 11~28px × 1.1 = 약 12~31px)는 읽히지 않는 그림으로 본다. 읽혀야 하면 카메라로 밀지 말고 해당 부품을 `src/parts`에서 꺼내 5장 크기로 보여준다 (화면 이미지는 ×1.82 넘게 키우면 흐려짐, 4장).
- 31px보다 작은 글자를 새로 만들지 않는다.

---

## 2. 배경

| 변수 | 값 | design.md | 언제 |
|---|---|---|---|
| `video-bg` | `#f7f7f8` | `color-surface` | 기본 배경 (밝은) |
| `video-end-bg` | `#18191b` | `color-text` | 엔드 카드 (어두운) |

- 기본 배경을 `color-bg`(흰색)가 아니라 `color-surface`로 둔다. parts 카드와 화면 이미지가 흰색이라 같은 흰색이면 경계가 사라진다.
- 단색만 쓴다. 그라디언트 · 질감 · 무늬 없음 (design.md에 없음).
- 엔드 카드 밖에서 어두운 배경을 쓰지 않는다.

---

## 3. 글자

폰트 `Pretendard` 로컬 파일만 (`design.md` 3장 A). 굵기 400 · 600 · 700. 자간 0%. 렌더 전 `document.fonts.ready`를 기다린다.

### 크기 (Figma × 2.8)

| 변수 | Figma 스타일 | 굵기 | 크기 / 행간 (px) |
|---|---|---|---|
| `video-display` | `Text/display` 28 / 34 | 700 | 78 / 95 |
| `video-title` | `Text/title` 24 / 32 | 600 | 67 / 90 |
| `video-compact` | `Text/compact-title` 22 / 28 | 700 | 62 / 78 |
| `video-section` | `Text/section` 20 / 28 | 700 | 56 / 78 |
| `video-heading` | `Text/heading` 18 / 28 | 600 | 50 / 78 |
| `video-body` | `Text/body` 15 / 24 | 400 | 42 / 67 |
| `video-list` | `Text/list-title` 15 / 22 | 600 | 42 / 62 |
| `video-label` | `Text/label` 14 / 20 | 600 | 39 / 56 |
| `video-caption` | `Text/caption` 12 / 16 | 400 | 34 / 45 |
| `video-eyebrow` | `Text/eyebrow` 11 / 16 | 600 | 31 / 45 |

### 헤드라인 (단정하게)

- 헤드라인은 `video-display` 78px, 최대 두 줄. 이보다 키우지 않는다.
- 헤드라인 아래 보조 줄은 `video-heading` 50px.
- 화면 · 부품이 주인공이고 글자는 거든다. 글자로 화면을 꽉 채우지 않는다.

### 색

| 변수 | 값 | design.md | 언제 |
|---|---|---|---|
| `video-text` | `#18191b` | `color-text` | 밝은 배경 위 기본 글자 |
| `video-text-muted` | `#75777c` | `color-text-muted` | 밝은 배경 위 보조 글자 |
| `video-accent` | `#3759de` | `color-primary` | 한 문장에서 한 단어만 강조 |
| `video-end-text` | `#ffffff` | `color-bg` | 엔드 카드 위 글자 |

- 엔드 카드 위 보조 글자는 `video-text-muted`를 쓰되 `video-label`(39px) 이상으로만 쓴다 (어두운 바탕에서 대비가 낮음).
- `color-error` · `color-success` · 일러스트 색은 글자에 쓰지 않는다.

---

## 4. 폰 프레임

`src/screens/*.png`(780×1688 = 390×844 @2x)를 감싸는 틀.

| 변수 | 값 | 근거 |
|---|---|---|
| `video-phone-screen` | 429 × 928 px | 390×844 × 1.1. 높이가 프레임의 86% |
| `video-phone-bezel` | 12px, `#18191b` | `color-text` |
| `video-phone-size` | 453 × 952 px | 화면 + 테두리 12 × 2 |
| `video-phone-radius` | 화면 52px · 바깥 64px | 테두리 두께만큼 바깥이 크다 |
| `video-phone-shadow` | `0 22px 67px #0000001F` | `Shadow/lg` × 2.8 |

- 화면 이미지는 고치지 않는다. 상태 표시줄(9:41)이 이미 들어 있으므로 노치 · 다이내믹 아일랜드를 그리지 않는다.
- 화면 이미지는 원본보다 크게 보이면 흐려진다. 폰 프레임을 키울 수 있는 한계는 **×1.82**(429 → 780px)다. `motion.md` 5장 카메라 밀기(약 ×1.5)는 이 안에 있다.
- 폰 프레임은 `video-bg` 위에만 놓는다.

---

## 5. parts

`src/parts/*.html`을 영상에 그대로 쓴다. 크기는 Figma 값 × 2.8 → 부품 안 글자가 3장 크기와 같아진다.

| 부품 | Figma | 영상 (×2.8) |
|---|---|---|
| `skill-card-1~3` | 350×88 | 980×246 |
| `asset-card` | 350×74 | 980×207 |
| `mission-card` | 350×253 | 980×708 |
| `stat-card` | 350×101 | 980×283 |
| `button-submit` | 350×44 | 980×123 |
| `badge-approved` | 108×32 | 302×90 |
| `brand-icon` | 98×98 | 274×274 |
| `logo` logotype | 149×19 | 417×53 |
| `logo` symbol | 100×100 | 280×280 |

- 키우기: 부품을 감싼 틀에 `zoom: 2.8`. 움직임은 `transform`으로 따로 준다 (둘을 한 속성에 섞지 않는다).
- 그림자: 흰 카드 부품(`skill-card` · `asset-card` · `mission-card` · `stat-card`)에 `0 11px 34px #00000014` (`Shadow/md` × 2.8). 다른 부품은 그림자 없음.
- 일러스트(`src/assets/*.png`, 1200×1200)는 ×2.8에서도 원본보다 작아 흐려지지 않는다.
- 로고 색: `video-bg` 위에는 `logotype-black` · `symbol-black`, `video-end-bg` 위에는 `logotype-white` · `symbol-white` (`logo.html`의 `data-state`).
- 부품 안의 값(색 · 여백 · 모서리)은 고치지 않는다. 바꿔야 하면 `design.md`부터 고친다.

---

## 6. 간격

영상 레이아웃(글자 ↔ 부품, 부품 ↔ 부품, 글자 ↔ 로고, 한 줄 ↔ 보조 줄) 간격. `design.md` 4장 간격 × 2.8 (반올림, px). 정한 날 2026-10-25 (`motion.md` 새 후보 ⑥).

| 변수 | px | design.md |
|---|---|---|
| `video-space-tight` | 11 | `space-tight` 4 |
| `video-space-inline` | 22 | `space-inline` 8 |
| `video-space-small` | 34 | `space-small` 12 |
| `video-space-content` | 45 | `space-content` 16 |
| `video-space-page` | 56 | `space-page` 20 |
| `video-space-section` | 67 | `space-section` 24 |
| `video-space-large` | 90 | `space-large` 32 |

- 이 표에 없는 간격은 쓰지 않는다. 부품 안 여백은 부품 그대로 둔다 (5장).
