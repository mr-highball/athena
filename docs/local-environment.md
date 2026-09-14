# Local environment bootstrap

[Home](../README.md) · [Build paths](fpc-builds.md) · [Toolchain record](../templates/TOOLCHAIN.md)

## Initial decisions

Before installing anything, read the project's profile, instructions and any local
readiness record. Existing user choices and valid installed tooling take priority.
Ask only for missing decisions:

- Native FPC, browser Pascal, CGE native, CGE web, or a combination?
- Which host OS/CPU is supported, and is an existing container/WSL environment preferred?
- May missing tools be installed, and is the allowed scope local or system-wide?

The [project template](../templates/PROJECT.md#setup-questions) supplies a compact
prompt. Do not infer CGE from the presence of this guide or install every target
“just in case.” Do read-only inspection and native work while awaiting a necessary
setup choice. Never treat elapsed time as installation permission.

## Inspect before installing

Check the chosen profile and explicit overrides first, then PATH. Do not scan an
entire disk or dump the full environment, which can expose credentials.
Inspect selected paths for native FPC, pas2js, runtime/configuration, engine tool,
Git and any chosen container runtime.

PowerShell discovery:

```powershell
Get-Command fpc, ppcx64, ppc386, ppcrosswasm32, pas2js, compileserver,
  castle-engine, git, docker -All -ErrorAction SilentlyContinue |
  Select-Object Name, Source
```

Bash discovery:

```sh
for tool in fpc ppcx64 ppc386 ppcrosswasm32 pas2js compileserver castle-engine git docker; do
  command -v "$tool" || true
done
```

Discovery does not prove capability. Run the [native fixture](../templates/native-fpc.md),
and only the optional probes below. Record each capability as verified, broken,
missing or not required. If a tool is broken, inspect its compiler config and RTL
paths before reinstalling. If multiple copies exist, select one explicitly.

## Native FPC setup

If a compatible native compiler passes the fixture, reuse it.

If it is missing on Ubuntu 24.04 and system package installation is authorized:

```sh
sudo apt-get update
sudo apt-get install --yes fp-compiler-3.2.2 fp-units-fcl-3.2.2 fp-utils-3.2.2
fpc -iV
```

If it is missing on Windows, use the [Windows recipe](../templates/toolchain-windows.md#native-fpc).
If macOS is the declared host, reuse a working FPC or install an approved
distribution; `brew install fpc` is a build-tool acquisition option when Homebrew
is already adopted. Verify its version and architecture rather than assuming it
matches the project pin. Cross-platform source-build recipes are not interchangeable.

The [official FPC manuals](https://www.freepascal.org/docs.html) remain the upstream
reference. An IDE is optional for the command-line baseline.

## Optional web tooling

If browser Pascal or CGE web is selected, check `pas2js -iV`, its configuration,
the matching `rtl.js`, and `compileserver` if it is the chosen local HTTP server.
Compile the smoke source in the [Linux recipe](../templates/toolchain-linux.md#capability-probes).
Keep `PAS2JS` and `PAS2JS_RUNTIME` explicit; a second executable without its
configuration can fail to find `System`.

If FPC WASM is required, compile that smoke source using
`fpc -Pwasm32 -Twasip1`. Merely finding `ppcrosswasm32` or printing a version
does not prove the matching RTL and linker are available.

If required capabilities are absent:

- On the supported Linux x86_64 host, use the [pinned source recipe](../templates/toolchain-linux.md).
- On Windows, choose the [Windows web route](../templates/toolchain-windows.md#web-toolchain).
- If a container is selected, first inspect and probe the chosen
  [image family](platforms/cge.md#container-selection); build missing capabilities
  into an isolated derived image. Docker is not a universal prerequisite.

If the project uses no browser target, skip all of these checks and installs.

## Optional engine setup

If CGE is selected, verify the gitlink and public source URL before initializing
submodules. Compile the command-line tool from that checkout and set its engine
path explicitly using the [CGE recipe](../templates/cge-build.md).
A preinstalled editor or globally installed engine is not proof that the project
pin is being used.

If only the engine CLI/application is needed, do not build the editor or install
its optional Lazarus packages. If native graphics execution is required, also
provide the platform libraries required by the selected engine target.

## Completion record

Compile and run the native fixture. For web targets, compile both applicable
smokes, build the engine application if used, and verify browser readiness over
HTTP. Record the exact commands, paths, versions, source pins and results in the
[ignored local record](../templates/TOOLCHAIN.md#ignored-local-readiness-record).
Keep portable pins in the committed profile.

Do not declare the environment ready when an applicable capability is only
installed or untested. Report remaining gaps specifically. A future agent should
read the record, run cheap probes and resume work; research is needed only if
the selected recipe is obsolete, unsupported or fails with new evidence.

Avoid global PATH changes by default. Use session-local activation or an ignored
activation file. Preserve the previous toolchain and record how to select it.
See [cache invalidation](fpc-builds.md#cache-boundaries) and
[agent handoff](agent-stewardship.md#handoff).
