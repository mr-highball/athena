# Native FPC starter

[Home](../README.md) · [Coding](../docs/coding-standards.md) · [Build contract](../docs/fpc-builds.md#build-contract)

## Fixture

Save this illustrative fixture as `tests/sample.tests.lpr`. Add the adopting
project's complete license notice before making it maintained source.
The fixture checks integer rounding without introducing a rendering dependency.

```pascal
program SampleChecks;

{$mode delphi}
{$H+}

uses
  SysUtils;

function RequiredSlots(const ACount, ACapacity: Int64): Int64;
begin
  if (ACount < 0) or (ACapacity <= 0) then
  begin
    raise EArgumentException.Create('Invalid count or capacity');
  end;
  Result := ACount div ACapacity;
  if ACount mod ACapacity <> 0 then
  begin
    Inc(Result);
  end;
end;

var
  LRejected: Boolean;
begin
  Assert(RequiredSlots(0, 4) = 0);
  Assert(RequiredSlots(8, 4) = 2);
  Assert(RequiredSlots(9, 4) = 3);
  Assert(RequiredSlots(High(Int64), 1) = High(Int64));
  LRejected := False;
  try
    RequiredSlots(1, 0);
  except
    on LException: EArgumentException do
    begin
      LRejected := True;
    end;
  end;
  Assert(LRejected);
  WriteLn('PASS native fixture');
end.
```

## Build commands

Run from the adopting repository root. Use a distinct build directory per
compiler/target in a multi-target project.

Bash, suitable as the body of `build.sh`:

```sh
#!/usr/bin/env bash
set -euo pipefail
compiler="${FPC:-fpc}"
mkdir -p build/native/units build/native/bin
"$compiler" -iV
"$compiler" -iTP
"$compiler" -iTO
"$compiler" -B -Mdelphi -Sa -Cr -Co -Ci -gl \
  -FUbuild/native/units -FEbuild/native/bin tests/sample.tests.lpr
./build/native/bin/sample.tests
```

PowerShell, suitable as the body of `build.ps1`:

```powershell
$ErrorActionPreference = 'Stop'
$compiler = if ($env:FPC) { $env:FPC } else { 'fpc' }
New-Item -ItemType Directory -Force build/native/units, build/native/bin | Out-Null
& $compiler -iV
if ($LASTEXITCODE -ne 0) { throw 'Compiler probe failed' }
& $compiler '-B' '-Mdelphi' '-Sa' '-Cr' '-Co' '-Ci' '-gl' `
  '-FUbuild/native/units' '-FEbuild/native/bin' tests/sample.tests.lpr
if ($LASTEXITCODE -ne 0) { throw 'Compilation failed' }
& ./build/native/bin/sample.tests.exe
if ($LASTEXITCODE -ne 0) { throw 'Native checks failed' }
```

Add the project's complete notice to maintained scripts as well.
Neither command installs dependencies or starts a server.
See [inspect-first setup](../docs/local-environment.md#inspect-before-installing)
if a compiler is missing.

## Expected result

The command prints the compiler version and `PASS native fixture`, returning
zero. Generated units/executables belong under ignored `build/`.
Replace this fixture with meaningful project tests as the implementation grows.
The corresponding [native CI job](github-actions.md#native-job) calls the same
script rather than maintaining another test implementation.
