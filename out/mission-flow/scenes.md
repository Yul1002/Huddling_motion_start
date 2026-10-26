# scenes — mission-flow

## 1차: 3안 요약

뼈대: `references/saadpastadev-347341.mp4` (A~J 10구간, refs.md). 새 후보 ④ · ⑤는 승인 전이라 refs.md의 대체 토큰으로 적었다 (R12 → 부품 속으로 뛰어들기 `duration-4` · `curve-exit`, R14 → `button-submit` `motion-enter`).

### 1안 (선택됨). 뼈대 그대로 — "미션 하나가 끝까지 가는 길"

- 요약: 레퍼런스 10구간을 순서대로 다 옮긴다. 글자 인트로 → 01 → 03 → 버튼 클로즈업 → 04 → 어두운 글자 → 엔드 카드.
- 흐름: A 글자 한 줄 + `skill-card-1~3` 차례로 → B `01-home` 폰 → C `mission-card`로 뛰어들어 크게 → 진행 바 점으로 오그라듦 → `03-mission`으로 빠지기 → D 머묾 · `button-submit` 누름 → F `button-submit` 단독 클로즈업, 진행 바 채움 → G `04-approved`, `badge-approved` 점에서 커짐, 위에서 `brand-icon`이 내려옴 → 밀기 → H `brand-icon`이 커져 `video-end-bg` → I 두 줄 롤(아래 줄: `src` 안 미션 단계 이름) → J `logotype-white` 엔드 카드.
- 주인공: `src/screens/01-home.png` · `03-mission.png` · `04-approved.png` / `src/parts/mission-card.html` · `button-submit.html` · `badge-approved.html` · `brand-icon.html` · `skill-card-1~3.html` · `logo.html`.
- 반영: R1~R23 전부 (23 / 23). R18은 알림 UI 대신 `brand-icon`. 어두운 배경은 H 이후 엔드 카드 구간에서만.

### 2안. 진행 바 한 줄 — "50%가 100%가 될 때까지"

- 요약: 폰 화면은 짧게, `mission-card` 진행 바를 주인공으로. 어두운 글자 롤(I)은 빼고 04 머묾 뒤 바로 엔드 카드.
- 흐름: A 글자 한 줄 → B `01-home` → C `mission-card`로 뛰어들기 · 크게 → `03-mission`으로 빠지기 → `button-submit` 누름 → `mission-card` 클로즈업, 진행 바 50% → 끝까지 채움 → 진행 바 끝이 `badge-approved` 점이 됨 → `04-approved`로 돌아와 아주 느린 밀기 → 화면 교체로 J 엔드 카드.
- 주인공: `src/parts/mission-card.html`(진행 바) · `badge-approved.html` / `src/screens/01-home.png` · `03-mission.png` · `04-approved.png`.
- 반영: R1 · R2 · R4 · R5 · R6 · R7 · R8 · R9 · R10 · R11 · R12 · R15 · R16 · R17 · R23 (15 / 23). 빠짐: R3 · R13 · R14 · R18 · R19 · R20 · R21 · R22. 길이는 24.5초보다 짧아짐.

### 3안. 글자가 끌고 가는 판 — "화면은 세 장, 말은 두 덩어리"

- 요약: 카메라 다이브 없이 01 → 03 → 04를 화면 교체로만 넘기고, 앞의 글자 인트로와 뒤의 어두운 글자 롤에 무게를 둔다.
- 흐름: A 글자 한 줄 + `skill-card-1~3` 차례로 → B `01-home` → 화면 교체 `03-mission` · `button-submit` 누름 → 화면 교체 `04-approved` · `badge-approved` 점에서 커짐 · 아주 느린 밀기 → 위에서 `brand-icon` 내려옴 → 밀기 → `brand-icon`이 커져 `video-end-bg` → I 두 줄 롤 → J 엔드 카드.
- 주인공: `src/screens/01-home.png` · `03-mission.png` · `04-approved.png` / `src/parts/skill-card-1~3.html` · `badge-approved.html` · `brand-icon.html` · `logo.html`.
- 반영: R1 · R2 · R3 · R4 · R5 · R10 · R11 · R16 · R17 · R18 · R19 · R20 · R21 · R22 · R23 (15 / 23). 빠짐: R6 · R7 · R8 · R9 · R12 · R13 · R14 · R15 (부품 클로즈업 · 다이브 전부).

