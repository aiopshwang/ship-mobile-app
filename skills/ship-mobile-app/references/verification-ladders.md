# Verification ladders

Use the smallest set of checks that directly supports the claim. The levels below
are evidence boundaries, not a ritual sequence. A higher level does not replace a
lower-level invariant test when both protect different failure modes.

## Evidence levels

| Level | Evidence | What it can support | What it cannot support alone |
|---|---|---|---|
| 0 | Source and configuration inspection | Intended wiring, scope, likely cause | Runtime behavior |
| 1 | Static checks and deterministic unit/property tests | Logic, parsing, invariants, boundary values | Framework, storage, OS, or distribution integration |
| 2 | Repository, database, API, queue, or integration tests | Cross-component data and failure contracts | Native UI/services or signed release behavior |
| 3 | Rendered interaction and lifecycle tests | User flows, visual states, navigation, app transitions | OS-owned services or release artifact contents |
| 4a | Release build and generated-output inspection | Merged configuration, resolved resources, signing inputs | Contents of the exact distributed package or runtime behavior |
| 4b | Exact packaged or signed artifact inspection | Permissions, entitlements, identity, version, and embedded values in that immutable artifact | Real provider, device, or remote-store behavior |
| 5 | Emulator or physical-device exercise | Runtime behavior at the exercised device boundary | Other devices/accounts/store availability |
| 6 | Remote read-back or independent install | Backend/store/public state and installability | Universal correctness or untested user paths |

State exactly which level or sublevel was reached for each material claim. Do not
treat a merged manifest, generated project file, or signing plan as inspection of
the exact APK, AAB, IPA, or other package that users will receive.

## Minimum credible evidence by claim

### “The calculation is correct”

- define the metric frame and its label;
- test ordinary, boundary, missing, and adversarial values;
- test properties or cross-surface agreement when example tests could pass with
  the wrong meaning.

### “The record is saved”

- observe the durable state represented by that word;
- cover failure, retry, duplicate, and account boundaries;
- if only durably queued, call it queued rather than remotely saved;
- read back from the authority when remote persistence is the claim.

### “The UI bug is fixed”

- reproduce the original geometry, theme, keyboard, text scale, state, or race;
- exercise the real interaction, not only widget existence;
- inspect the final render and add a regression at the layer that failed.

### “Login works”

- exercise provider UI through callback, backend session, domain account, and
  relaunch on the intended build type;
- include cancellation or missing-provider-data behavior when it caused the bug;
- distinguish code/config validation from real provider completion.

### “Notifications or background behavior work”

- verify permission handling, latest-state scheduling, replacement/cancellation,
  delivery timing, tap entry, and stale content under the relevant lifecycle;
- a scheduling API return value does not prove OS delivery.

### “The release build is configured”

- build through the canonical release path;
- inspect merged/generated release output for required declarations and resolved
  values, and label that evidence as Level 4a;
- separately identify and inspect the exact immutable APK, AAB, IPA, or equivalent
  package for required permissions, entitlements, identity, version, environment,
  and hash, and label that evidence as Level 4b;
- run the high-risk path from that artifact when practical.

### “The build was uploaded or published”

- separate build/sign, transport, processing, review, rollout, and availability;
- query the remote system after the final action;
- identify the exact version/build/artifact and target track;
- do not infer publication from a CLI exit code or dashboard navigation.

### “Privacy or store declarations are accurate”

- trace actual data collection, local storage, network destinations, retention,
  deletion, and third-party SDK behavior;
- compare code, signed artifact, store metadata, privacy text, and exercised
  deletion/export paths as one contract.

## Release transaction

Only perform external release actions when they are in the user's authorized
scope. Before an authorized build/upload, capture:

```text
target platform and track
source branch + exact commit + dirty-worktree disposition
backend/migration/provider state
version/build and current remote maximum
production configuration source
signing identity and artifact destination
rollout order, compatibility, and rollback
```

Afterward, capture:

```text
exact immutable artifact identity or hash
artifact inspection results
install/launch/auth/core-flow result at the strongest available boundary
remote processing/review/availability state
remaining human/device checks
```

If upload transport fails after a valid signed artifact exists, first determine
whether the remote accepted it. Reuse the artifact for a safe transport retry when
the target system allows it; do not rebuild and change identity without cause.

## Mutation tests for critical guards

For a safety, authorization, missing-data, or release-config guard, a normal green
test can pass through an unrelated condition. Use mutation testing only when edits
are authorized and the mutation runs in a disposable isolated checkout or through
a test-only override, without production credentials, production network access,
or overlapping user changes. When the guard is load-bearing and the cost is
reasonable:

1. prove the intended negative fixture reaches that guard;
2. temporarily weaken or invert only that guard in the isolated check;
3. confirm the regression becomes red for the expected reason;
4. restore the implementation and confirm green.

Skip this method when isolation cannot be guaranteed. Verify the final diff and
rerun the restored guard before reporting completion; do not leave mutations in
the working tree. This is most useful when an accidental pass would justify
publication, a destructive action, or a high-stakes claim.

## Honest status language

- **Verified:** name the exact observation and boundary.
- **Partially verified:** state the proven layer and the next untested layer.
- **Not verified:** state the missing device, account, access, artifact, or remote
  state and the smallest next action.

Avoid “fully tested,” “production-ready,” or “works on iOS and Android” unless the
evidence genuinely covers the stated platforms, build types, and user paths.
