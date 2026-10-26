# motion.md

우리 서비스의 움직임 기준. 성격: **경쾌한** (빠르게 나오고, 꽂히듯 멈추고, 튕기지 않는다).
규칙: 이 문서에 있는 값만 쓴다. 없는 숫자가 필요하면 "새 후보"에 올리고 묻는다.
장면 순서 · 화면 배치는 여기 적지 않는다 (영상마다 비트 시트로). 색 · 글자 · 로고는 `design.md`만 따른다.

출처 (2026-10-25)
- **영상**: skillry `saadpastadev-347341` 원본 → `references/saadpastadev-347341.mp4` (1280×720 · 30fps · 24.5s). 시점은 `mm:ss 프레임번호f`.
- **Carbon**: Carbon Design System, *Motion overview* (duration 6개 · easing cubic-bezier).
- **Remotion**: Remotion Prompts, *Apple-Style Device Rise Animation* (30fps · ease-out cubic).

단위: 프레임(f), 30fps 기준. ms = f × 33.3. 다른 fps로 렌더하면 ms를 지킨다.

---

## 1. Primitives

### 길이 (duration) 6단계

| 변수 | f | ms | 레퍼런스 시점 | Carbon 대응 |
|---|---|---|---|---|
| `duration-3` | 3 | 100 | 00:17 회사 이름 롤인 518→521f | `duration-fast-02` 110ms |
| `duration-4` | 4 | 133 | 00:05 검색창으로 줌 157→160f · 00:21 끝 문장 퇴장 658→662f | `duration-moderate-01` 150ms |
| `duration-6` | 6 | 200 | 00:00 첫 단어 "Stock" 등장 0→6f | 없음 (영상 값) |
| `duration-8` | 8 | 267 | 00:14 알림 내려옴 438→446f · 00:16 알림이 검정 화면으로 커짐 483→491f | `duration-moderate-02` 240ms |
| `duration-12` | 12 | 400 | 00:12 스와이프 버튼 펼쳐짐 375→388f · 00:03 키보드 올라옴 116→126f | `duration-slow-01` 400ms |
| `duration-24` | 24 | 800 | 00:15 알림으로 카메라 밀기 456→482f · 00:01 로고 3개 날아와 앉음 50→78f | `duration-slow-02` 700ms |

### 곡선 (curve)

성격이 "경쾌한"이라 Carbon **expressive** 값을 쓴다. productive는 쓰지 않는다.

| 변수 | cubic-bezier | Carbon 원래 이름 | 레퍼런스 시점 |
|---|---|---|---|
| `curve-enter` | `0, 0, 0.3, 1` | entrance · expressive | 00:00 "Stock" 1f에 이미 절반 크기, 3f에 거의 다 큼 → 앞이 빠르고 끝이 길다 |
| `curve-exit` | `0.4, 0.14, 1, 1` | exit · expressive | 00:05 검색창 줌 157→160f, 마지막 프레임에서 가장 빠름 |
| `curve-standard` | `0.4, 0.14, 0.3, 1` | standard · expressive | 00:15 카메라 밀기 456→482f, 천천히 시작해 천천히 멈춤 |
| `curve-linear` | `0, 0, 1, 1` | 없음 | 진행 · 회전처럼 일정한 속도 자체가 뜻일 때만 |

- 튕김(spring · overshoot) 없음. 영상 전체에서 크기가 목표를 넘었다 돌아오는 프레임을 찾지 못했다.
- Remotion의 `Easing.out(Easing.cubic)`(= `0.33, 1, 0.68, 1`)은 `curve-enter`로 대신한다.

---

## 2. Semantic

부품 · 화면에는 이 5개만 붙인다. Primitive를 직접 쓰지 않는다.