### 추천: 1안

이유: 뼈대가 하나뿐이고 BRIEF 길이가 뼈대 길이(약 24.5초)라, 23개 R을 모두 토큰(R12 · R14는 대체 토큰)으로 채울 수 있는 1안이 길이와 흐름을 그대로 맞춘다.

> 선택: 1안 (2026-10-25). 새 후보 ④ · ⑤는 docs에 넣지 않음 → R12 · R14는 대체 토큰 그대로.

---

## 2차: 장면표 (1안)

- 30fps · 프레임 번호는 영상 처음부터. 길이는 모두 `docs/motion.md` 1 · 2 · 4 · 5장 토큰의 합.
- 화면 교체는 겹침 4f (motion.md 2장): 나가는 장면 `motion-exit`(4f)와 들어오는 장면 `motion-enter`(6f)가 같은 프레임에 시작한다. 그래서 다음 장면 시작 = 앞 장면 끝 − 4f인 곳이 있다.
- 배경: S1~S10은 `video-bg`, S11부터 S13까지는 `video-end-bg` (video.md 2장, refs R20 메모: 어두운 화면 이후는 엔드 카드 구간).
- 폰은 언제나 `video-phone-screen` · `video-phone-size` · `video-phone-bezel` · `video-phone-radius` · `video-phone-shadow`, 프레임 가로 · 세로 가운데 (R5). 화면 이미지는 ×1.82를 넘게 키우지 않는다 (video.md 4장).
- 부품 단독 장면은 `zoom: 2.8` (video.md 5장). 흰 카드 부품만 그림자 `Shadow/md` × 2.8.

