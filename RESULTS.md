# Results

## 1. 실험 요약
- 저장소: app-local-chat-arena
- 커밋 해시: a813762
- 실험 일시: 2026-05-20T15:34:18.580Z -> 2026-05-20T15:34:23.385Z
- 담당자: ai-webgpu-lab
- 실험 유형: `integration`
- 상태: `success`

## 2. 질문
- 하나의 앱 surface에서 두 local-chat profile을 같은 prompt budget으로 비교할 수 있는가
- winner summary와 세부 메트릭이 앱 결과 문서에 동시에 남는가
- benchmark-only surface에서 demo-ready arena로 승격할 최소 기준을 만들 수 있는가

## 3. 실행 환경
### 브라우저
- 이름: Chrome
- 버전: 147.0.7727.15

### 운영체제
- OS: Linux
- 버전: unknown

### 디바이스
- 장치명: Linux x86_64
- device class: `desktop-high`
- CPU: 16 threads
- 메모리: 32 GB
- 전원 상태: `unknown`

### GPU / 실행 모드
- adapter: arena-profile-driven
- backend: `webgpu`
- fallback triggered: `false`
- worker mode: `mixed`
- cache state: `warm`
- required features: ["shader-f16"]
- limits snapshot: {}

## 4. 워크로드 정의
- 시나리오 이름: Local Chat Arena
- 입력 프로필: prompt-21-output-52
- 데이터 크기: arena-fast:ttft=17.3,decode=228.77,turn=331.1; arena-steady:ttft=21.2,decode=215.23,turn=328.1; automation=playwright-chromium, arena-fast:ttft=17.2,decode=220.25,turn=334.6; arena-steady:ttft=23.1,decode=211.81,turn=334.4; realAdapter=fallback(manifest fetch failed for https://ai-webgpu-lab.github.io/app-local-chat-arena/manifests/arena-v1.json); automation=playwright-chromium
- dataset: -
- model_id 또는 renderer: arena-fast
- 양자화/정밀도: -
- resolution: -
- context_tokens: 21
- output_tokens: 52

## 5. 측정 지표
### 공통
- time_to_interactive_ms: 882.8 ~ 1000.5 ms
- init_ms: 76.2 ~ 80.2 ms
- success_rate: 1
- peak_memory_note: 32 GB reported by browser
- error_type: -

### LLM / Benchmark
- ttft_ms: 17.2 ~ 17.3 ms
- prefill_tok_per_sec: 889.83 ~ 941.7 tok/s
- decode_tok_per_sec: 220.25 ~ 228.77 tok/s
- turn_latency_ms: 331.1 ~ 334.6 ms
- backends: webgpu
- fallback states: false

## 6. 결과 표
| Run | Scenario | Backend | Cache | Mean | P95 | Notes |
|---|---|---:|---:|---:|---:|---|
| 1 | Local Chat Arena | webgpu | warm | 228.77 | 17.3 | prefill=889.83 tok/s, metric=decode tok/s / TTFT ms |
| 2 | Local Chat Arena | webgpu | warm | 220.25 | 17.2 | prefill=941.7 tok/s, metric=decode tok/s / TTFT ms |

## 7. 관찰
- arena winner는 Local Chat Arena가 아니라 raw meta.notes에 기록된 profile 비교로 계산됐다.
- 앱 surface에서도 TTFT=17.3 ms, decode=228.77 tok/s를 바로 추적할 수 있게 됐다.
- playwright-chromium로 수집된 automation baseline이며 headless=true, browser=Chromium 147.0.7727.15.
- 실제 runtime/model/renderer 교체 전 deterministic harness 결과이므로, 절대 성능보다 보고 경로와 재현성 확인에 우선 의미가 있다.

## 8. Real Adapter vs Deterministic
- adapter: real=not-connected (no real adapter registered — falling back to deterministic), deterministic=deterministic-observatory
- decode tok/s: real=220.25, deterministic=228.77, delta=-8.52
- TTFT: real=17.2 ms, deterministic=17.3 ms, delta=-0.1 ms

## 9. 결론
- local chat arena demo가 generic probe를 벗어나 pairwise 비교 surface와 첫 raw result를 갖게 됐다.
- 다음 단계는 benchmark profile 대신 실제 local runtime providers를 같은 arena protocol에 연결하는 것이다.
- 내부 데모 승격을 위해 transcript quality와 session UX 메모를 추가로 기록해야 한다.

## 10. 첨부
- 스크린샷: ./reports/screenshots/01-local-chat-arena.png, ./reports/screenshots/02-local-chat-arena-real-chat-arena.png
- 로그 파일: ./reports/logs/01-local-chat-arena.log, ./reports/logs/02-local-chat-arena-real-chat-arena.log
- raw json: ./reports/raw/01-local-chat-arena.json, ./reports/raw/02-local-chat-arena-real-chat-arena.json
- 배포 URL: https://ai-webgpu-lab.github.io/app-local-chat-arena/
- 관련 이슈/PR: -
