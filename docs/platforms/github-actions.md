# GitHub Actions

[Home](../../README.md) · [Build paths](../fpc-builds.md) · [Workflow template](../../templates/github-actions.md)

## Native gate

Start with the supported FPC compiler on one declared runner. Invoke the same
build script used locally. Add other operating systems only when they are
supported products or compatibility targets. Make a development compiler a
separate canary, not an accidental replacement for the stable gate.

Use explicit timeouts, read-only build permissions and concurrency cancellation
for superseded checks. Pin third-party actions to reviewed commit SHAs.
Check out recursive submodules only if the project uses them. Do not bootstrap
an engine for a native library's unit tests.

Install missing prerequisites using the [local setup recipe](../local-environment.md);
CI should differ mainly in a clean environment, not in compiler configuration.

## Caches and artifacts

Apply the [cache boundaries](../fpc-builds.md#cache-boundaries). Save verified
toolchains before product tests. Keep failure logs and small evidence artifacts;
exclude browser profiles, personal environment records and unrelated downloads.

Do not upload a failed or partially staged build. The directory exercised by
runtime checks must be the one passed to publication.
Use a fresh output stage identified by the current build and manifest.

## Pages

If a static browser target is published, choose GitHub Actions as the Pages
source. The deployment job needs `pages: write`, `id-token: write`, a
`github-pages` environment and a dependency on the successful build/upload job.
The [official custom-workflow guide](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages)
describes these requirements.

Restrict deployment to the adopted publishing branch; pull requests only validate.
Keep site/environment policy aligned with the workflow condition.
See the [Pages template](../../templates/github-actions.md#pages-extension).

Test both `/` and a repository subpath such as `/sample/`. Workers, WASM,
catalogs and media must resolve from that base. A root-only localhost test can
miss a broken published site. See [browser hosting](browser.md#hosting).

## Runner quirks

- Linux package availability and hosted images evolve. Verify the compiler
  version after installation; a package command's success is insufficient.
- Shell steps inside Linux containers default differently from host Bash steps.
  Declare `shell: bash` if using Bash syntax.
- Windows argument quoting, path case and executable suffixes differ from Linux.
  Use argument arrays in PowerShell and propagate native exit codes.
- A container build does not prove hardware-accelerated rendering.
  Distinguish software GPU, emulated viewport and physical-device evidence.
- Browser sandbox or user-namespace errors require a diagnosed runner-specific
  remedy. Do not disable sandboxing globally as a default setup step.
- Avoid filesystem deletion across mixed shells. Resolve cleanup paths inside
  the intended build directory before removing them.

CGE/compiler-specific issues are in [CGE](cge.md) and
[local bootstrap](../local-environment.md#completion-record).
