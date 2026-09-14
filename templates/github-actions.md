# GitHub Actions templates

[Home](../README.md) · [CI standard](../docs/platforms/github-actions.md) · [Native starter](native-fpc.md)

## Native job

After adopting `build.sh` and the fixture from the native starter, place the
following in `.github/workflows/ci.yml`. Update the publishing branch if needed.
The reviewed checkout pin below resolves to v7.0.1.

```yaml
name: Native FPC
on:
  push:
  pull_request:
  workflow_dispatch:

permissions:
  contents: read

concurrency:
  group: checks-${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-24.04
    timeout-minutes: 15
    steps:
      - uses: actions/checkout@3d3c42e5aac5ba805825da76410c181273ba90b1
        with:
          submodules: recursive
          persist-credentials: false
      - name: Install native FPC
        run: |
          sudo apt-get update
          sudo apt-get install --yes fp-compiler-3.2.2 fp-units-fcl-3.2.2
          test "$(fpc -iV)" = "3.2.2"
      - name: Build and check
        shell: bash
        run: bash ./build.sh
```

This installs only the selected native compiler units, not an engine or browser.
Recursive checkout is harmless without submodules; use `false` if dependency
checkout is deliberately disabled. SHA pins were resolved from the public action
repository; review upgrades deliberately. See [runner quirks](../docs/platforms/github-actions.md#runner-quirks).

## Optional web build

If the project profile selects CGE web, run the adopted
[Linux toolchain recipe](toolchain-linux.md) and [CGE recipe](cge-build.md)
before staging. Run the native gate first. Store the custom compiler cache
separately and save it after capability probes pass.

The web build must expose a verified `build/site` stage or another declared path.
Run the [browser checks](../docs/platforms/browser.md#representative-checks)
against that stage, including a repository subpath. Do not copy an unverified
directory from a previous job.

## Pages extension

Only after the web build and smoke checks, append this step to the build job:

```yaml
      - name: Upload verified site
        if: github.event_name != 'pull_request' && github.ref == 'refs/heads/main'
        uses: actions/upload-pages-artifact@fc324d3547104276b827a68afc52ff2a11cc49c9
        with:
          path: build/site
```

Then add a sibling job:

```yaml
  deploy:
    if: github.event_name != 'pull_request' && github.ref == 'refs/heads/main'
    needs: build
    runs-on: ubuntu-24.04
    timeout-minutes: 10
    permissions:
      pages: write
      id-token: write
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    concurrency:
      group: pages
      cancel-in-progress: false
    steps:
      - name: Publish verified artifact
        id: deployment
        uses: actions/deploy-pages@368f82528645a54fb793d4d04e342629a3f51346
```

The example pins correspond to upload-pages-artifact v5.0.0 and deploy-pages v5.0.1.
If adding deployment to the native workflow, move cancellation policy to the
build job or disable workflow-level cancellation so an active deploy is not
cancelled by a new push. Configure the Pages source/environment as described in
[Pages setup](../docs/platforms/github-actions.md#pages).
This extension is not meaningful for a native executable alone.

## Container jobs

If a verified container is selected, declare its immutable reference under the
build job's `container.image`, then use explicit Bash steps. Supply the project
engine through its gitlink, not whichever engine happens to be in the image.
See [image selection](../docs/platforms/cge.md#container-selection) and
[toolchain records](TOOLCHAIN.md). No unverified digest is embedded in this template.