| 변수 | 길이 | 곡선 | 뜻 | 레퍼런스 시점 |
|---|---|---|---|---|
| `motion-enter` | `duration-6` | `curve-enter` | 화면에 새로 나타남 (크기 0 → 1, 투명 → 불투명) | 00:00 "Stock" 0→6f · 00:01 "is" 30→36f |
| `motion-exit` | `duration-4` | `curve-exit` | 화면에서 사라짐. 등장보다 짧다 | 00:21 끝 문장 658→662f · 00:00 첫 줄 27→29f(3f) |
| `motion-swap` | `duration-3` | `curve-enter` | 제자리에서 내용만 바뀜 (글자 · 상태 · 숫자) | 00:17 회사 이름 롤 518→521f · 527→530f |
| `motion-transform` | `duration-8` | `curve-standard` | 한 물체가 모양 · 크기를 바꿔 다음 것이 됨 | 00:06 검색창 → 점 188→197f · 00:16 알림 → 검정 화면 483→491f |
| `motion-travel` | `duration-12` | `curve-standard` | 먼 거리를 이동하거나 화면 끝에서 들어옴 | 00:03 키보드 116→126f · 00:12 스와이프 버튼 375→388f |

함께 쓰는 규칙
- **겹치기(stagger)**: 여러 개가 차례로 나올 때 간격 `duration-8`. — 00:01 로고 3개 50 · 57 · 65f, Remotion 알림 간격 0.3s(9f).
- **화면 교체**: 나가는 쪽 `motion-exit`가 끝나기 전에 들어오는 쪽 `motion-enter`를 시작한다 (겹침 4f). — 00:02 글자 → 휴대폰 81→89f.
- 같은 장면에서 등장 방식을 매번 똑같이 쓰지 않는다. 영상도 커지기 · 롤 · 모양 바뀜 · 아래에서 올라옴을 섞는다.

---

## 3. Pattern

`src/parts` · `src/screens` 기준. 표에 없는 움직임은 새 후보로 묻는다.

### src/parts

| 부품 | 움직임 | 토큰 | 레퍼런스 시점 |
|---|---|---|---|
| `skill-card-1~3` | 목록으로 차례로 등장 | `motion-enter` + stagger `duration-8` | 00:01 로고 3개 50 · 57 · 65f |
| `asset-card` | `data-state` 4개 사이 바뀜 | `motion-swap` | 00:17 이름 롤 518→521f |
| `button-submit` | 문구(`data-state`) 바뀜 | `motion-swap` | 00:17 이름 롤 518→521f |
| `button-submit` | 누름 → 화면이 빠짐 | `motion-exit` 뒤 다음 화면 `motion-enter` | 00:10 Buy 누름 307→313f, 새 화면 314→321f |
| `badge-approved` | 점에서 커지며 자리 잡음 | `motion-transform` | 00:14 체크 표시 420→428f |
| `stat-card` | 숫자 바뀜: 한 자리씩 끊어서 교체(사이 움직임 없음), 간격 `duration-6` | 교체 0f · 간격 `duration-6` | 00:11 "5"→"50"→"500"→"5,000" 332 · 339 · 345 · 351f |
| `mission-card` | 진행 바 채움 (왼쪽 → 오른쪽) | `motion-travel` | 00:13 버튼 채움 395→411f (16f → `duration-12`로 줄임) |
| `logo` · `brand-icon` | 등장 | `motion-enter` | 레퍼런스 로고 움직임은 가져오지 않음. 00:00 "Stock" 0→6f와 같은 방식 |

### src/screens

| 움직임 | 토큰 | 레퍼런스 시점 |
|---|---|---|
| 화면 → 화면 교체 (겹쳐 바뀜) | `motion-exit` + `motion-enter`, 겹침 4f | 00:02 81→89f · 00:13 415→428f |
| 화면 위로 알림 · 카드가 위에서 내려옴 | `motion-enter` 길이를 `duration-8`로 | 00:14 438→446f |
| 화면 아래에서 키보드 · 시트가 올라옴 | `motion-travel` | 00:03 116→126f |
| 화면 안 스크롤 | `duration-8` · `curve-standard` | 00:09 285→293f |
| 화면 속 부품이 다음 장면이 됨 (부품이 커져 화면을 채움) | `motion-transform` | 00:16 483→491f |
| 글자 타자 (한 글자씩 나타남, 줄 사이 쉼) | 글자 등장 0f · 글자 간격 `hold-tick` · 줄 사이 `hold-glance` | 00:05 "O" "G" "D" "C" 161 · 165 · 169 · 173f |
| 휴대폰째 아래에서 솟아오름 (아래 400px · 크기 0.8 → 1 · 기울기 35° → 8°) | `duration-24` · `curve-enter` | Remotion *Device Rise* 1.5s(45f → `duration-24`로 줄임) |

