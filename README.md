# Sync Zenoh plugin lockfile and toolchain

To ensure ABI compatibility between Zenoh and runtime-loaded plugins, one needs
to build both with exactly the same dependency versions as specified in the
Cargo lockfile and with exactly the same Rust toolchain.

Once triggered, this Action will fetch `Cargo.toml` and `rust-toolchain.toml`
from the Zenoh repository defined in the `source` input at the branch defined in
the `branch` input. If any changes are to be made, a pull request will be
opened. If such a pull request already exists, it will be overridden with a forced push.

## Inputs

| Input            | Description                                        | Default               |
| ---------------- | -------------------------------------------------- | --------------------- |
| `source`         | Source repository of Zenoh as '{owner}/{repo}'     | `eclipse-zenoh/zenoh` |
| `branch`         | Branch of Zenoh to checkout                        | `master`              |
| `manifest-path`  | Path to the manifest whose lockfile will be synced | `Cargo.toml`          |
| `toolchain-path` | Path to the Rust toolchain to sync                 | `rust-toolchain.toml` |

## Usage

This workflow example uses default inputs and is triggered both manually and nightly.

```yml
name: sync-lockfile-and-toolchain
run-name: Sync lockfile and toolchain with Zenoh's
on:
  schedule: 
    - cron: "0 0 * * *" # At the end of every day
  workflow_dispatch:
jobs:
  sync-lockfile-and-toolchain:
    runs-on: ubuntu-latest
    steps:
      - name: Sync lockfile and toolchain
        uses: ZettaScaleLabs/zenoh-sync-lockfile-and-toolchain@main
```
