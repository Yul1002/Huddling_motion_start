# CLAUDE.md

허들링 클럽 서비스 화면으로 모션 영상을 만드는 프로젝트. 영상은 HyperFrames로 만든다 (`/hyperframes`).
"모션 만들자"라고 하면 `/make-video` 스킬로 시작한다.

## 바뀌는 것 · 고정된 것

| | 무엇 | 어디 |
|---|---|---|
| **바뀜** (영상마다) | BRIEF · 레퍼런스 | `out/<영상이름>/BRIEF.md` · `references/` |
| **고정** | 색 · 글자 · 크기 | `docs/design.md` · `docs/video.md` |
| **고정** | 길이 · 곡선 · 머무는 시간 · 카메라 | `docs/motion.md` |
| **고정** | 화면 · 부품 · 그림 · 로고 · 폰트 파일 | `src/screens` · `src/parts` · `src/assets` |

- 영상을 만드는 중에는 `docs/` · `src/`를 고치지 않는다. 고쳐야 하면 멈추고 사람에게 묻는다.
- 레퍼런스에서는 **구성 · 구도 · 카메라 · 전환 · 글자 배치**만 참조한다. 색 · 글자(폰트) · 로고 · 숫자는 가져오지 않는다.
- 레퍼런스가 여러 개면 **뼈대는 하나**(장면 흐름 · 길이), 나머지는 한 가지씩 부분 역할을 맡는다.
- docs에 없는 숫자가 필요하면 쓰지 말고 `docs/motion.md` "새 후보" 방식으로 묻는다.

## 기준 문서 (내용은 각 문서를 본다)

- `docs/design.md`: 1장 색 · 2장 글자 · 3장 폰트 로드 · 4장 간격 · 그림자 · 6장 부품 · 화면 목록
- `docs/motion.md`: 1장 Primitives · 2장 Semantic · 3장 Pattern · 4장 머무는 시간 · 5장 카메라 · 새 후보
- `docs/video.md`: 1장 최소 글자 · 2장 배경 · 3장 글자 · 4장 폰 프레임 · 5장 parts

## 역할 (`.claude/agents/`)

art-director(레퍼런스 정리) → director(장면표) → builder(스냅보드 · 영상) → critic(판정만).
순서 · 승인 · 게이트는 `.claude/skills/make-video/SKILL.md`.

## 폴더

- `references/`: 받은 레퍼런스 파일은 여기에만 둔다.
- `out/<영상이름>/`: 영상 한 편의 BRIEF와 모든 결과물.