| # | 시작 · 길이 (f) | 화면 · 부품 | 움직임 | 카메라 | 글자 | 위치 근거 | 레퍼런스 |
|---|---|---|---|---|---|---|---|
| S1 글자 인트로 | 0 · 100 | `src/parts/skill-card-1.html` · `skill-card-2.html` · `skill-card-3.html` (각 980×246, `Shadow/md` × 2.8) | 단어 1 `motion-enter` 0–6 → `hold-glance` 6–18 → 단어 2 `motion-enter` 18–24 → `hold-glance` 24–36 → 단어 3 `motion-enter` 36–42 → `hold-glance` 42–54 → 헤드라인이 위로 올라감 `motion-travel` 54–66 → `skill-card-1~3` `motion-enter`, stagger `duration-8` (66 · 74 · 82 시작, 88 끝) → `hold-glance` 88–100 | 없음 | 한 줄 "오늘도 / 하나씩, / 내 실력으로" (`src/screens/01-home.png` 헤드라인). `video-display` · `video-text`, "실력으로"만 `video-accent` ("내" · "오늘도" · "하나씩,"은 `video-text`) | 시작: 헤드라인 한 줄을 프레임 가로 · 세로 가운데. 끝: 헤드라인 + 카드 3장 세로 묶음이 프레임 가로 · 세로 가운데에 오도록 헤드라인이 묶음 맨 위 자리로 올라간다 (가로 위치는 그대로). 카드 순서는 01-home의 스킬 목록 순서. 헤드라인 ↔ 카드 `video-space-section`, 카드 ↔ 카드 `video-space-small` (video.md 6장) | R1 · R2 · R3 (A 0–80f, `f0000` · `f0030` · `f0060`) |
| S2 폰 등장 · 홈 | 100 · 54 | `src/screens/01-home.png` in 폰 프레임 | S1 전체 `motion-exit` 100–104 + 폰 `motion-enter` 100–106 (겹침 4f) → `hold-screen` 106–154 | 없음 | 없음 (화면 이미지 글자는 그림, video.md 1장) | 폰 하나를 프레임 가운데, 곁에 다른 물체 없음 | R4 · R5 (B 81–156f, `f0081` · `f0089` · `f0105`) |
| S3 미션 카드로 뛰어들기 | 154 · 4 | `01-home.png` → `src/parts/mission-card.html` | 끝 프레임에서 화면 이미지를 부품으로 바꿔 이음 (컷 없이, motion.md 5장). 화면 이미지가 ×1.82에 닿기 전 프레임에서 바꾼다 | 부품 속으로 뛰어들기 `duration-4` · `curve-exit`, 01-home의 미션 카드 가운데로 | 없음 | 뛰어드는 중심 = 01-home 미션 카드 자리 (화면 가운데보다 조금 위) | R6 (C 157–160f, `f0157` · `f0160`) |
| S4 미션 카드 크게 | 158 · 24 | `mission-card.html` 980×708, `Shadow/md` × 2.8, 진행 바 `--progress` 0.5 (기본) | 없음 · `hold-read` 158–182 | 없음 | 부품 안 글자 그대로 ("반복 업무를 줄이는 AI 자동화" 등, 3장 크기) | 부품 하나를 프레임 가운데 | R7 (C 160–185f, `f0160` · `f0185`) |
| S5 진행 바 채움 | 182 · 27 | `mission-card.html` (S4에서 그대로 이어짐) | S4 카드가 같은 자리에 그대로 있으므로 교체 · 등장 없이 바로 진행 바 `--progress` 0.5 → 1 `motion-travel` 182–194 → 진행 글자 `motion-swap` 194–197 → `hold-glance` 197–209 | 없음 | 진행 글자 "50% · 2/4 단계 완료" → "100% · 4/4 단계 완료" (`04-approved.png` 문구) | 부품 하나를 프레임 가운데 (S4와 같은 자리) | R15 (F 395–411f, `f0395` · `f0403` · `f0411`) |
| S6 홈으로 빠지기 | 209 · 12 | `mission-card.html` → `01-home.png` in 폰 프레임 | 처음 프레임 쪽 빠른 구간에서 부품을 화면 이미지로 바꿔 이음. 부품은 100%, 홈 화면 이미지 카드는 50%로 보이는 차이는 그대로 둔다 (사람 결정) | 빠지기 `duration-12` · `curve-standard`, 부품 → 폰 전체 | 없음 | 부품이 01-home 안 제자리(미션 카드 자리)로 돌아간다. 01-home 카드에는 버튼이 들어 있어 부품과 모양이 같다 | R9 (C 200–215f, `f0204` · `f0215`) |
| S7 홈 머묾 · 버튼 누름 | 221 · 48 (+ 퇴장 4) | `01-home.png` in 폰 프레임 (카드 안 버튼 = `button-submit` `apply-case` 모양) | `hold-screen` 221–269 → 버튼 누름 → 화면 `motion-exit` 269–273 | 없음 | 없음 | 누르는 대상: 01-home 미션 카드의 "적용 사례 정리하기 →". 누름 표시(손가락 · 물결)는 docs에 없어 그리지 않고 바로 퇴장 | R5 · R11 (D 215–313f, `f0307` · `f0313`) |
| S8 이번 달 미션 | 269 · 54 | `src/screens/03-mission.png` in 폰 프레임 | `motion-enter` 269–275 (S7 퇴장과 겹침 4f) → `hold-screen` 275–323 | 아주 느리게 밀기 275–323 (머무는 시간 전체 · `curve-linear` · 약 1 → 1.05), 폰 가운데 기준 | 없음 | 폰 가운데. 밀기 중에도 화면 · 부품은 멈춤 | R5 · R10 · R11 (E 314–374f, `f0316` · `f0345` · `f0365`) |
| S9 제출 버튼으로 뛰어들기 | 323 · 4 | `03-mission.png` → `src/parts/button-submit.html` `data-state="submit"` | 끝 프레임에서 부품으로 바꿔 이음 (S3과 같은 방식) | 부품 속으로 뛰어들기 `duration-4` · `curve-exit` (R12 대체 토큰, 새 후보 ④ 미채택) | 없음 | 뛰어드는 중심 = 03-mission 맨 아래 "제출하기" 버튼 | R12 (F 374–375f, `f0374` · `f0375`) |
| S10 승인 화면 · 버튼으로 밀기 | 327 · 42 | `src/screens/04-approved.png` in 폰 프레임 | S9 끝의 버튼 `motion-exit` 327–331 + 폰 `motion-enter` 327–333 (화면 교체 겹침 4f) → `hold-glance` 333–345 | 천천히 밀기 345–369 `duration-24` · `curve-standard` · 약 1 → 1.5, 04-approved 맨 아래 "내 자산에서 보기" 버튼 중심으로 (화면 이미지 ×1.5 ≤ ×1.82) | 없음 | 폰 가운데에서 시작. 밀기 중심 = 04-approved의 "내 자산에서 보기" 버튼 (`button-submit` `view-assets` 모양, 화면 아래쪽) | R5 · R16 · R19 (G 415–482f, `f0415` · `f0428` · `f0456` · `f0482`) |
| S11 어두운 화면으로 (화면 교체) | 369 · 6 | `04-approved.png` 폰 → 배경 `video-end-bg` | 밀기 끝 상태의 폰 `motion-exit` 369–373 + `video-end-bg` 바탕 투명 → 불투명만 369–375 (`duration-6` · `curve-enter`, 크기 변화 없음). 글자는 나오지 않는다. 바탕이 다 들어온 375f에 S12 시작 | 없음 (S10 밀기 끝 상태에서 폰이 퇴장) | 없음 | 바탕은 프레임 전체 | 없음 (R20 뺌, 화면 교체 토큰은 motion.md 2장) |
| S12 어두운 두 줄 타자 | 375 · 148 | 배경 `video-end-bg` | 글자 타자 (motion.md 3장 src/screens: 글자 등장 0f · 글자 간격 `hold-tick` · 줄 사이 `hold-glance`). 세는 법: 보이는 글자(한글 · 쉼표)만 한 칸씩 세고, 띄어쓰기는 세지 않는다(다음 글자와 같은 프레임에 붙음). 글자 k번째(0부터)는 줄 시작 + 4k f에 나타나고, 마지막 글자가 나타난 프레임부터 다음 쉼이 시작된다. ① 윗줄 "이번 달 미션," 6자(이 · 번 · 달 · 미 · 션 · 쉼표, 띄어쓰기 2 제외) 375 · 379 · 383 · 387 · 391 · 395 → 줄 사이 `hold-glance` 395–407 → ② 아랫줄 "적용 사례 정리하기" 8자(띄어쓰기 2 제외) 407 · 411 · … · 435 → `hold-read` 435–459 → 아랫줄 `motion-exit` 459–463 → ③ 아랫줄 "내 자산에 등록됐어요" 9자(띄어쓰기 2 제외) 463 · 467 · … · 495 → `hold-read` 495–519 → 두 줄 `motion-exit` 519–523. 롤(`motion-swap`)은 쓰지 않음 | 없음 | 위 줄 "이번 달 미션," / 아래 줄 "적용 사례 정리하기" → "내 자산에 등록됐어요" (01 · 03 · 04 화면 문구). `video-display` 두 줄 · `video-end-text` | 두 줄을 프레임 가운데, 가운데 정렬 (지금 배치 그대로). 치는 동안 줄은 항상 가운데: 글자가 늘 때마다 그때까지 쳐진 글자 묶음을 가운데 정렬로 다시 맞춘다 (줄이 조금씩 옆으로 움직임, 다시 맞추는 움직임은 글자 등장과 같은 0f). 아래 줄 아이콘 없음 | R22 (I 630–662f, `f0630` · `f0658` · `f0662`) |
| S13 엔드 카드 | 519 · 78 | 배경 `video-end-bg` · `src/parts/logo.html` `logotype-white` 417×53 | `motion-enter` 519–525 (S12 퇴장과 겹침 4f) → `hold-end` 525–597 | 없음 | 1줄 "내 실력으로" (`video-display` · `video-end-text`) / 2줄 `logotype-white` / 3줄 "반복 업무를 줄이는 AI 자동화" (`video-label` · `video-text-muted`). 고지 글 없음 | 세 줄 모두 가운데 정렬, 세 줄 묶음을 프레임 가운데. 1줄 ↔ 2줄 `video-space-small`, 2줄 ↔ 3줄 `video-space-section` (video.md 6장, 사람 결정) | R23 (J 665–736f, `f0665` · `f0690` · `f0735`) |

