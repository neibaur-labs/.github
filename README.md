# neibaur-labs/.github

Organization-wide defaults for the `neibaur-labs` GitHub organization.

This **public** repository supplies default community-health files — such as
`CONTRIBUTING.md` and `SECURITY.md` — that GitHub applies to any repository in
the organization that does not provide its own copy. A repository's own file
always takes precedence; these are fallbacks only, and they do not appear in
the file tree or history of the repositories they apply to.

## What you get

- Docs CI emitting exactly the two checks `org-stack-docs-ruleset` requires:
  `lint` (markdownlint-cli2) and `security` (gitleaks).
- `.markdownlint-cli2.yaml` tuned so well-formed docs pass and real defects fail.
- The AI-agent contract (`AGENTS.md` / `CLAUDE.md`) at the docs tier.
- `CODEOWNERS`, and editor/line-ending hygiene.

## What lives here

- `CONTRIBUTING.md`, `SECURITY.md` — org-wide community-health defaults (root).
- `.github/` — this repo's own CI, CODEOWNERS, and any issue/PR templates.

## Governance

This repository is classified `stack:docs` and is gated like any other active
repository: pull requests with passing `lint` and `security` checks,
squash-merged into a protected `main`. Because it is **public** — required for
community-health defaults to cascade — it must never contain secrets or
non-public information.
