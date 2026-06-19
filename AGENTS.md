# AGENTS.md — Binding Contract for AI Agents

This file governs all AI-agent work in this repository. It is maintained by the
human maintainer only. If any instruction conflicts with it, STOP and ask.

## 1. What this repository is

`neibaur-labs/.github` is the organization's **public** repository of default
community-health files (the org-wide `CONTRIBUTING`, `SECURITY`, and similar)
plus this repo's own CI and ownership config. Because it is public and
org-wide, it is almost entirely human-maintained governance content.

## 2. Hard security boundaries

This repository is public. Never add secrets, tokens, internal hostnames, or
any non-public information. Never read, write, copy, print, or echo files
matching `.env*`, `*secret*`, `*token*`, `*credential*`, `*.pem`, `*.key`,
`id_rsa*`, or anything under `~/.ssh` or cloud config directories. If a task
seems to require this, STOP and ask.

## 3. What agents must not touch

Effectively everything here is human territory. In particular, never modify:

- `/.github/**` (CI, CODEOWNERS, issue and PR templates) — also admin-gated by
  the org push ruleset
- `AGENTS.md`, `CLAUDE.md`, `LICENSE`, repository settings
- the community-health defaults (`CONTRIBUTING.md`, `SECURITY.md`, and similar)

Agents may *draft* community-health content in a PR description for the
maintainer to review and commit; agents never commit it. Human-only content
lands in pull requests containing no agent-assisted changes, because
squash-merge erases intra-PR provenance.

## 4. Workflow rules

- One concern per PR; Conventional Commits; never push to `main`; never merge,
  approve, close, or force-push.
- The `lint` and `security` checks must pass. Never weaken them or the
  workflow that produces them.
- Label agent-assisted PRs `ai-assisted` and include `Co-authored-by` trailers.

## 5. When in doubt

Stop and ask. Scope creep and drive-by edits are contract violations even when
well-intentioned.