- 총 길이: **597f (약 19.9초)**. 레퍼런스(736f)보다 139f 짧다. 사람 결정: 영상이 짧아져도 됨.
- R1(구성)은 표 전체에 들어간다: 글자 인트로(S1) → 폰 화면 흐름 + 부품 클로즈업(S2~S10) → 어두운 글자(S11~S12) → 엔드 카드(S13).
- S6 빠지기는 01-home으로 돌아간다 (03-mission 카드에는 버튼이 없어 부품과 모양이 다름).
- R21(아래 줄 롤)은 수정 3에서 타자로 바뀌어 빠졌다.

### 새 후보 (메인에게 넘김, 정해지기 전까지 숫자 쓰지 않음)

| # | 무엇 | 쓰는 곳 | 레퍼런스 시점 | 메모 |
|---|---|---|---|---|
| ⑥ | 영상 레이아웃 간격 (글자 ↔ 부품, 부품 ↔ 부품, 글자 ↔ 로고, 한 줄 ↔ 보조 줄) | S1 · S13 | 00:01 `f0060` 단어와 아이콘 사이 · 00:22 `f0690` 단어 ↔ 로고 ↔ 주소 줄 | 결정: video.md 6장 |

반영한 R: R1 · R2 · R3 · R4 · R5 · R6 · R7 · R9 · R10 · R11 · R12 · R15 · R16 · R19 · R22 · R23 → **16 / 23**
빠진 R: R8 · R13 · R14 · R17 · R18 · R20 · R21

