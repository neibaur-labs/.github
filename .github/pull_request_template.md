## What & why

<!-- One concern. Link the session charter or issue. -->

**Spec:** <!-- link to specs/<feature>.md, or "n/a - trivial change" -->

## Risk & impact

<!-- For reviewers: focus attention on architectural impact, not line-by-line. -->

- **Blast radius:** <!-- files / modules / users affected if this is wrong -->
- **Breakage points:** <!-- what could break: client state / localStorage, the
  share hash, affiliate links, the static build / export -->
- **Rollback:** <!-- how to undo this if it goes wrong -->
- **Risk level:** low | medium | high - <!-- one line of justification -->

## Verification

<!-- List commands run and their results. -->

## Checklist

- [ ] One concern only
- [ ] <= 400 changed lines, excluding lockfiles and generated fixtures
- [ ] No dependency changes, or proposal included below
- [ ] No pinned version downgraded to match training data
- [ ] No secrets, real PII, or hardcoded endpoints in the diff or fixtures
- [ ] Governance/protected-file changes are human-authored and intentional
- [ ] Accessibility impact considered for user-facing changes

## Dependency proposal

<!-- If applicable: name, exact version, purpose, size, maintenance status,
alternatives considered, and why no-dependency is insufficient. -->

## AI assistance

- [ ] PR labeled `ai-assisted` and `Co-authored-by` trailers present, or N/A