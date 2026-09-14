# State, determinism and constraints

[Home](../README.md) · [Coding](coding-standards.md) · [Validation](validation.md)

## Portable source of truth

Own domain models, canonical serialization, hashes, replay and semantic validation
in Pascal. Renderers and editors consume these models; they do not define different
versions of the rules. Specify integer widths, overflow policy, text encoding,
ordering, units and rounding.

If replay crosses native and browser targets, use the same fixtures and compare
semantic results or canonical bytes as appropriate. Do not assume platform random
generators, floating-point formatting or dictionary iteration are interchangeable.
See [browser cautions](platforms/browser.md#language-and-bridge-cautions).

## Atomic edits

An edit declares a baseline revision, editable scope, requested change and
preserved state. Build a detached candidate, validate it independently, then
publish once. Failure, cancellation or a stale revision must preserve the baseline.
Include dependency/support references and nested objects in preservation checks.

Stable IDs support history and save compatibility. Validate imported state;
do not silently regenerate it into a different valid result. Version wire
contracts when meaning changes. Use [work records](../templates/WORK.md#acceptance-and-evidence)
to specify exact preservation and rollback expectations.

## If a constraint solver is used

Separate rule construction from acceptance checks. Document what cells, domains,
passes, neighborhoods and quotas mean in domain units. A tiny independent oracle
or exhaustive fixture is often more valuable than a larger mirrored implementation.

Distinguish invalid input, contradiction, bounded-search exhaustion, cancellation
and success. Exhausting a search budget does not prove impossibility. Weights
do not establish optimality. Fix seeds and bound work; record algorithm/policy
versions when changing replay behavior.

If a request is approximate, name its metric and report achieved output. A density
control might mean item count, occupied surface area or volume; these are different
contracts. Do not make the UI promise one while implementing another.

## If partial application is allowed

Keep hard invariants: locks, scope, support, non-overlap, connectivity and data
integrity. If an independent candidate cannot fit, skip or defer it and explain
the shortfall. Validate dependencies incrementally so one rejected candidate
does not invalidate all successful work.

Do not silently broaden a user's selection or smooth protected terrain.
Automatic repair needs an explicit bounded repair envelope.
See [lessons on validation](lessons.md#validation-and-intent) and
[behavior checks](validation.md#validation-matrix).