## 수정 기록 (2026-10-25)

### 수정 1 (장면 번호는 그때 기준)

1. **S1 헤드라인 올라감** (스냅보드 검토 요청). 헤드라인이 처음엔 프레임 가로 · 세로 가운데에 있다가, 카드가 들어오기 전에 `motion-travel`(`duration-12` · `curve-standard`, motion.md 2장 "먼 거리를 이동")로 묶음 맨 위 자리까지 올라간다. 끝 배치 간격(`video-space-section` · `video-space-small`)은 그대로. 카드 stagger는 올라감이 끝난 66f부터. S1이 88 → 100f(+12)가 되어 S2 ~ S11 시작을 12f씩 밀었다. 강조색은 장면표대로 "실력으로"만 `video-accent` (스냅보드의 "내 실력으로" 전체 강조는 builder가 고칠 것).
2. **S12 `brand-icon` 뺌** (스냅보드 검토 요청). 대신 04-approved 화면 안의 "내 자산에서 보기" 버튼(`src/parts/button-submit.html` `view-assets`)으로 밀고(R19), S13에서 그 버튼이 커져 프레임을 채운 뒤 바탕을 `video-end-bg`로 바꾸고, S14 첫 4f에 버튼이 `motion-exit`로 빠지며 어두운 바탕이 드러난다(R20 · 화면 교체 겹침 4f). R18은 살리지 못했다: 04-approved 위로 내려올 수 있는 `src/parts` 부품이 없다 (`badge-approved` · `button-submit` · `mission-card`는 이미 04 화면 안에 있어 겹쳐 내려오면 같은 UI가 두 개 보이고, `asset-card` · `stat-card`는 BRIEF 화면 밖). S12가 50 → 42f(−8)가 되어 S13 ~ S15를 다시 맞췄다. 총 길이 593 → 597f.

### 수정 2 (스냅보드 검토 · 장면 순서 다시 정함)

사람이 준 대응표대로 다시 썼다 (새 ← 옛): S1 ← S1 · S2 ← S2 · S3 ← S3 · S4 ← S4 · S5 ← S10 · S6 ← S5 · S7 ← S6 · S8 ← S7 · S9 ← S8 · S10 ← S12 · S11 ← S13 앞부분(화면 교체로 바꿈) · S12 ← S14(첫 4f 뺌) · S13 ← S15(세 줄 배치).

