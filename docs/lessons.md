# Lessons converted into standards

[Home](../README.md) · [Documentation maintenance](documentation.md) · [Work record](../templates/WORK.md)

## Delivery before expansion

**Observed pattern:** native compilation, engine compilation and CI packaging
can each pass while the deployed application fails.

**Rule:** establish a tiny end-to-end artifact early. Keep compilation, staging,
runtime readiness and publication as distinct checkpoints.

**Apply:** [build paths](fpc-builds.md#choose-a-path),
[Pages checks](platforms/github-actions.md#pages),
[browser readiness](platforms/browser.md#runtime-readiness).
**Example:** [Pages extension](../templates/github-actions.md#pages-extension).

## Toolchain and cache ambiguity

**Observed pattern:** an unintended compiler, mismatched runtime, stale caller
or unavailable submodule commit creates failures far from the original change.

**Rule:** record actual executable paths and versions, pin public source commits,
and invalidate caches at interface/toolchain boundaries.

**Apply:** [cache boundaries](fpc-builds.md#cache-boundaries),
[submodule workflow](dependencies.md#submodule-workflow).
**Example:** [CGE recipe](../templates/cge-build.md).

## Collection and usability

**Observed pattern:** a large inventory is mistaken for a usable catalog;
substring classification produces false matches; a flat selector hides useful
choices; overlapping batches inflate counts.

**Rule:** separate source collection from runtime admission and discovery.
Use explicit categories, measured dimensions, bounded mixtures and honest ledgers.
A whole-word classifier must not confuse a food name containing “table” with furniture.

**Apply:** [artifact checks](validation.md#artifact-and-catalog-checks).
**Example:** [deferral ledger](../templates/WORK.md#deferral-ledger).

## Validation and intent

**Observed pattern:** safety checks also encode convenient implementation limits,
so reasonable edits do nothing or reject an entire batch.

**Rule:** distinguish immutable correctness rules from configurable policy.
Name the user's metric, use bounded repairs only within authorized scope, and
report achieved output or a useful shortfall.

**Apply:** [partial application](state-and-constraints.md#if-partial-application-is-allowed),
[validation matrix](validation.md#validation-matrix).
**Example:** [acceptance record](../templates/WORK.md#acceptance-and-evidence).

## Portable results need portable semantics

**Observed pattern:** native and browser targets differ in record/array ownership,
numeric boundaries or serialization despite sharing source.

**Rule:** define canonical state and use independent conformance fixtures on
every shipped execution target. Keep renderer data out of core contracts.

**Apply:** [portable source of truth](state-and-constraints.md#portable-source-of-truth),
[browser cautions](platforms/browser.md#language-and-bridge-cautions).
**Example:** [native fixture](../templates/native-fpc.md#fixture).

## Review and agent overhead

**Observed pattern:** repeated full validation, overlapping helpers, large context
forks and subjective critic loops consume effort without resolving new risks.

**Rule:** tie effort to consequences and evidence gaps. Start with one agent,
use bounded authorized delegation and stop blind retries.

**Apply:** [stewardship](agent-stewardship.md), [acceptance](validation.md#acceptance-without-review-loops).
**Example:** [work and handoff record](../templates/WORK.md).

## Promote lessons selectively

Keep only lessons that recur or prevent a material failure. Each addition needs
a general rule, applicability condition, example and verification link. Remove
obsolete advice and private incident details. A retrospective should improve
defaults, not become an ever-growing mandatory reading list.
