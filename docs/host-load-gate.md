# 호스트 로드 수동 게이트

CI의 pluginval/auval 통과는 호스트 로드를 증명하지 않는다. 릴리스 태그를
만들기 전에 실제 호스트에서 한 번 검증한다.

## 절차

1. Release 빌드 산출물을 설치 위치에 복사한다.
   - VST3: `~/Library/Audio/Plug-Ins/VST3/`
   - AU: `~/Library/Audio/Plug-Ins/Components/` (auval은 CI가 이미 수행)
2. REAPER에서 해당 플러그인을 로드하고 간단히 렌더한다.
   - 파라미터 자동화 한 번, 프로젝트 저장 후 재오픈해 상태 복원 확인.
3. Ableton Live에서도 동일하게 로드 확인.
4. 증거를 기록한다. 아래 항목이 없으면 증거로 인정하지 않는다:
   - 설치 바이너리의 SHA256
   - 호스트 이름과 버전
   - 샘플레이트, 버퍼 크기
   - 확인 일시

## 증거 기록 위치

제품 저장소의 `docs/` 또는 릴리스 PR 본문에 위 항목을 남긴다.
측정 불가한 항목은 추정으로 채우지 않고 `unavailable`로 명시한다.

## 참고

- 포터블 검증 스크립트 템플릿: 로컬 `audio-knowledge` 저장소의
  `validation/validate_vst3_au.sh` (pluginval + auval 러너).
- self-hosted 러너 `eon-mac`에서도 동일 절차를 잡으로 자동화할 수 있다 —
  REAPER/Live가 설치된 머신이므로 가능. 자동화는 릴리스 단계에서 검토.