---

## 4. 머무는 시간

움직임이 끝난 뒤 다음 움직임까지. 머무는 동안 제목 · 부품은 멈춰 있고, 움직임은 카메라(5장)만 맡는다.

| 변수 | f | 언제 | 레퍼런스 시점 |
|---|---|---|---|
| `hold-tick` | 4 | 타이핑 한 글자 | 00:05 "O" "G" "D" "C" 161 · 165 · 169 · 173f |
| `hold-glance` | 12 | 단어 하나 · 이름 하나 | 00:00 단어 간격 0 → 10f · 00:17 이름 롤 주기 10f |
| `hold-read` | 24 | 한 줄 읽기 | 00:21 "every Pakistani company" 630→658f (28f) |
| `hold-screen` | 48 | 화면 하나 보여주기 | 00:14 주문 완료 화면 428→482f (54f) |
| `hold-end` | 72 | 영상 마지막 화면 | 00:22 끝 화면 665→736f (71f) |

- `hold-*`는 `duration-*`의 배수(4 · 12 · 24 · 24×2 · 24×3)로만 만든다.
- 다음 강조 직전에는 `hold-glance`만큼 숨을 고른다. — 00:12 버튼 펼쳐진 뒤 388→395f.

---

## 5. 카메라

카메라는 화면 전체를 감싼 바깥 틀(wrapper)의 `scale` · `x` · `y`만 움직인다. 부품 안은 건드리지 않는다.

| 움직임 | 길이 | 곡선 | 크기 | 레퍼런스 시점 |
|---|---|---|---|---|
| 천천히 밀기 (push-in) | `duration-24` | `curve-standard` | 약 1 → 1.5 | 00:15 알림으로 456→482f |
| 아주 느리게 밀기 (머무는 동안) | 머무는 시간 전체 | `curve-linear` | 약 1 → 1.05 | 00:11 금액 화면 351→365f |
| 부품 속으로 뛰어들기 (zoom through) | `duration-4` | `curve-exit` | 부품이 화면을 채울 때까지 | 00:05 검색창으로 157→160f |
| 빠지기 (pull-out) | `duration-12` | `curve-standard` | 부품 → 휴대폰 전체 | 00:06 그래프 → 회사 화면 200→215f |

- 뛰어들기 뒤 들어간 장면은 컷 없이 이어간다 (빠른 프레임에서 바꿔 이음).
- 카메라를 흔들거나 기울이지 않는다. 영상에는 없다.

---

## 새 후보

지금 열린 후보 없음. 새로 생기면 이 표에 올리고 묻는다 (정해지기 전까지 쓰지 않는다).

| # | 움직임 | 결정 (2026-10-25) |
|---|---|---|
| ① | `mission-card` 진행 바 채움 (16f) | `duration-12`로 줄임 → `motion-travel` |
| ② | `logo` · `brand-icon` 등장 | `motion-enter` |
| ③ | 휴대폰째 솟아오름 (45f) | `duration-24`로 줄임 · `curve-enter` |
| ④ | 겹침 없는 장면 컷 (0f) | 넣지 않음 → 부품 속으로 뛰어들기 `duration-4` · `curve-exit`로 대체 |
| ⑤ | `button-submit` 원 → 알약 넓어짐 | 넣지 않음 → `motion-enter`로 대체 |
| ⑥ | 영상 레이아웃 간격 | `design.md` 4장 × 2.8 → `video.md` 6장 |
| ⑦ | `motion-enter` 시작 크기 | 0 (00:00 "Stock" 0→6f 측정, `curve-enter` 맞춤 오차 0.04) → 2장 |
| ⑧ | 글자 타자 | 등장 0f · 간격 `hold-tick` · 줄 사이 `hold-glance` → 3장 src/screens |
