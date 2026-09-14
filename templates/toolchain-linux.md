# Linux web toolchain recipe

[Home](../README.md) · [Inspect first](../docs/local-environment.md#inspect-before-installing) · [Toolchain record](TOOLCHAIN.md)

## When this applies

Use this reference recipe only if the selected target needs FPC WebAssembly or
pas2js and the required capability is missing. It targets Ubuntu 24.04 on x86_64.
A native-only project can use distribution FPC and skip this page.

Read the profile and local readiness record first. Reuse a compatible working
installation. Install packages only within the scope already authorized by the
user. These source pins describe a previously used compiler pairing; they are
not a claim of compatibility with every CGE revision or of current upstream support.

| Component | Public source | Reference pin |
| --- | --- | --- |
| FPC native compiler, cross compiler and pas2js executable | [FPC source](https://gitlab.com/freepascal.org/fpc/source) | d7f522a5611b13f37164c5eac87ade49b2f5b324 |
| pas2js package sources | [pas2js source](https://gitlab.com/freepascal.org/fpc/pas2js) | fa10c59214cd226c60af465c831d66a7321f0214 |

The executable and generated RTL JavaScript below both come from the FPC source
pin. The separate pas2js checkout provides package sources and configuration
layout. Record all three origins; replacing only one is not a safe upgrade.
Clean-fetch availability and the selected application's compatibility must be
verified during adoption.

## Install missing prerequisites

If these packages are absent and system installation is authorized:

```sh
sudo apt-get update
sudo apt-get install --yes \
  git ca-certificates build-essential \
  fp-compiler-3.2.2 fp-units-fcl-3.2.2 fp-utils-3.2.2
```

Check the distribution compiler's version before building. It is the native
bootstrap compiler, not the WASM compiler.

## Build an isolated toolchain

Run the following as Bash in a repository. Use a new, dedicated directory in an
ignored build area. Do not point it at an existing checkout or shared installation.
A failed setup may be diagnosed in place; do not treat it as ready or overwrite
a working environment to retry.

```bash
set -euo pipefail
toolchain_root="$PWD/build/toolchains/web-reference"
fpc_pin=d7f522a5611b13f37164c5eac87ade49b2f5b324
pas2js_pin=fa10c59214cd226c60af465c831d66a7321f0214
test ! -e "$toolchain_root"
mkdir -p "$toolchain_root/logs"
source_dir="$toolchain_root/fpc-source"
pas2js_dir="$toolchain_root/pas2js-source"
prefix="$toolchain_root/install"
logs="$toolchain_root/logs"

fetch_source() {
  local url=$1 revision=$2 destination=$3
  git init "$destination"
  git -C "$destination" fetch --depth 1 "$url" "$revision"
  git -C "$destination" checkout --detach FETCH_HEAD
  test "$(git -C "$destination" rev-parse HEAD)" = "$revision"
}
fetch_source https://gitlab.com/freepascal.org/fpc/source.git \
  "$fpc_pin" "$source_dir"
fetch_source https://gitlab.com/freepascal.org/fpc/pas2js.git \
  "$pas2js_pin" "$pas2js_dir"

/usr/bin/ppcx64 -iV
make -C "$source_dir" -j2 all PP=/usr/bin/ppcx64 NOGDB=1 OPT=-O2 \
  > "$logs/fpc-native.log" 2>&1
make -C "$source_dir" install INSTALL_PREFIX="$prefix" \
  > "$logs/fpc-install.log" 2>&1
test -e "$prefix/bin/ppcx64" || \
  ln -s "$prefix/lib/fpc/3.3.1/ppcx64" "$prefix/bin/ppcx64"
cat > "$prefix/bin/fpc.cfg" <<EOF
-Fu$prefix/lib/fpc/3.3.1/units/\$fpctarget/*
-Fl$(dirname "$(gcc -print-libgcc-file-name)")
EOF

export PATH="$prefix/bin:$PATH"
export PPC_CONFIG_PATH="$prefix/bin"
make -C "$source_dir" -j2 crossall CPU_TARGET=wasm32 OS_TARGET=wasip1 \
  FPC="$prefix/bin/fpc" NOGDB=1 OPT=-O2 > "$logs/fpc-wasm.log" 2>&1
make -C "$source_dir" crossinstall CPU_TARGET=wasm32 OS_TARGET=wasip1 \
  INSTALL_PREFIX="$prefix" > "$logs/fpc-wasm-install.log" 2>&1
test -e "$prefix/bin/ppcrosswasm32" || \
  ln -s "$prefix/lib/fpc/3.3.1/ppcrosswasm32" "$prefix/bin/ppcrosswasm32"

mkdir -p "$pas2js_dir/bin/x86_64-linux"
cp "$prefix/bin/pas2js" "$pas2js_dir/bin/x86_64-linux/pas2js"
cp "$source_dir/utils/pas2js/dist/rtl.js" "$pas2js_dir/packages/rtl/rtl.js"
cat > "$pas2js_dir/bin/x86_64-linux/pas2js.cfg" <<'EOF'
-Sc
-Fu$CfgDir/../../packages/*/src
-Fu$CfgDir/../../packages/rtl
-Jc
EOF

export PATH="$pas2js_dir/bin/x86_64-linux:$prefix/bin:$PATH"
export PAS2JS="$pas2js_dir/bin/x86_64-linux/pas2js"
export PAS2JS_RUNTIME="$pas2js_dir/packages/rtl/rtl.js"
fpc -iV
fpc -Pwasm32 -Twasip1 -iV
"$PAS2JS" -iV
test -s "$PAS2JS_RUNTIME"
```

Keep these exports session-local, or save them in an ignored activation script.
Verify that installed compiler links resolve within the chosen prefix.
Installation layouts can change with pins.

## Capability probes

First compile and run the [native fixture](native-fpc.md) with the chosen native
compiler. Then save this source as build/probes/toolchain_smoke.lpr:

```pascal
program ToolchainSmoke;

{$mode delphi}
{$H+}

begin
  WriteLn('PASS compiler smoke');
end.
```

Compile only the capabilities selected by the profile. For a profile using both:

```bash
mkdir -p build/probes/wasm/units build/probes/js
fpc -Pwasm32 -Twasip1 \
  -FUbuild/probes/wasm/units -FEbuild/probes/wasm \
  build/probes/toolchain_smoke.lpr
"$PAS2JS" -Tbrowser -obuild/probes/js/toolchain_smoke.js \
  build/probes/toolchain_smoke.lpr
test -s build/probes/js/toolchain_smoke.js
test -s "$PAS2JS_RUNTIME"
```

Successful compilation proves compiler/RTL resolution, not browser execution.
For CGE web, build the chosen engine application and serve its distribution
using the [CGE recipe](cge-build.md#build-the-chosen-target).
Check the rendered page and runtime readiness as described in
[browser validation](../docs/platforms/browser.md). If compileserver is the
selected server, also probe that executable and verify HTTP responses.

Record readiness only after the applicable probes pass. Include host, source pins,
recipe revision and actual executable/configuration paths in the
[local readiness record](TOOLCHAIN.md#ignored-local-readiness-record).
Keep failed logs for diagnosis. Apply [cache boundaries](../docs/fpc-builds.md#cache-boundaries)
when reusing tools or changing compiler and engine revisions.
