# Windows toolchain recipe

[Home](../README.md) · [Inspect first](../docs/local-environment.md#inspect-before-installing) · [Toolchain record](TOOLCHAIN.md)

## Native FPC

Read the project profile and inspect existing executables before downloading.
If the installed compiler passes the [native fixture](native-fpc.md), reuse it.
This reference installs FPC 3.2.2 for an i386 Windows target; do not choose it
for a project requiring a different host/target pairing.

Only run this after installation is authorized. Use a new directory and keep
existing compilers intact. The example uses the public upstream installer and
a fixed checksum; a changed download must fail verification.

```powershell
$ErrorActionPreference = 'Stop'
$installRoot = Join-Path $env:LOCALAPPDATA 'PascalToolchains\fpc-3.2.2-i386'
if (Test-Path -LiteralPath $installRoot) {
  throw 'Inspect the existing installation before installing again'
}
$installer = Join-Path $env:TEMP 'fpc-3.2.2.i386-win32.exe'
$uri = 'https://downloads.freepascal.org/fpc/dist/3.2.2/i386-win32/fpc-3.2.2.i386-win32.exe'
$expected = '7ec78b1790ecac7685f440b17f9e03865bc09846b7c068a9270c4d37704b5ac8'
Invoke-WebRequest -Uri $uri -OutFile $installer
$actual = (Get-FileHash -LiteralPath $installer -Algorithm SHA256).Hash
if ($actual -ne $expected) { throw 'FPC installer checksum mismatch' }

$arguments = '/SP- /VERYSILENT /SUPPRESSMSGBOXES /NORESTART /DIR="' + $installRoot + '"'
$process = Start-Process -FilePath $installer -ArgumentList $arguments -WindowStyle Hidden -Wait -PassThru
if ($process.ExitCode -ne 0) { throw 'FPC installation failed' }
$compilerDir = Join-Path $installRoot 'bin\i386-win32'
$nativeCompiler = Join-Path $compilerDir 'fpc.exe'
$env:PATH = $compilerDir + ';' + $env:PATH
& $nativeCompiler -iV
if ($LASTEXITCODE -ne 0) { throw 'FPC version probe failed' }
```

Review the selected installer's behavior and required privileges before use.
The directory is local; that alone does not guarantee an installer makes no
system changes. If installation is not authorized, report the missing capability
and use an already approved toolchain or container where available.

Compile and run the native fixture next. A version string alone is insufficient.
No Lazarus IDE is required for this path.

## Web toolchain

If no browser target is selected, skip this section.

If a compatible toolchain already exists, explicitly select its FPC, pas2js,
configuration and RTL paths. Confirm the target capabilities using
[compiler probes](toolchain-linux.md#capability-probes); use PowerShell invocation
syntax and check each exit code.

If tools are missing, select one approved route:

| Route | Use when | Setup |
| --- | --- | --- |
| Existing WSL Ubuntu 24.04 x86_64 | The project supports Linux-built outputs and WSL is available | Run the [Linux recipe](toolchain-linux.md) inside that distribution |
| Windows-native FPCupdeluxe | The project requires native Windows build tools | Use the WA setup described by the [CGE web guide](https://castle-engine.io/web) and record resulting toolchain versions |
| Approved container | The project already uses Docker | Select and probe the [conditional CGE image](../docs/platforms/cge.md#container-selection), adding missing web tools in a pinned derived image |

Do not enable WSL, install Docker, switch host architecture or install a GUI tool
without an applicable user choice. Linux paths and activation exports belong
inside the Linux environment; they are not Windows executable paths.

For the Windows-native route, inspect the FPCupdeluxe installation's
ccr/pas2js-rtl/bin/target directory for the paired pas2js executable,
configuration and package tree, replacing target with the actual host directory.
Another copy on PATH can lack matching configuration. Prefer an explicit path;
do not delete the other compiler to resolve precedence. Record actual compiler
and source revisions and compare them with the adopted profile.

Set PAS2JS and PAS2JS_RUNTIME in the current session.
After resolving actual paths into PowerShell variables:

```powershell
$env:PAS2JS = $pas2jsExecutable
$env:PAS2JS_RUNTIME = $pas2jsRuntime
& $env:PAS2JS -iV
if ($LASTEXITCODE -ne 0) { throw 'pas2js version probe failed' }
if (-not (Test-Path -LiteralPath $env:PAS2JS_RUNTIME)) {
  throw 'Matching pas2js runtime is missing'
}
& $webCompiler '-Pwasm32' '-Twasip1' '-iV'
if ($LASTEXITCODE -ne 0) { throw 'WASM version probe failed' }
```

These variables must come from inspected paths, not placeholders copied literally.
Use the web-capable FPC for WASM; a working stable native compiler is not evidence
that it contains a WASM target. Compile the small probes and, if CGE is selected,
build its pinned CLI with the [PowerShell recipe](cge-build.md#build-the-pinned-tool).

## Save readiness

Follow the [completion record](../docs/local-environment.md#completion-record).
Record exact paths and configuration locally, portable pins in the project
profile, and any unsupported or untested capability as a gap. Keep changes to
PATH session-local. Future agents should probe and reuse this environment rather
than repeating downloads or researching a new setup route.
