# Huddling Motion Start

허들링 클럽 서비스 화면으로 모션 영상을 만드는 프로젝트. 영상은 [HyperFrames](https://hyperframes.heygen.com)(HTML → 영상)로 만들고, Claude Code 에이전트 네 명이 순서대로 나눠 맡는다.

## 만든 영상

| 파일 | 길이 | 설명 |
|---|---|---|
| `out/mission-flow/mission-flow.mp4` | 19.9초 (597f) | 미션 흐름 첫 버전: 홈 → 이번 달 미션 → 결과물 제출 → 승인 완료 |
| `out/mission-flow/mission-flow-v2.mp4` | 18.53초 (556f) | 장면 길이 조정판 (S2 · S3 · S7 · S8 · S9 · S13) |

1920×1080 · 30fps.

## 만드는 순서

Claude Code에서 "모션 만들자"라고 하면 `make-video` 스킬로 시작한다.

```
BRIEF → 레퍼런스 정리 → 장면표 [승인 1] → 스냅보드 [승인 2] → 영상
```

| 역할 | 하는 일 | 결과 |
|---|---|---|
| art-director | 레퍼런스에서 옮길 수 있는 것만 정리 | `refs.md` |
| director | 3안 요약 → 고른 안으로 장면표 | `scenes.md` |
| builder | 스냅보드(장면별 정지 화면) → HyperFrames 영상 렌더 | `snapboard/` · `project/` · `.mp4` |
| critic | 게이트 세 가지로 판정만 (고치지 않음) | `verdict.md` |

## 폴더

```
docs/          고정 기준: design.md(색 · 글자 · 간격) · motion.md(길이 · 곡선 · 카메라) · video.md(영상 크기 · 폰 프레임)
src/           고정 소스: screens(서비스 화면) · parts(부품 HTML) · assets(로고 · 폰트 · 그림)
references/    받은 레퍼런스 영상
out/<영상>/    영상 한 편의 BRIEF · refs · 장면표 · 스냅보드 · HyperFrames 프로젝트 · 결과 영상
.claude/       에이전트 4개 · make-video 등 스킬 · 미리보기 서버 설정(launch.json)
.agents/       HyperFrames 스킬 원본
CLAUDE.md      작업 규칙 (Claude Code가 읽음)
```

## 규칙 요약

- 영상마다 바뀌는 것은 BRIEF와 레퍼런스뿐. 색 · 글자 · 모션 값은 `docs/`, 화면 · 부품은 `src/`에서만 가져온다.
- 레퍼런스에서는 구성 · 구도 · 카메라 · 전환 · 글자 배치만 참조한다. 색 · 폰트 · 로고 · 숫자는 가져오지 않는다.
- docs에 없는 숫자가 필요하면 `docs/motion.md` "새 후보"에 올리고 사람에게 묻는다.

## 미리보기 · 렌더

```bash
cd out/mission-flow/project-preview
npx --yes hyperframes@0.8.198 preview --no-open --port 3003
npx --yes hyperframes@0.8.198 render -o ../mission-flow-v2.mp4
```
