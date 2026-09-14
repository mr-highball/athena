# FPC build paths

[Home](../README.md) · [Native example](../templates/native-fpc.md) · [CI](platforms/github-actions.md)

## Choose a path

| If | Then |
| --- | --- |
| Native library, CLI or portable core only | Use FPC and standard units; no engine, browser or Docker requirement. |
| Multiple native platforms are supported | Add only those runner/compiler combinations to CI. |
| A compiler upgrade is under evaluation | Keep the supported compiler gate; add a separate bounded canary. |
| Browser presentation without CGE is required | Use Pascal adapters compiled with pas2js and its matching runtime; retain native core tests. |
| CGE is used for a native target | Pin the engine submodule and compile its build tool from that source. |
| CGE is used for a browser target | Also establish the WASM compiler, pas2js runtime and browser host contract in [CGE](platforms/cge.md#web-target). |
| A container is required | Select by actual capabilities and pin its digest; follow [CGE image choices](platforms/cge.md#container-selection) if relevant. |
| Static browser files are published | Test the staged directory and follow [Pages](platforms/github-actions.md#pages). |

## Build contract

Provide one documented command that compiles and executes the native checks.
It must work from a clean checkout without a developer IDE installation.
FPC 3.2.2 is the example stable baseline here, not an eternal requirement.
Declare the selected version and target in the project profile.

Print the resolved compiler path, `fpc -iV`, `fpc -iTP` and `fpc -iTO`.
Allow an explicit compiler override. On Windows, quote each compiler argument in
PowerShell and check `$LASTEXITCODE` after native commands.

Use `-B -Sa -Cr -Co -Ci -gl` for checked fixtures where applicable:
rebuild, assertions, range, overflow, I/O and line information.
Use explicit output/search paths. Do not share generated unit directories between
FPC releases, target architectures, pas2js and CGE.
See the [copyable command](../templates/native-fpc.md#build-commands).

## Cache boundaries

A cache accelerates a valid build; it must not make a broken clean build appear valid.

- Toolchain key: OS, architecture, compiler source/install checksum, bootstrap
  recipe and target set. Save only after toolchain probes pass.
- Compiled-unit key: compiler, CPU/OS, dialect/options, engine/dependency pins
  and relevant interfaces. Rebuild dependent callers after record/layout changes.
- Asset/staging key: source manifests, transform version and packaging policy.
  See [closure checks](validation.md#artifact-and-catalog-checks).

Persist a successfully built compiler before application tests run, so a later
application failure does not discard expensive valid toolchain work.
Never cache credentials, transient browser profiles or an unverified installation.

## Development compilers

If a required target is unavailable in the stable compiler, pin a reviewed
development source commit and its bootstrap compiler. Record the matching native
and cross RTL, configuration paths and compiler provenance. Verify a native
fixture and a tiny cross-target application before building the whole product.
A version banner alone does not prove a functioning linker, RTL or browser host.

Keep this extension in a build script; do not introduce a package manager or
a second implementation language. Consult [platform quirks](platforms/github-actions.md#runner-quirks).
