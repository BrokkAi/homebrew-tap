# Brokk Homebrew Tap

Homebrew formulae for [Brokk](https://github.com/brokkai) tools, built from the
prebuilt binaries attached to each project's GitHub releases.

## Usage

```sh
brew install brokkai/tap/mjolnir   # installs the `mj` terminal client
brew install brokkai/tap/anvil     # ACP server
brew install brokkai/tap/bifrost   # static analysis engine
```

macOS (universal), Linux x86_64, and Linux aarch64 are supported.

## How updates work

The formulae in `Formula/` are generated — do not edit them by hand. A
[scheduled workflow](.github/workflows/update.yml) runs every 6 hours:

1. `scripts/update-formulae.sh` queries each repo's latest GitHub release and
   regenerates the formulae, taking checksums from the `.sha256` files
   published alongside the release assets.
2. If anything changed, the workflow installs the updated formulae and runs
   `--version` as a smoke test.
3. Passing changes are committed and pushed automatically.

To force a refresh, run the "Update formulae" workflow manually from the
Actions tab, or run `./scripts/update-formulae.sh` locally (requires `gh`).