- 삭제: 옛 S9(제출 버튼 클로즈업) · 옛 S11(카드 → 점 → 승인 배지) · 옛 S13의 버튼 커짐 · 옛 S14 첫 4f(버튼 퇴장). 사람 지시: 언급 안 한 스냅은 삭제, 영상이 짧아져도 됨.
- 이음 (지금 표에 있던 방식 안에서 고름):
  - S4 → S5: 같은 카드가 같은 자리에 있으므로 옛 S10의 "버튼 퇴장 + 카드 등장"을 빼고 바로 진행 바를 채운다.
  - S5 → S6: 옛 S5 빠지기 그대로. 100% 부품이 50% 홈 이미지로 바뀌는 차이는 사람 결정으로 둔다.
  - S9 → S10: 뛰어들기 끝의 `button-submit` 부품을 나가는 쪽으로 보고 04 폰과 화면 교체(겹침 4f). 옛 S12의 "배지 퇴장" 자리에 버튼이 들어간 것.
  - S10 → S11 → S12: 사람 결정대로 폰 `motion-exit` + `video-end-bg` · 두 줄 `motion-enter`(겹침 4f). 첫 아래 줄 "적용 사례 정리하기"가 S11에서 들어와 S12의 첫 `hold-glance`로 이어진다.
- S13 엔드 카드: 한 줄(단어 + 로고) → 세 줄(단어 / 로고 / 서브), 간격 1↔2 `video-space-small` · 2↔3 `video-space-section` (사람 결정).
- 빠진 R: R8(모양 바뀜) · R13(버튼 단독 클로즈업) · R14(버튼 펼쳐짐 대체) · R17(배지 점에서 커짐) · R20(부품이 커져 어두운 장면이 됨, 화면 교체로 바뀜). R18은 수정 1에서 이미 뺐다. 22 → 17 / 23.
- 총 길이 597 → 537f.
- S11 바탕 확인 (사람 결정): `video-end-bg` 바탕은 크기 변화 없이 투명 → 불투명만 (`duration-6` · `curve-enter`), 크기 작게 → 1은 두 줄에만 건다. S9 → S10 이음은 승인.

### 수정 3 (S11 · S12, 글자 타자 패턴 반영)

- motion.md 3장 src/screens "글자 타자"(새 후보 ⑧, 사람 승인: 글자 등장 0f · 간격 `hold-tick` · 줄 사이 `hold-glance`)를 S12에 썼다.
- S11: 폰 `motion-exit` + `video-end-bg` 바탕 투명 → 불투명(`duration-6` · `curve-enter`)만. 두 줄은 S11에서 나오지 않는다. 길이 6f 그대로.
- S12: 윗줄 타자 → `hold-glance` → 아랫줄 "적용 사례 정리하기" 타자 → `hold-read` → 아랫줄 `motion-exit` → 아랫줄 "내 자산에 등록됐어요" 타자 → `hold-read` → 두 줄 `motion-exit`. 롤(`motion-swap`)과 중간 문구("결과물 파일 첨부" · "결과물 제출" · "승인 완료")는 뺐다. 88 → 148f.
- 글자 수 세는 법(장면표에 적음): 한글 · 쉼표는 한 글자, 띄어쓰기는 세지 않음. 6 · 8 · 9자. 셋째 줄 타자는 둘째 줄 퇴장(4f)이 끝난 뒤 시작한다.
- S13 시작 459 → 519f. 총 길이 537 → 597f.
- R21(아래 줄이 굴러 바뀜)이 빠져 17 → 16 / 23.
- 사람 확인: 띄어쓰기 안 셈 · 마지막 글자 프레임부터 쉼 · 셋째 줄은 둘째 줄 퇴장 뒤 시작은 그대로. 치는 동안 줄은 항상 가운데로 바꿈 (글자가 늘 때마다 쳐진 글자 묶음을 0f로 다시 가운데 정렬).
