# Validation and evidence

[Home](../README.md) · [State contracts](state-and-constraints.md) · [Stewardship](agent-stewardship.md)

## Validation matrix

| Change | Minimum meaningful evidence |
| --- | --- |
| Wording or Markdown links | Review meaning; check paths, anchors and privacy. |
| Portable algorithm or codec | Checked FPC fixtures, relevant failure/boundary cases and replay. |
| Shared data layout | Rebuild affected callers; compatibility/round-trip fixtures. |
| Browser-facing behavior | Native checks plus the changed browser path. |
| UI structure | Actual interaction and desktop/narrow viewport screenshots. |
| Dependency/compiler pin | Clean fetch/build and the affected consumer checks. |
| Packaging or CI | Inspect staged contents; test the artifact and deployment base path. |
| Asset batch | Cached measured admission, pass/fail ledger and representative rendering. |

Broaden beyond this matrix when a concrete unresolved risk warrants it.
Once relevant checks pass, repeat them only after a meaningful change, failure
or evidence that the earlier result no longer applies.

## Acceptance without review loops

Define a small observable result before implementing. Required invariants stay
required even in a fast delivery profile. A review should identify actionable
defects, not force repeated subjective grading until an arbitrary score appears.

Use independent review when the risk or project requirement justifies it.
If authorized agent delegation is used, apply the
[bounded review policy](agent-stewardship.md#delegation-and-review).
A build pass proves compilation, not rendering, usability, performance or release
readiness. Record what was actually exercised and what remains untested.

## Artifact and catalog checks

If files are bundled or published, validate the current manifest and complete
transitive closure: paths, byte lengths, hashes, metadata and license notices.
Validate the staged bytes that will be uploaded. Avoid globbing stale hashed
generations or copying a developer's whole output directory.

If a large collection is integrated, reuse fingerprinted measurements, apply
explicit budgets, and record per-item pass/fail/deferred/existing outcomes and
reasons. Distinguish collected, decoded, admitted, selectable and rendered.
Do not treat every mechanical pass as individual visual approval.
Deduplicate cumulative counts when batches overlap.

If an item fails, defer it instead of repeatedly repairing it within a broad
batch. Version changed policy and invalidate only affected evidence.
See [catalog lessons](lessons.md#collection-and-usability).

## Evidence record

Record revision, toolchain/target, command, outcome, concise failure details and
artifact location. Separate native, browser, emulated-device and physical-device
evidence. Timing comparisons need the same workload and environment.

Keep generated logs/screenshots under ignored build output. Preserve small
curated fixtures in source control. The [work template](../templates/WORK.md)
captures acceptance, evidence, limitations and deferred work without a transcript.
