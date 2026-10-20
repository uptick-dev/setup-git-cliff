# setup-git-cliff

Install a pinned, **prebuilt** [git-cliff](https://git-cliff.org/) binary and add
it to `PATH` — no Rust toolchain, no Docker build. A stable, Dependabot-friendly
alternative to actions that compile git-cliff from source.

## Why

Actions that build git-cliff (or run it in a Rust/Docker container) can break on
toolchain/version bumps and end up in Dependabot pinning fights. This action
downloads the official **prebuilt release binary** for the runner's platform, so
installs are fast and reproducible. The git-cliff version is a plain string
input — Dependabot never sees it, so it can't try to bump it.

## Usage

```yaml
- uses: uptick-dev/setup-git-cliff@v1
  with:
    version: "2.12.0"   # optional; this is the default

- name: Generate changelog
  run: git-cliff --config cliff.toml --unreleased -o CHANGES.md
```

## Inputs

| Name | Default | Description |
| --- | --- | --- |
| `version` | `2.12.0` | git-cliff release to install (no leading `v`). |

## Outputs

| Name | Description |
| --- | --- |
| `version` | The installed git-cliff version. |
| `path` | Absolute path to the installed binary. |

## Platforms

Linux and macOS, on `x86_64` and `arm64` — downloads the matching
`*-unknown-linux-gnu` / `*-apple-darwin` release asset.

Part of the changelog actions suite — used internally by
[`changelog-generate`](https://github.com/uptick-dev/changelog-generate)
and for the git-cliff fallback in release workflows.
