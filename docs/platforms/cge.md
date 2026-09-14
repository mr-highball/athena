# Optional Castle Game Engine

[Home](../../README.md) · [Dependencies](../dependencies.md) · [Bootstrap](../local-environment.md)

## Source selection

If CGE is used, prefer the canonical source repository as a pinned submodule:

```sh
git submodule add https://github.com/castle-engine/castle-engine.git vendor/castle-engine
git -C vendor/castle-engine checkout --detach "$CGE_COMMIT"
```

`CGE_COMMIT` must be an adopted, reachable commit, not a placeholder left in CI.
If a necessary fix requires a fork, document the fork, upstream ancestry,
consumer checks and rollback commit. Do not copy a contributor's fork into a
general starter. Follow the [submodule workflow](../dependencies.md#submodule-workflow).

Build the command-line tool from this checkout and explicitly set
`CASTLE_ENGINE_PATH` to it. A tool or engine preinstalled elsewhere may be a
different revision. The [official source build guide](https://castle-engine.io/compiling_from_source)
documents the platform-specific build-tool scripts.
Use the [CGE recipe](../../templates/cge-build.md#build-the-pinned-tool).

## Web target

If CGE targets the browser, the toolchain includes an FPC WASM cross-compiler,
matching target RTL, pas2js and its matching runtime/configuration.
The documented target is `wasm32-wasip1`; the higher-level command
`castle-engine compile --target=web` also builds the browser host.
Compiling a standalone WASI program is not equivalent.
See [CGE web documentation](https://castle-engine.io/web).

Use [inspect-first setup](../local-environment.md#inspect-before-installing) and
the [pinned Linux compiler recipe](../../templates/toolchain-linux.md).
Probe a real compile, not just version banners. Do not upgrade the engine,
cross-compiler and browser host independently without compatibility evidence.

Keep engine-specific code at the edge of a native-testable Pascal model.
Do not edit generated host code directly when the generating Pascal source can
be changed. Test bridge changes at numeric boundaries, with representative
rendering and relevant recovery behavior; see [browser checks](browser.md).

## Container selection

Docker is optional. These public image families are documented by the
[CGE Docker manual](https://castle-engine.io/docker):

| If | Candidate | Required follow-up |
| --- | --- | --- |
| You need compiler/platform tools and will supply a pinned engine | `kambi/castle-engine-cloud-builds-tools:cge-none` | Inspect bundled compiler; build your engine tool. |
| You need a development FPC family | `kambi/castle-engine-cloud-builds-tools:cge-none-fpc331` | Record exact compiler revision and probe the target. |
| You are investigating upstream engine behavior | `kambi/castle-engine-cloud-builds-tools:cge-unstable` | Treat bundled engine as an explicit alternate input. |

Resolve a selected tag to an immutable digest and record it in the
[toolchain profile](../../templates/TOOLCHAIN.md). These are candidates, not a
claim that every image includes a compatible WASM/pas2js pair. The upstream web
guide still describes additional setup; an FPC 3.3.1 label alone proves neither
cross-target support nor runtime compatibility.

If the image lacks a required tool, extend a pinned image with the
[compiler recipe](../../templates/toolchain-linux.md) or build directly on the
declared Linux runner. Do not make Docker mandatory merely to hide an unknown
local compiler configuration.

## Packaging

Use the engine's complete web distribution, then stage only its current referenced
files. If custom asset manifests or runtime chunks are added, verify hashes,
lengths, order and the binding between host and manifest before upload.
Never reuse stale engine output merely because it contains a plausible filename.
Follow [artifact checks](../validation.md#artifact-and-catalog-checks) and
[Pages](github-actions.md#pages).

These conditions do not make an engine editor, Android toolchain or texture
conversion suite mandatory for a command-line native build.
