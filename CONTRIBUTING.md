# Contributing

Thanks for contributing to a `neibaur-labs` project. These are the
organization-wide defaults; an individual repository may add its own
`CONTRIBUTING.md` or `AGENTS.md`, which takes precedence.

## Workflow

- All changes go through a pull request. Direct pushes to the default branch
  are blocked by organization rulesets.
- Keep each pull request to a single concern — smaller PRs review faster.
- Use [Conventional Commits](https://www.conventionalcommits.org), for example
  `fix(parser): handle empty input`.
- Branch names follow `feat/*`, `fix/*`, `chore/*`, `test/*`, `docs/*`.

## Before you open a pull request

- Run the repository's checks locally and make sure they pass. The required
  status checks vary by the repository's stack, and all must be green before a
  PR can merge.
- Resolve all review conversations, and keep the branch up to date with the
  default branch.
- Pull requests are squash-merged, so write a clear PR title — it becomes the
  commit message on the default branch.

## AI-assisted contributions

- Label AI-assisted pull requests `ai-assisted` and include `Co-authored-by`
  trailers.
- Governance and protected paths (`.github/**`, `AGENTS.md`, `CLAUDE.md`,
  `LICENSE`, repository settings) are human-maintained. Agents may propose
  changes in the PR description; only a maintainer commits them, in a pull
  request containing no agent-assisted changes.

## Security

Never commit secrets, credentials, or tokens. See `SECURITY.md` for how to
report a vulnerability.
