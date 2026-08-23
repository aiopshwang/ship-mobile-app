# Mobile boundary checks

Read only the sections relevant to the current request. These checks identify
contracts worth making explicit; they are not a requirement to add process to a
simple change.

## Domain meaning

Define a value before computing or displaying it:

```text
subject + included event types + anchor + time zone + day boundary
+ window + denominator + unit + missing-data rule + user-facing label
```

Check especially:

- start time versus end time versus elapsed duration;
- running versus completed records;
- backdated values and ranges that cross midnight;
- total, average, maximum, percentile, rank, and population direction;
- whether multiple raw events form one user-level session;
- whether every surface uses the same named definition.

Prefer property tests such as monotonicity, conservation across a boundary, and
cross-surface agreement over a handful of convenient example values.

## State and synchronization

Name the write states the product can actually observe, for example:

```text
local-only -> durably queued -> remote accepted -> read back
           \-> rejected or retryable failure
```

Do not use these names blindly; adapt them to the system's real guarantees.

Check:

- which state drives success copy and undo or retry actions;
- idempotency keys and duplicate handling across taps and retries;
- retryable versus terminal failures, retry budget, and poison-item isolation;
- explicit ordering, stable tie-breakers, row limits, and pagination;
- optimistic updates, rollback, server echo, and stale-response suppression;
- schema constraints, ownership, and server-side authorization;
- partial success and whether continuing can corrupt later work.

An offline queue belongs to an identity. Prevent a queued write from one account
being sent under another account. Do not silently discard recoverable pending data
merely to simplify logout.

## Identity and privacy

Trace sign-in through all layers that matter:

```text
provider UI -> OS capability -> callback or deep link -> backend session
            -> domain account -> persisted session -> relaunch
```

Test new-user, returning-user, denied/cancelled, missing-provider-data, relaunch,
logout, account switch, and deletion paths when relevant.

Inventory user-scoped state beyond the main database:

- auth and refresh tokens;
- preferences and derived caches;
- offline queues and local files;
- widgets, notifications, badges, and app-group/shared storage;
- deep-link or navigation seeds;
- feature cooldowns, analytics identity, and paid AI caches.

Centralize cleanup but make independent cleanup steps resilient so one failure
does not prevent the rest. Keep server secrets and destructive account authority
outside an untrusted client; protect device-local credentials with the platform's
secure-storage boundary.

## Lifecycle and concurrency

Normal foreground use is only one path. Select the transitions the feature owns:

- cold start and warm resume;
- foreground, background, termination, and restoration;
- deep link, push tap, widget, share extension, or shortcut entry;
- permission not determined, denied, limited, and granted;
- rapid repeated taps and two entry points racing;
- state written by another process or extension;
- rebuilds that accidentally repeat expensive or effectful work.

Establish a runtime-appropriate atomic, actor, serialized-queue, or in-flight
guard before competing work can pass its first suspension point. Do not hold a
thread-blocking lock across `await`. Inject clocks and lifecycle adapters where
practical. Reload external/shared state at a defined boundary instead of trusting
a warm in-memory copy forever.

## Visual and interaction truth

For visual failures, reproduce the failing constraints before tweaking styles:

- target screen dimensions, safe areas, orientation, and platform;
- keyboard and system insets;
- light/dark/high-contrast themes;
- text scale, localization, long values, and empty values;
- scroll position, overlays, sheets, and parent layout constraints;
- minimum tap target, disabled/loading/error states, and rapid input.

Inspect parent constraints and the rendered screen. A child widget's source can
look correct while its parent makes it invisible or untappable.

## Native platform and production configuration

Separate source declarations from final artifact facts.

For the touched platform, inspect the relevant merged or signed output for:

- application or bundle identity and version/build number;
- release environment values and service endpoints;
- permissions and user-facing purpose strings;
- deep links, URL schemes, package visibility, and associated domains;
- entitlements, capabilities, app groups, keychain groups, and extensions;
- signing identity, provisioning, architectures, symbols, and minimum OS target;
- background modes, network policy, exported components, and embedded frameworks.

Debug success does not prove release configuration. Prefer one repeatable release
path with pre-build assertions and post-build artifact inspection to multiple
manual runbooks that can drift.

## Notifications, background work, and derived state

Check that scheduled work is derived from the latest accepted state, not a stale
server echo. Cancel or replace obsolete work after edits, deletes, account changes,
or relevant settings changes.

Distinguish:

- preparation from actual delivery;
- delivery from user observation;
- cached content from cooldown consumption;
- relative-time copy generated today from copy delivered tomorrow.

Do not run paid, recursive, or side-effectful preparation from an uncontrolled
render/rebuild path.

## AI and high-stakes claims

Separate four responsibilities:

1. deterministic fact computation;
2. deterministic eligibility or policy gate;
3. optional model wording, ranking, extraction, or veto;
4. user-facing action and durable state transition.

For higher-risk domains, a model may narrow an already-valid candidate but should
not revive a deterministic rejection. Unknown or unavailable inputs usually block
publication or a harmful action; low-risk copy may fall back to deterministic
wording instead.

Check missing versus zero, sparse-window completeness, negative polarity, and
whether a friendly label hides an adverse measurement. Test that conversational
promises agree with the structured action actually committed, and invalidate
stale pending actions after correction, cancellation, or a new intent.

When provider compatibility is material and external calls are authorized,
live-probe the exact API composition intended for production—model + tools +
response format + endpoint—using an approved sandbox or test account and
synthetic or minimized data. Do not mutate production or incur unapproved cost.
Otherwise label compatibility unverified. Mock tests remain useful but cannot
establish provider compatibility.

## Operational and policy surfaces

When applicable, trace behavior into:

- database migrations, server functions, provider consoles, and rollout order;
- backward compatibility with older installed clients;
- account deletion, export, moderation, reporting, and blocking;
- privacy/data-safety declarations and actual network/data paths;
- content rights, attribution, affiliate or advertising disclosure;
- current store requirements and reviewer-accessible flows.

Treat a required human console step as part of the operational contract, with an
owner, order, observable proof, and rollback. Do not call the wider feature ready
while that gate remains unapplied.
