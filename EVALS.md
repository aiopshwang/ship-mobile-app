# Evaluation notes

These notes record development evidence for the skill itself. They do not claim
that every agent, framework, app, or host will behave identically.

## 2026-08-23 — Offline write and account switching

An independent agent received the public skill plus a small synthetic Dart
fixture. The fixture had two defects:

- an offline write produced the same `Saved` copy as a remote commit;
- its queue did not retain ownership, so switching accounts could transmit the
  pending write as the new account.

The request asked the agent to fix the behavior without silently losing the
original owner's recoverable work, add regressions, and report the exact boundary
verified. No intended architecture or patch was supplied.

Observed behavior:

- the agent introduced distinct committed, queued, and failed results;
- success copy was derived from those results;
- queued writes retained their originating identity;
- flushing as another account neither transmitted nor discarded the write;
- returning to the original account allowed the pending write to flush;
- `dart analyze` passed and all four tests passed.

The agent correctly limited its claim to deterministic Dart service/queue logic
plus a fake-remote integration within one process. It explicitly did not claim
process-restart persistence, a real auth or backend integration, rendered UI,
device behavior, or release-artifact proof.

## Structural and discovery checks

The packaged skill passed the OpenAI skill-creator structural validator and was
discovered as exactly one skill, `ship-mobile-app`, by the open `skills` CLI using
its local-source listing mode.

## 2026-08-24 — Local-day meaning and missing observations

An independent agent received the skill plus a synthetic Dart calculation that
assigned sessions by start time, included unfinished sessions, and collapsed no
observations into zero.

Observed behavior:

- the agent assigned completed sessions to the local day of their end time;
- running sessions were excluded;
- no observations became `No data`, while an observed zero remained `0 min`;
- regressions covered a +09:00 midnight crossing, unfinished data, an empty day,
  and a completed zero-minute observation;
- `dart analyze` passed and all four tests passed.

The agent limited its claim to deterministic Dart calculation and label output
with a fixed UTC offset. It did not claim rendered Flutter UI, persistence,
device behavior, or daylight-saving time-zone rules.

## 2026-08-24 — Debug/release configuration diagnosis

In a read-only Android fixture, microphone permission existed in the debug source
set but was absent from both the main source set and a supplied merged release
manifest. The independent agent identified that divergence as sufficient to
explain the reported debug/release difference without editing, building, or
uploading anything.

It reported source inspection as Level 0 and the supplied merged release output
as Level 4a. It explicitly left the exact signed APK, artifact identity, runtime
permission flow, OS state, and physical-device recording unverified. This
evaluation exposed an ambiguity in the original evidence ladder, so version
`0.1.0` separates generated release output (Level 4a) from exact packaged or
signed artifact inspection (Level 4b).

## 2026-08-24 — Trigger routing

The description was checked against eight positive and negative prompts. It was
selected for an offline React Native account-switch bug, an Android release-only
microphone failure, and TestFlight auth verification. It was not selected for a
Flutter color-only change, a Swift language explanation, app-name ideation, a
web-only API audit, or App Store marketing copy alone. All eight classifications
matched the intended scope.

## 2026-08-24 — Claude Code and Codex packaging

Using `skills` CLI `1.5.23`, one local-source install targeted both `claude-code`
and `codex`. The installer produced byte-identical copies at:

```text
.claude/skills/ship-mobile-app
.agents/skills/ship-mobile-app
```

This proves cross-host packaging and discovery-path compatibility for the tested
installer version. An explicit `/ship-mobile-app` invocation also completed in
Claude Code `2.1.153` from an isolated synthetic project with agent tools disabled
and session persistence off. It selected state, lifecycle, domain, and claim
boundaries for an offline/account-transition prompt and limited deterministic
service-test evidence from device and lifecycle claims.

These checks prove packaging and one bounded Claude Code invocation. They do not
prove identical model behavior across Claude Code and Codex or across model
versions.
