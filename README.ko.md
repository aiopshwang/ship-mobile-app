# Ship Mobile App

[English](README.md)

[![skills.sh](https://skills.sh/b/aiopshwang/ship-mobile-app)](https://skills.sh/aiopshwang/ship-mobile-app)

![Ship Mobile App — 코드 한 조각이 아니라 실제 사용자 경로를 만드세요.](assets/social-card.svg)

**코드 한 조각이 아니라 실제 사용자 경로를 만드세요.**

Ship Mobile App은 Claude Code와 Codex에서 사용할 수 있는 오픈 Agent
Skill입니다. 코딩 에이전트가 모바일 앱이 실제로 무너지는 지점 — 도메인 의미,
로컬·서버 상태, 오프라인 동작, 앱 생명주기, 네이티브 설정, 서명된 산출물,
사용자에게 표시하는 주장 — 까지 검증하도록 만듭니다.

특정 아키텍처를 강제하지 않고 Flutter, React Native, 네이티브 iOS·Android에
적용합니다.

## 왜 필요한가

모바일에서는 컴파일되고, 테스트를 통과하고, 디버그 빌드에서 잘 도는 코드도
사용자를 배신할 수 있습니다.

- 오프라인 저장이 실제 커밋과 똑같은 `저장됨`을 보여주고는 프로세스와 함께
  사라진다.
- 대기 중이던 쓰기가 그 순간 로그인된 계정 이름으로 전송된다.
- 권한이 디버그 소스셋에는 있지만 서명된 릴리스에는 빠져 있다.
- "완료" 보고가 실제로 관찰한 것보다 더 많은 것을 주장한다.

대부분의 에이전트 워크플로는 "테스트 통과"에서 멈춥니다. 이 스킬은 그 이후의
모든 층위에 대해 에이전트가 정직하도록 붙잡습니다.

## 다섯 가지 진실의 경계

모든 요청은 실제로 건드리는 경계에 대해서만 점검합니다.

| 경계 | 확인할 질문 |
|---|---|
| 도메인 | 데이터의 의미가 화면 라벨과 실제 동작에 맞는가? |
| 상태 | 낙관적·대기·커밋·오래됨·실패 상태를 구별하는가? |
| 생명주기 | 콜드스타트·복귀·백그라운드·권한·계정 전환에서 유지되는가? |
| 플랫폼 | 실제 서명된 산출물에 필요한 설정이 들어 있는가? |
| 주장 | UI·AI·개인정보·배포 보고가 관찰한 사실보다 앞서지 않는가? |

스킬은 다음 실제 경로를 따라갑니다.

```text
사용자 행동 -> UI -> 도메인 로직 -> 저장/동기화
            -> 네이티브·외부 서비스 -> 서명된 산출물 -> 사용자 결과
```

모든 체크리스트를 기계적으로 적용하지 않고, 요청한 작업이 실제로 통과하는
경계만 선택합니다.

## Claude Code와 Codex에 설치

현재 프로젝트에 함께 설치:

```bash
npx skills add aiopshwang/ship-mobile-app --skill ship-mobile-app -a claude-code -a codex
```

모든 프로젝트에서 사용하려면 `--global`을 추가합니다.

```bash
npx skills add aiopshwang/ship-mobile-app --skill ship-mobile-app --global -a claude-code -a codex
```

| 호스트 | 직접 호출 | 프로젝트 설치 위치 |
|---|---|---|
| Claude Code | `/ship-mobile-app` | `.claude/skills/ship-mobile-app` |
| Codex | `$ship-mobile-app` | `.agents/skills/ship-mobile-app` |

사용 예:

```text
Ship Mobile App을 사용해서 이 오프라인 저장 기능을 구현하고,
계정 전환·콜드스타트·서명된 릴리스 빌드까지 검증해줘.
```

두 호스트 모두 작업이 설명과 일치할 때 스킬을 자동으로 선택할 수도 있습니다.
이 패키지는 [Claude Code](https://code.claude.com/docs/en/skills)와
[Codex](https://learn.chatgpt.com/docs/build-skills)가 지원하는 열린 Agent
Skills 형식을 따릅니다.

## 적합한 작업

- UI·저장소·백엔드·네이티브 계층을 가로지르는 모바일 기능
- 오프라인 저장, 동기화, 오래된 상태, 계정 전환
- 인증, 딥링크, 알림, 백그라운드, 위젯, 권한, AI 기능
- 화면 제약·생명주기·릴리스·실기기에서만 나타나는 버그
- 릴리스 후보와 근거 기반 스토어 전달 준비

코드 조각 설명, 단순 스타일 변경, 웹·서버 전용 작업, 아이디어 브레인스토밍,
스토어 마케팅 문구만 작성하는 작업에는 사용하지 않습니다.

## 구성

```text
skills/ship-mobile-app/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── boundary-checks.md
    ├── failure-patterns.md
    └── verification-ladders.md
```

- `SKILL.md`: 핵심 작업 방식
- `boundary-checks.md`: 시간·상태·계정·생명주기·플랫폼·AI·운영 경계
- `verification-ladders.md`: 소스·테스트·산출물·기기·원격 상태를 구분하는 증거 단계
- `failure-patterns.md`: 실제 시행착오를 일반화한 익명 합성 진단 사례

## 검증과 한계

Ship Mobile App은 초기 공개 프리뷰입니다. 공개 전에 다음 검증을 통과했습니다.

- 오픈 `skills` CLI의 구조 검증과 단일 스킬 검색
- Claude Code·Codex 교차 설치 확인과 한 차례의 제한된 Claude Code 실제 호출
- 긍정·부정 프롬프트 8건에 대한 트리거 라우팅 확인
- 독립 합성 평가 3건: 소규모 Dart 픽스처 2건(오프라인 저장·계정 전환 결함,
  로컬 날짜 계산 결함)과 읽기 전용 Android 디버그/릴리스 설정 진단 1건

각 검증에서 실제로 관찰한 내용과 아직 검증하지 않은 경계는
[EVALS.md](EVALS.md)에 기록했습니다. 이는 스킬 자체의 개발 증거이지 벤치마크가
아닙니다. 모든 에이전트·프레임워크·기기·백엔드·스토어에서 생산성, 정확성,
앱 성공률이 보편적으로 향상된다는 증거가 아닙니다.

## Goal to Proof와의 관계

두 스킬은 상호 보완적이며 서로 독립적입니다.

- **Ship Mobile App**은 모바일 앱 개발에 특화된 판단과 검증 방법을 담당합니다.
- **Goal to Proof**는 도메인과 무관한 완료 검증을 담당합니다.

서로 독립적으로 쓸 수 있으며 함께 설치해야 하는 의존성은 없습니다.

## 유래·개인정보·보안

실제 크로스플랫폼 소비자 앱을 출시·운영하며 반복해서 만난 실패 형태에서
작업 방식을 추출했습니다. 원문 대화, 비공개 코드, 사용자 데이터, 인증정보,
내부 경로, 프로젝트 식별정보는 포함하지 않았습니다. 모든 사례는 합성·일반화했습니다.

[PRIVACY.md](PRIVACY.md)와 [SECURITY.md](SECURITY.md)를 참고하세요. 재현 가능한
오작동 트리거나 빠진 모바일 경계는 GitHub Issue로, 보안 문제는 비공개 취약점
신고 기능으로 알려주세요.

## aiopshwang 스킬 패밀리

함께 쓰기 좋은 독립 Agent Skill들:

- [goal-to-proof](https://github.com/aiopshwang/goal-to-proof) — 범용 완료 게이트: 승인된 작업을 끝까지 수행하고 결과를 증명.
- [verify-regression-tests](https://github.com/aiopshwang/verify-regression-tests) — 회귀 테스트가 의도한 결함을 실제로 잡는지 증명.
- [data-analysis-ml-agent-skills](https://github.com/aiopshwang/data-analysis-ml-agent-skills) — 의사결정 수준 데이터 분석·ML: 감사, 누수 안전 실험, 검증, 재현 가능한 인계.
- [fresh-eyes-check](https://github.com/aiopshwang/fresh-eyes-check) — 맥락 없는 다른 모델이 예전 지시가 지금도 맞는지 확인한 뒤 행동.

## 라이선스

MIT © `aiopshwang`.
