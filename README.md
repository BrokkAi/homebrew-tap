# Brokk Homebrew Tap

Homebrew formulae for [Brokk](https://github.com/brokkai) tools, built from the
prebuilt binaries attached to each project's GitHub releases.

## Usage

```sh
brew tap brokkai/tap
brew trust brokkai/tap
brew install --formula brokkai/tap/mjolnir   # installs the `mj` terminal client
brew install --formula brokkai/tap/micro-acp # Go ACP terminal client
brew install --formula brokkai/tap/anvil     # ACP server
brew install --formula brokkai/tap/bifrost   # static analysis engine
```

Always use the full `brokkai/tap/<formula>` name. A bare `brew install
mjolnir` installs an unrelated, deprecated cask of the same name instead of
`mj`. Upgrade the same way: `brew upgrade --formula brokkai/tap/mjolnir`.

Recent Homebrew versions refuse to load formulae from an untrusted tap, hence
`brew trust`. Tap first: the one-line `brew install brokkai/tap/<formula>`
without a prior `brew tap` is not reliable on Linuxbrew.

macOS (universal), Linux x86_64, and Linux aarch64 are supported.

## How updates work

The formulae in `Formula/` are generated — do not edit them by hand. A
[scheduled workflow](.github/workflows/update.yml) runs every 2 hours:

1. `scripts/update-formulae.sh` queries each repo's latest GitHub release and
   regenerates the formulae, taking checksums from the `.sha256` files
   published alongside the release assets.
2. If anything changed, the workflow installs the updated formulae and runs
   `--version` as a smoke test.
3. Passing changes are committed and pushed automatically.

To force a refresh, run the "Update formulae" workflow manually from the
Actions tab, or run `./scripts/update-formulae.sh` locally (requires `gh`).
