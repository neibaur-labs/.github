# Contributing

All changes must arrive through pull requests. Do not push directly to `main`.

## First-Time Setup

Use pnpm only. After cloning, install the committed dependency set and activate
the Git hooks:

```sh
pnpm install --frozen-lockfile
pnpm prepare
```

`.npmrc` sets `ignore-scripts=true`, so `pnpm prepare` must be run manually
after each fresh clone. Install gitleaks before committing:

- Windows: `winget install gitleaks`
- macOS: `brew install gitleaks`
- Linux: <https://github.com/gitleaks/gitleaks#installing>

## Workflow

1. Use [Conventional Commits](https://www.conventionalcommits.org/).
2. Commit failing tests before the implementation that makes them pass.
3. Run `pnpm validate` before opening a PR.
4. Keep each PR to one concern and at most 400 changed lines, excluding
   lockfiles and generated fixtures.

AI-assisted work is governed by [AGENTS.md](./AGENTS.md). Agent-authored PRs
must carry the `ai-assisted` label and `Co-authored-by` trailers.

Record significant decisions as Architecture Decision Records in
[docs/adr/](./docs/adr/).
