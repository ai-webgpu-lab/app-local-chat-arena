# app-local-chat-arena

`로컬 채팅 런타임 비교`를 실제 사용자 흐름으로 묶어 보여주는 통합 데모 저장소입니다. 여러 baseline을 하나의 사용 시나리오로 연결해 실험 결과가 제품 UX로 이어질 수 있는지 확인합니다.

## 저장소 역할
- 실험과 벤치 결과를 실제 사용자 플로우로 조합합니다.
- 조직 외부에서도 상태를 이해할 수 있는 데모 surface를 제공합니다.
- 각 기능 조합에서 병목, 실패 지점, UX 리스크를 조기에 드러냅니다.

## 핵심 질문
- 개별 baseline을 묶었을 때 사용자 관점에서 충분히 동작하는가
- 성능과 품질이 UX 수준에서 허용 가능한가
- 어떤 실험/벤치 결과가 실제 통합 제품 설계에 가장 큰 영향을 주는가

## 포함 범위
- 핵심 사용자 시나리오 1~2개 구현
- 필요한 baseline/모델/유틸 조합
- 데모 운영에 필요한 최소 상태 관리와 결과 보고

## 비범위
- 제품 출시 수준의 완성도, 인증, 결제, 운영 백엔드
- 광범위한 기능 확장
- 원인 분리가 어려운 ad hoc 통합

## 기본 구조
- `src/` - 구현 코드 또는 baseline 프로토타입
- `public/` - GitHub Pages baseline probe 또는 실제 정적 데모 산출물
- `reports/raw/` - 원시 측정 결과 JSON/CSV/로그
- `reports/screenshots/` - 시각 결과 스크린샷
- `reports/logs/` - 실행 로그와 디버깅 산출물
- `schemas/ai-webgpu-lab-result.schema.json` - 공통 결과 스키마
- `RESULTS.md` - 핵심 결과 요약과 해석

## 메타데이터
- Track: Integration
- Kind: integration
- Priority: P1

## 현재 상태
- Repository scaffold initialized
- Shared result schema copied to `schemas/ai-webgpu-lab-result.schema.json`
- Shared reporting template copied to `RESULTS.md`
- Repo-specific Pages baseline copied from `repo-scaffolds/repos/app-local-chat-arena/`
- Generated entry point updated in `public/index.html` and related assets
- GitHub Pages workflow copied to `.github/workflows/deploy-pages.yml`

## 현재 baseline 상태
- Repository-specific runnable baseline active: local chat arena demo with pairwise synthetic runtime battle, shared prompt input, and app-level scoreboard export
- Generated override source: `repo-scaffolds/repos/app-local-chat-arena/`
- Results/report scaffold is ready to promote exported JSON into `reports/raw/` and `RESULTS.md`

## GitHub Pages 운영 메모
- Pages URL: https://ai-webgpu-lab.github.io/app-local-chat-arena/
- 기본 bootstrap workflow는 `public/` baseline probe 정적 artifact를 배포합니다.
- 실제 빌드가 필요한 저장소는 install/build 단계와 artifact 경로를 저장소 사양에 맞게 교체해야 합니다.

## 조직 상태 대시보드
- 전체 Pages/demo 상태는 `docs-lab-roadmap/docs/PAGES-STATUS.md`에서 확인합니다.
- 이 저장소의 live demo는 `https://ai-webgpu-lab.github.io/app-local-chat-arena/`입니다.
- 통합 sketch/adapter 상태는 `docs-lab-roadmap/docs/INTEGRATION-STATUS.md`에서 확인합니다.
- sketch capabilities는 `docs-lab-roadmap/docs/SKETCH-METRICS.md`에서 확인합니다.

## 측정 및 검증 포인트
- end-to-end latency와 사용자 상호작용 응답성
- load/cache behavior와 세션 지속성
- 통합 시 발생하는 오류 흐름과 fallback UX

## 산출물
- 사용자 흐름을 보여주는 runnable demo
- 통합 결과 요약과 known issues
- GitHub Pages 또는 별도 정적 surface에서 확인 가능한 설명 페이지

## 작업 및 갱신 절차
- `src/` 아래에 첫 runnable baseline 또는 비교 harness를 구현합니다.
- 실제 사용 스택이 정해지면 이 README에 install/dev/build/test 명령을 추가합니다.
- 측정 결과는 `reports/raw/`와 `RESULTS.md`에 함께 반영합니다.
- 브라우저, OS, 디바이스, cache, worker 여부 등 재현 조건을 결과와 같이 기록합니다.
- Pages를 유지하는 경우 baseline probe 또는 workflow를 실제 저장소 동작에 맞게 교체합니다.

## 완료 기준
- 핵심 사용자 흐름이 끝까지 재현됩니다.
- 통합 리스크와 병목이 README/RESULTS에 정리되어 있습니다.
- 관련 실험/벤치 저장소와 연결 관계가 문서화되어 있습니다.

## 관련 저장소
- 관련 `exp-*` 저장소 - 개별 baseline 출처
- 관련 `bench-*` 저장소 - 통합 전에 확보한 비교 결과
- `shared-webgpu-capability`, `shared-bench-schema`, `docs-lab-roadmap`

## 라이선스
MIT
