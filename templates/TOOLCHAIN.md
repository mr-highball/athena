# Toolchain record template

[Home](../README.md) · [Local setup](../docs/local-environment.md) · [Cache keys](../docs/fpc-builds.md#cache-boundaries)

## Committed portable profile

Record public facts only:

| Input | Value |
| --- | --- |
| Profile ID and supported host/CPU | TO BE SET |
| Native FPC version or source commit | TO BE SET |
| Bootstrap compiler source and checksum | TO BE SET if needed |
| WASM target and compiler commit | Not applicable, or exact pin |
| pas2js compiler origin, RTL source commit and rtl.js origin | Not applicable, or exact provenance |
| CGE public URL and gitlink | Not applicable, or exact pin |
| Container reference | Not applicable, or repository@sha256:digest |
| Build recipe revision | Commit or recipe hash |
| Native/browser probe commands | Relative paths and parameters |

Do not treat this file's placeholder values as authorization to install anything.
Select applicable entries using the [project profile](PROJECT.md).

## Ignored local readiness record

Create `build/local-environment.md` in the adopting project, or another ignored
local state file. It may contain resolved executable/configuration paths because
it stays local. Never paste it into shared examples or CI artifacts unfiltered.

Record each capability as **available and verified**, **present but broken**,
**missing**, or **not required**. Include actual versions, architecture,
configuration/RTL locations, pin/digest verification, probe command, exit status
and date. Keep a list of tools changed by setup and how to select the previous
installation. Link back to the adopted portable profile and bootstrap recipe.

## Reuse and invalidation

On the next session, read the record and confirm files still exist and reported
pins/versions match. Run a cheap capability probe. Rebuild or repair only if the
profile, compiler, host architecture, engine pin or probe result changed.
A stale “ready” marker is not proof of readiness. A working system FPC need not
be replaced by a private install merely for consistency of path names.

See [completion records](../docs/local-environment.md#completion-record) and
[handoff](WORK.md#handoff).
