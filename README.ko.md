# Ship Mobile App

[English](README.md)

[![skills.sh](https://skills.sh/b/aiopshwang/ship-mobile-app)](https://skills.sh/aiopshwang/ship-mobile-app)

**코드 한 조각이 아니라 실제 사용자 경로를 만드세요.**

Ship Mobile App은 Claude Code와 Codex에서 사용할 수 있는 오픈 Agent
Skill입니다. 모바일 기능을 개발·디버깅·출시 준비할 때 도메인 의미, 로컬·서버
상태, 오프라인 동작, 앱 생명주기, 네이티브 설정, 서명된 산출물, 사용자에게
표시하는 주장의 정직성을 실제 경계까지 추적합니다.

특정 아키텍처를 강제하지 않고 Flutter, React Native, 네이티브 iOS·Android에
적용합니다.

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

## 다섯 가지 진실의 경계

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

`0.1.0`은 최초 공개 프리뷰입니다. 구조 검증, Claude Code·Codex 교차 설치,
독립 합성 시나리오 평가를 통과했습니다. 실제 결과와 검증하지 않은 경계는
[EVALS.md](EVALS.md)에 기록했습니다.

이 검증은 모든 에이전트·프레임워크·기기·백엔드·스토어에서 생산성, 정확성,
앱 성공률이 보편적으로 향상된다는 증거가 아닙니다.

## Goal to Proof와의 관계

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

## 라이선스

MIT © `aiopshwang`.
