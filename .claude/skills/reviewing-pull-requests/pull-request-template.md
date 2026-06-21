<!-- markdownlint-disable MD041 -->
<!--
Suggested .github/pull_request_template.md for project-template-node.
Reconcile with your current template — this adds the risk/impact summary and a
spec reference on top of the governance checklist you already use.
-->

## Summary

<!-- What does this PR do, and why? One short paragraph. -->

**Spec:** <link to specs/<feature>.md, or "n/a — trivial change">

## Risk & impact

<!-- For reviewers: focus attention on architectural impact, not line-by-line. -->

- **Blast radius:** <files / modules / users affected if this is wrong>
- **Breakage points:** <what could break — call out auth, data access, public
  APIs, shared modules, anything touching money or mail>
- **Rollback:** <how to undo this if it goes wrong>
- **Risk level:** low | medium | high — <one line of justification>

## How this was verified

<!-- Which scenarios / tests cover it; what you ran locally. -->

- [ ] Failing tests for the new behavior were written first, then made to pass
- [ ] `lint`, `typecheck`, `test`, `build`, `security` pass locally

## Governance checklist

- [ ] One concern, one PR; under the 400-line cap (excluding lockfile/fixtures)
- [ ] Does **not** edit tests and implementation in the same PR
- [ ] No unrelated cleanup, renames, or drive-by edits
- [ ] No dependency added/changed (or: proposed in this description, not added)
- [ ] No pinned version downgraded to match training data
- [ ] No secrets, real PII, or hardcoded endpoints in the diff or fixtures
- [ ] Protected paths (`.github/**`, `AGENTS.md`, `CLAUDE.md`, `LICENSE`,
      `.claude/skills/**`) untouched — or this is a human-only PR with no
      agent-assisted commits
- [ ] If agent-assisted: labeled `ai-assisted` with `Co-authored-by` trailers
