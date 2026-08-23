# Recurring mobile failure patterns

These are anonymized synthetic patterns. Use them to select a hypothesis or a
regression boundary, not as proof that the current app has the same defect.

## Solution before user loop

**Symptom:** the requested screen exists, but it is placed in the wrong journey or
does not close the user's problem.

**Check:** restate the user scene, entry, action, success, recovery, return path,
and non-goals. Inspect whether existing components already cover part of the loop.

**Invariant:** architecture follows the user loop; a named UI is not automatically
the requested result.

## Breadth before the hard promise

**Symptom:** many peripheral features ship while the product's differentiating
behavior stays permanently “next.”

**Check:** identify the product promise and split its riskiest assumption into a
small vertical slice that can be exercised now.

**Invariant:** defer optional breadth, not the core promise merely because it
crosses difficult boundaries.

## Creation without return or recovery

**Symptom:** a user can create a record or post but cannot find, edit, undo, retry,
or receive a relevant response later.

**Check:** follow discover -> act -> confirm -> correct -> find again -> notify.

**Invariant:** an API write is not a closed product loop.

## Repeated visual guess fixes

**Symptom:** several style edits fail to repair text hidden by a keyboard or a
control that is untappable on a small device.

**Check:** reproduce exact viewport, insets, theme, text scale, content, overlay,
and parent constraints. Exercise the interaction in the rendered screen.

**Invariant:** diagnose the layout tree under the failing constraints before
tuning the nearest child.

## Green units, broken data path

**Symptom:** a new domain type passes its tests but pollutes timelines, analytics,
exports, notifications, or AI context after integration.

**Check:** trace create -> store -> sync -> query -> display -> aggregate -> export
-> notify -> delete.

**Invariant:** test at least one vertical path and the negative spaces touched by a
new concept.

## Queued announced as saved

**Symptom:** the UI says “saved” after an offline request, while a later retry may
still reject or drop it.

**Check:** inspect the write-state model, retry classifier, idempotency, owner
scope, undo behavior, and remote read-back.

**Invariant:** user-visible success is derived from observed write state:
committed, durably queued, retryable, or rejected are not synonyms.

## Missing observations treated as good news

**Symptom:** sparse logging is interpreted as an event disappearing or a metric
improving.

**Check:** window completeness, independent-day coverage, sample thickness,
polarity, and absence-versus-unobserved fixtures.

**Invariant:** missing data is not a negative fact, and positive copy cannot make
an adverse or ambiguous metric safe.

## Correct arithmetic, wrong meaning

**Symptom:** a number is calculated correctly but its direction, denominator,
anchor, population, or label is wrong.

**Check:** define the full metric frame and compare every surface that names it.

**Invariant:** the label and reference frame are part of correctness.

## Unordered current-record selection

**Symptom:** an update changes database row order, and the app appears to switch
profiles or lose data.

**Check:** positional queries, ownership filters, deterministic ordering, stable
tie-breakers, unique constraints, backend row caps, and pagination.

**Invariant:** never derive identity or “current” from unspecified database order;
enforce uniqueness at the authority.

## Fresh mutation, stale derived behavior

**Symptom:** the screen updates but a notification or insight is computed from an
older server echo, or an older async result overwrites the new state.

**Check:** mutation ordering, local reconciliation, derived recomputation, server
confirmation, rollback, cancellation, and freshness tokens.

**Invariant:** mutation and every dependent side effect share one freshness
contract.

## Account switch leaves a ghost user

**Symptom:** widgets, notifications, local queues, caches, or background work show
the previous account after logout.

**Check:** enumerate every local and external side effect, scope it by identity,
and exercise logout, switch, relaunch, and deletion.

**Invariant:** session boundaries include more than tokens and database rows.

## Auth configuration mistaken for auth success

**Symptom:** capabilities and source settings look correct, yet provider sign-in
fails on a release device or the session disappears after relaunch.

**Check:** provider UI, native capability, callback/deep link, backend session,
domain account creation, persisted session, and fresh-account behavior.

**Invariant:** verify the complete auth transaction in the intended build and
account state; diagnose provider or device boundaries before rewriting app logic.

## Debug success, release failure

**Symptom:** debug works, but the distributed app lacks a permission, endpoint,
deep-link declaration, entitlement, or environment value.

**Check:** canonical release lane, merged configuration, signed artifact contents,
and the critical path installed from that artifact.

**Invariant:** the shipped artifact is the configuration truth.

## CLI failure or success mistaken for remote state

**Symptom:** an upload tool exits badly after the remote accepted the build, or
exits successfully while processing later fails.

**Check:** artifact identity, transport response, remote processing, track, review,
and user availability through direct remote read-back.

**Invariant:** build, sign, upload, process, review, rollout, and availability are
separate states.

## App code done, operational dependency missing

**Symptom:** the app ships before its migration, server function, provider switch,
store product, or privacy page, leaving the feature broken or unsafe.

**Check:** app version, backend state, rollout order, backward compatibility,
owner, rollback, and evidence for each human console step.

**Invariant:** release is a coordinated transaction, not a client commit.

## AI both creates and approves truth

**Symptom:** a model invents a structured item and then judges its own output safe,
or promises an action that no structured state transition performed.

**Check:** deterministic facts, eligibility gates, model authority, unknown-input
behavior, stale pending actions, tool results, and exact live API composition.

**Invariant:** high-stakes eligibility belongs to deterministic authority; AI may
present or veto but cannot resurrect a deterministic rejection.

## Policy copy detached from behavior

**Symptom:** privacy or store text claims local-only processing, successful account
deletion, or supported functionality that the actual data path contradicts.

**Check:** source, signed binary, network path, data stores, deletion/export E2E,
store metadata, and the affected user path after any warning-driven change.

**Invariant:** policy and store claims are executable product surfaces and must be
derived from observed behavior.
