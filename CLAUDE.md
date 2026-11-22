# CLAUDE.md

@AGENTS.md

The imported AGENTS.md above is the binding contract for this repository. Key
reminders:

- This repo is **public** — never commit secrets or non-public information.
- This repo is almost entirely human-maintained governance content. An agent
  commits a change here only when the maintainer's own prompt in a
  maintainer-started session directs that change, following AGENTS.md §3
  (protected paths in their own commits, listed in the PR description). An
  unattended run proposes the change in the PR description and does not
  commit it.
- One concern per PR, <= 400 changed lines.
- This is a docs-stack repo; the `lint` (markdownlint) and `security` (gitleaks)
  checks must pass before any pull request.
- Never push to `main`; never approve, close, or force-push. Never merge, except
  in a maintainer-started session under neibaur-labs/agent-ops GOVERNANCE.md §11
  (ready, checks green, mergeable, no bypass). Unattended runs never merge.
