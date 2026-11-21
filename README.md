# Speak Daily · 영어 스피킹 웹앱

스픽(Speak) 3단계 학습법을 따라가는 모바일 영어 스피킹 학습 웹앱입니다.
핵심 패턴 학습 → 패턴 변형 연습 → 실전 롤플레이 순서로 하루 분량을 진행합니다.
배포 주소: https://danielsonghoon-sketch.github.io/speak-english/

## 코스와 자료 출처

- 트랙 A 비즈니스 실무 영어 29일 · 트랙 B 비즈니스 회사생활 영어 28일 · 트랙 C(원어민처럼 스피킹 중급 1~3탄, 구동사 격파 1~2탄) 137일 — **총 194 Day**.
- 각 Day의 **핵심 문장(오늘의 패턴)과 뜻은 실제 스픽 커리큘럼의 Day 문장**입니다. 레슨 STEP 1에 `스픽 실제 Day 문장` 표시와 출처 링크가 붙습니다.
- **패턴 변형 연습과 실전 롤플레이는 보충 연습**입니다. 스픽 유료 앱 안의 회차·변형 문장은 외부에서 열람할 수 없어, 그 Day의 주제와 패턴에 맞춰 새로 만들었습니다. STEP 2·3에 `보충 연습` 표시가 붙습니다.
- 코스별 전체 출처 목록은 앱의 **기록 탭 → 자료 출처**에서 볼 수 있습니다.
- 2026-11-21 194일 전수 점검에서 나온 오류·어색한 표현을 반영했습니다. 뜻이 틀리거나 원어민이 쓰지 않는 표현이던 16개 Day의 핵심 문장은 자연스러운 표현으로 다듬었고(예: C4 D5 `make away with` → `get rid of`), 고친 목록은 `english-study/sources/speak-day-lists.md`의 「앱에서 다듬은 핵심 문장」에 있습니다.

## 앱으로 설치하기 (PWA)

- **안드로이드(크롬·삼성 인터넷)**: 주소를 연 뒤 브라우저 메뉴에서 **앱 설치**(또는 홈 화면에 추가)를 누르면 주소창 없는 앱으로 열립니다.
- **아이폰(사파리)**: 공유 → **홈 화면에 추가**.
- 앱 이름·아이콘·시작 주소는 `manifest.json`에서 정합니다(`start_url`/`scope` = `/speak-english/`, `display` = `standalone`).
- 한 번 열어 두면 `sw.js` 서비스 워커가 화면과 아이콘을 기기에 저장해 두어 **인터넷이 없어도 마지막으로 받은 버전이 열립니다.** 새 버전은 열 때마다 네트워크에서 먼저 확인하고, 바뀐 게 있으면 캐시를 새로 받습니다.
- 음성 인식(말하기 연습)은 HTTPS(또는 localhost)에서만 동작합니다.

## 학습 기록 백업·복원

- 설정(톱니바퀴) → **학습 기록 백업** → `파일로 저장`(JSON 파일 내려받기) 또는 `JSON 복사`.
- **학습 기록 복원** → 백업 파일을 고르거나, 복사해 둔 JSON을 붙여넣고 복원.
- 복원 전에 지금 기록과 백업 내용(완료 일수·연속 일수)을 보여 주고 한 번 더 확인합니다. 복원하면 지금 기록은 백업 내용으로 바뀝니다.
- 백업 파일에는 완료한 Day, 날짜별 학습량, 연속 일수, 화면 설정이 들어갑니다. **OpenAI API 키는 백업에 포함되지 않고**, 복원해도 기기에 저장된 키는 그대로 유지됩니다.
- 학습 상태는 그 브라우저의 localStorage(`speakdaily.v1`)에만 저장됩니다. 브라우저 기록을 지우면 사라지므로 그 전에 백업해 두세요.

## OpenAI API 키 (선택)

- 실전 롤플레이의 AI 프리토킹과 교정에만 씁니다.
- 설정에 키를 넣으면 브라우저가 `https://api.openai.com/v1/chat/completions`(모델 `gpt-4o-mini`)로 **직접** 요청합니다. 이 앱에는 서버가 없고, 키는 그 기기 브라우저의 localStorage에만 저장되며 어디로도 전송되지 않습니다.
- 사용료는 키 주인의 OpenAI 계정에 청구됩니다. 공용 기기에서는 키를 저장하지 말고, 노출되었다면 OpenAI에서 폐기하세요.

## 구성

- `index.html` — 앱 전체(HTML·CSS·JS·194일 학습 데이터)가 들어 있는 단일 파일. 외부 라이브러리가 없고, AI 프리토킹을 쓸 때만 `api.openai.com`으로 요청합니다.
- `manifest.json` — 앱 이름, 아이콘, 시작 주소·범위, standalone 표시, 테마 색.
- `sw.js` — 오프라인 캐시. 앱 화면은 네트워크 우선, 아이콘·매니페스트는 캐시 우선이며 캐시 이름에 빌드 해시가 붙어 새 빌드에서 자동으로 갈아끼웁니다.
- 아이콘 — `icon-192.png`, `icon-512.png`, `icon-maskable-192.png`, `icon-maskable-512.png`, `apple-touch-icon.png`, `favicon-32.png`.

## 갱신 방법

원본은 `english-study/`에서 관리합니다. 실제 스픽 Day 목록과 대조 근거는 `english-study/sources/speak-day-lists.md`에 있습니다.

1. `english-study/src/` 수정 → `python3 english-study/build.py`
   (데이터 검증 + `speak-webapp.html` 빌드 + 이 저장소의 `index.html`·`manifest.json`·`sw.js`·아이콘 갱신)
2. `ALL_DAYS=1 WITH_SR=1 node english-study/test/dom-smoke.js` 로 동작 확인 (node가 없는 환경에서는 `python3 english-study/test/data-smoke.py`)
3. 이 폴더에서 커밋·푸시하면 GitHub Pages가 자동으로 다시 배포합니다.
