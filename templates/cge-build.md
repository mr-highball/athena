# Conditional CGE build recipe

[Home](../README.md) · [CGE standard](../docs/platforms/cge.md) · [Local setup](../docs/local-environment.md)

## Prerequisites

Use only when the project profile selects CGE. The engine submodule must already
be pinned and initialized; required native or web compiler probes must pass.
Set `CGE_PROJECT` to the relative directory containing `CastleEngineManifest.xml`.
This recipe does not invent a compatible engine commit for every application.

## Build the pinned tool

Unix shell, from the consuming repository root:

```sh
set -euo pipefail
repo_root="$PWD"
export CASTLE_ENGINE_PATH="$repo_root/vendor/castle-engine"
(
  cd "$CASTLE_ENGINE_PATH/tools/build-tool"
  bash ./castle-engine_compile.sh
)
castle_tool="$CASTLE_ENGINE_PATH/tools/build-tool/castle-engine"
test -x "$castle_tool"
"$castle_tool" --version
```

Windows PowerShell:

```powershell
$ErrorActionPreference = 'Stop'
$env:CASTLE_ENGINE_PATH = Join-Path $PWD 'vendor/castle-engine'
Push-Location (Join-Path $env:CASTLE_ENGINE_PATH 'tools/build-tool')
try {
  & ./castle-engine_compile.ps1
  if ($LASTEXITCODE -ne 0) { throw 'Engine tool compilation failed' }
} finally {
  Pop-Location
}
$castleTool = Join-Path $env:CASTLE_ENGINE_PATH 'tools/build-tool/castle-engine.exe'
& $castleTool --version
if ($LASTEXITCODE -ne 0) { throw 'Engine tool probe failed' }
```

If script execution is blocked, diagnose the local execution policy and follow
authorized system policy; do not silently disable protections.
Use the actual output location of the selected upstream revision if it differs.
See the [source build reference](https://castle-engine.io/compiling_from_source).

## Build the chosen target

Using the Unix variables above, with `CGE_PROJECT` set:

```sh
test -f "$CGE_PROJECT/CastleEngineManifest.xml"
"$castle_tool" "--project=$CGE_PROJECT" compile --mode=release
```

If the chosen target is web, use this instead:

```sh
"$castle_tool" "--project=$CGE_PROJECT" compile --target=web --mode=release
test -f "$CGE_PROJECT/castle-engine-output/web/dist/index.html"
```

PowerShell uses the same arguments with `& $castleTool`, checking
`$LASTEXITCODE` after each command. The [web target documentation](https://castle-engine.io/web)
describes the generated distribution. Inspect actual output for the pinned revision.

## Stage and test

Create a fresh site directory from the completed web distribution. Validate its
required resources before assigning the stable CI stage path.
If the project adds a catalog or split runtime, the Pascal stager must verify
its full current closure; do not treat a recursive copy as that validator.

Serve the stage with the selected Pascal HTTP server, run representative browser
checks at root and subpath, then pass the same stage to
[Pages upload](github-actions.md#pages-extension).

A native build uses neither the web host nor these publication steps.
The native core remains independently testable through [FPC](native-fpc.md).
