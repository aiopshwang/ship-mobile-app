# Public launch kit

## GitHub repository description

> An open Agent Skill for Claude Code and Codex to build, debug, and prepare production mobile apps across domain, state, lifecycle, native platform, signed artifact, and user-claim boundaries. Framework-neutral for Flutter, React Native, iOS, and Android.

## GitHub topics

```text
agent-skills
ai-coding
coding-agents
claude-code
codex
mobile-app-development
cross-platform
flutter
react-native
ios
android
developer-tools
```

## First release

Title:

> Ship Mobile App v0.1.0 — Initial Public Preview

Release notes:

````markdown
Ship Mobile App is an instruction-only Agent Skill for Claude Code and Codex. It
helps coding agents carry non-trivial mobile work through five truth boundaries:
domain, state, lifecycle, platform, and user-facing claims.

### Included

- A framework-neutral workflow for Flutter, React Native, native iOS, and Android
- Boundary checks for time, identity, offline state, sync, permissions, native
  configuration, AI behavior, and release delivery
- Evidence ladders that distinguish source, tests, merged release output, exact
  signed artifacts, devices, provider state, and store availability
- Synthetic failure patterns for diagnosing cross-boundary mobile defects
- Progressive `SKILL.md` packaging for Claude Code and Codex

### Install

```bash
npx skills add aiopshwang/ship-mobile-app --skill ship-mobile-app -a claude-code -a codex
```

Use `/ship-mobile-app` in Claude Code or `$ship-mobile-app` in Codex. Both hosts
may also select it automatically when a task matches its description.

### Evidence and limitations

The package passed structural validation, cross-host installation checks, a
bounded Claude Code invocation, an eight-prompt trigger-routing check, and three
synthetic mobile scenarios evaluated independently from the authoring pass. The
scenarios cover offline account-owned writes, local-day/missing-data semantics,
and debug/release configuration diagnosis.

This evidence does not establish universal performance across agents, frameworks,
devices, backends, or stores. Physical-device and store-delivery behavior were
not evaluated for this release.

MIT licensed.
````

## English launch post

````markdown
A mobile change can pass its tests and still fail one boundary later.

“Saved” may mean only optimistic. An offline write may outlive the account that
created it. A cold start may restore stale state. A debug build may hide missing
native configuration. UI or AI copy may claim more than the app observed.

Today I’m releasing **Ship Mobile App v0.1.0**, an open Agent Skill for Claude
Code and Codex.

It helps coding agents trace non-trivial mobile work across five boundaries:

- domain meaning;
- local and server state;
- app lifecycle;
- native platform and signed artifacts;
- truthful user-facing claims.

It is framework-neutral and designed for Flutter, React Native, native iOS, and
Android. It does not choose an architecture for you or turn every task into a
release project. It focuses on the boundaries touched by the requested user path.

Install for both hosts:

```bash
npx skills add aiopshwang/ship-mobile-app --skill ship-mobile-app -a claude-code -a codex
```

Claude Code: `/ship-mobile-app`

Codex: `$ship-mobile-app`

The evidence is intentionally bounded and published in `EVALS.md`; this is not a
universal productivity or success-rate claim.

[github.com/aiopshwang/ship-mobile-app](https://github.com/aiopshwang/ship-mobile-app)

Feedback on false triggers, missing boundaries, and reproducible mobile failure
cases is welcome.
````

## Korean launch post

````markdown
모바일 앱 변경은 테스트를 통과하고도 한 경계 뒤에서 실패할 수 있습니다.

화면의 “저장 완료”가 실제로는 낙관적 상태일 수 있고, 오프라인 기록이 생성한
계정과 분리될 수 있습니다. 콜드스타트에서 오래된 상태가 되살아날 수 있고,
디버그 빌드는 정상인데 서명된 산출물에는 네이티브 설정이 빠질 수도 있습니다.

오늘 **Ship Mobile App v0.1.0**을 공개합니다.

Claude Code와 Codex에서 사용하는 오픈 Agent Skill로, 비단순 모바일 작업을
다음 다섯 가지 경계까지 추적합니다.

- 도메인 의미
- 로컬·서버 상태
- 앱 생명주기
- 네이티브 플랫폼과 서명된 산출물
- 사용자에게 표시하는 주장의 정직성

Flutter, React Native, 네이티브 iOS·Android를 대상으로 하며 특정 아키텍처를
강제하지 않습니다. 모든 체크리스트를 기계적으로 적용하지 않고 요청한 사용자
경로가 통과하는 경계만 선택합니다.

두 호스트에 함께 설치:

```bash
npx skills add aiopshwang/ship-mobile-app --skill ship-mobile-app -a claude-code -a codex
```

Claude Code: `/ship-mobile-app`

Codex: `$ship-mobile-app`

검증 범위와 한계는 `EVALS.md`에 공개했습니다. 모든 앱이나 에이전트의 생산성·
성공률 향상을 주장하지 않습니다.

[github.com/aiopshwang/ship-mobile-app](https://github.com/aiopshwang/ship-mobile-app)

잘못 작동하는 트리거, 빠진 경계, 재현 가능한 모바일 실패 사례에 대한 피드백을
기다립니다.
````
