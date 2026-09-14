# Dependencies and submodules

[Home](../README.md) · [Principles](principles.md) · [Optional CGE](platforms/cge.md)

## Dependency boundary

Default: implement maintainable shared behavior in portable Pascal with FPC's
standard libraries. Prefer a small owned implementation when it is reasonable;
convenience alone does not justify a second language or package ecosystem.

Before adding a dependency, state the capability, maintenance cost, license,
supported compilers and why the owned Pascal path is insufficient. For specialized
capabilities such as graphics engines, use an optional adapter. Core public types,
canonical artifacts and tests must remain usable without that adapter.

Build orchestration may use shell, PowerShell, Make, Git, archive utilities,
compiler prerequisites and Docker. Do not introduce Node/Python test servers,
package managers, asset validators, browser drivers or document generators.
If an upstream maintenance tool uses such a runtime, isolate that upstream-only
step; do not inherit it as an ordinary project requirement.

Official GitHub actions and agent clients can have their own internal runtimes.
Using the platform is distinct from requiring npm or Node for the Pascal project.
The [CI template](../templates/github-actions.md#native-job) uses maintained
checkout/artifact actions; it makes no claim of a runner with zero non-Pascal processes.

## Submodule workflow

If third-party source is necessary, prefer a Git submodule under `vendor/`
over copying its source or using an opaque binary.

1. Select a public upstream or an explicitly adopted maintained fork.
2. Record its URL, immutable commit, license and reason in the project profile.
3. Commit the gitlink and `.gitmodules`; initialize recursively on a fresh clone.
4. Develop dependency fixes in a separate checkout. Publish the dependency commit
   to the recorded remote before advancing the consuming project's pin.
5. Verify that a clean clone can fetch the exact pin. A local commit, moving
   branch name or cached checkout is not proof that CI can obtain it.

```sh
git submodule sync --recursive
git submodule update --init --recursive
git submodule status --recursive
```

Do not use `git submodule update --remote` in a reproducible build.
The [CGE path](platforms/cge.md#source-selection) supplies a canonical engine URL.
Other libraries require their own explicit dependency decision; no solver or
engine is mandatory for Athena adoption.

## Upgrade evidence

A dependency upgrade should include the old/new pins, consumer checks, clean
fetch result and rollback pin. Keep compiled units separate by target/compiler;
see [cache invalidation](fpc-builds.md#cache-boundaries).

If Athena itself is a submodule, place a short root `AGENTS.md` in the consumer
that links to the selected Athena standards. The submodule's instructions do not
automatically govern files outside it. See [template adoption](../templates/README.md#copying-templates).
