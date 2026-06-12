# neibaur-labs — Repository Template & Org Setup Plan

Goal: any future repo starts life already past ~90% of Phase 0, with the
remaining 10% reduced to a checklist and a 10-minute drill.

Two mechanisms, used together:
- **Org-level configuration** — settings that GitHub applies to repos
  automatically (rulesets, Actions defaults, security defaults). Done once.
- **Template repository** — the files. Stamped into each new repo.

Plus a `SETUP.md` checklist inside the template for the handful of steps
neither mechanism can automate.

---

## A. Org-level configuration (do once — covers every future repo)

1. **Promote the branch ruleset to org level.** Org Settings → Rulesets →
   New branch ruleset, targeting **all repositories**, default branch.
   Recreate the terminal-run ruleset exactly: require PR; required status
   checks `lint, typecheck, test, build, security`; require up-to-date
   branches; linear history; **squash merge only**; block force pushes and
   deletions; require conversation resolution; **empty bypass list**.
   (New repos are born protected — this is the single biggest time-saver.)
2. **Promote the push ruleset to org level.** Restrict file paths
   `.github/**`, all repositories, bypass = organization/repository admin
   role only.
3. **Org Actions defaults.** Settings → Actions → General: default workflow
   permissions = **read-only**; **uncheck** "Allow GitHub Actions to create
   and approve pull requests."
4. **Org billing.** Actions spending limit set explicitly (degrade, not
   bill). Confirm it once a year.
5. **Org security defaults.** Settings → Code security: enable Dependabot
   alerts + security updates **"for new repositories"** so each repo
   inherits them at creation. Enable private vulnerability reporting
   default if offered at org level.
6. *(Optional)* an org `.github` repository for default community-health
   files (fallback SECURITY.md / support docs) — low priority since the
   template carries its own.

## B. The template repository — `neibaur-labs/project-template`

Create it **clean** (do not fork terminal-run and delete — residue always
survives). Build from these artifacts, genericized, then flip
Settings → **Template repository: ON**.

### Files to include

**Governance & agent contract**
- `AGENTS.md` — the binding contract, with project-specifics isolated in a
  clearly marked "PROJECT SECTION — customize" block (project description,
  any project-specific boundaries). Universal sections stay verbatim: hard
  security boundaries, human-only paths, dependency policy,
  charter-as-approval pattern, workflow rules, tests-first, PR caps.
- `CLAUDE.md` — `@AGENTS.md` import + key reminders.
- `docs/` — `adr/0000-adr-template.md`; **seed ADRs** for the universal
  decisions (AI-assisted development governance; cost-constrained
  architecture / no-uncapped-billing; accessibility-with-enforcement) as
  drafts to accept or adapt; `scope-exception-log.md` (empty, rule at top);
  `phase-0-drills.md` (blank template incl. the prevention/catch/remediate
  secret-layer framing); `playtest-observation-template.md` if the project
  is user-facing.
- `SECURITY.md`, `CONTRIBUTING.md` (Conventional Commits, pnpm-only,
  `pnpm prepare` fresh-clone requirement, validate-before-PR),
  `SETUP.md` (Section C below). **No LICENSE file** — add deliberately per
  project; a placeholder gets forgotten and becomes accidental policy.

**CI & GitHub config**
- `.github/workflows/ci.yml` — the five-job pipeline, all actions
  SHA-pinned, security job = gitleaks CLI (git mode, fetch-depth 0) +
  forbidden-pattern grep + `pnpm audit`, `permissions: contents: read`,
  concurrency cancellation. (Dependabot keeps the SHAs fresh per-repo.)
- `.github/dependabot.yml` — npm weekly grouped minor/patch + majors
  separate; github-actions weekly.
- `.github/pull_request_template.md` — the checklist version.
- `.github/CODEOWNERS` — `* @neibaur` plus `/.github/**`, `AGENTS.md`,
  `CLAUDE.md`, `/docs/**` entries.

**Local prevention layer (the hard-won, verified versions)**
- `.husky/pre-commit` — `set -e`; lint-staged; gitleaks via
  `git diff --cached | gitleaks stdin --redact --no-banner --config
  "$(git rev-parse --show-toplevel)/.gitleaks.toml"`; fail-closed with
  install instructions.
- `.husky/commit-msg` — commitlint.
- `commitlint.config.js` — config-conventional.
- `.gitleaks.toml` — `[extend] useDefault = true` + the
  word-boundary standalone-key-ID rule.

**Toolchain configs**
- `.npmrc` (`ignore-scripts=true`, `engine-strict=true`), `.gitattributes`
  (`* text=auto eol=lf`), `.editorconfig`, `.nvmrc`, `.gitignore`.
- `tsconfig.base.json` (strict + noUncheckedIndexedAccess +
  exactOptionalPropertyTypes), `eslint.config.js` (strict-type-checked,
  `no-restricted-syntax` banning eval/Function, no-literal-string seam,
  Next rootDir setting parameterized or removed for non-Next projects),
  prettier config, `vitest.config.ts` with coverage thresholds (values
  marked "tune per project").
- Root `package.json` — scripts `lint / typecheck / test / validate /
  format / prepare`, **top-level** `lint-staged` block, `engines`,
  `packageManager` pin. Keep the workspace layout minimal (a single
  `packages/` example) — monorepo shape is project-specific.

### Template caveats
- **Templates copy files only.** Rulesets, secrets, enabled features, and
  the Code app connection never copy — that's what Section A and SETUP.md
  exist for.
- **Templates drift.** Standing rule: any governance improvement made in a
  real project gets backported to the template in the same sitting.

## C. `SETUP.md` — per-new-repo checklist (target: under 30 minutes)

1. Create repo **inside the org** from the template → org rulesets and
   security defaults apply automatically. Verify under the repo's
   Rules tab.
2. Decide and add **LICENSE** (deliberate choice, logged in an ADR if
   nonstandard).
3. Customize: AGENTS.md project section, README, CODEOWNERS if different,
   coverage thresholds, eslint Next/rootDir bits, repo name references.
4. Connect the **Claude Code GitHub app** to the new repo (org app
   settings → repository access).
5. First clone, per machine (most are once-ever per machine):
   `corepack enable` (admin shell) → `pnpm install --frozen-lockfile` →
   `pnpm prepare` (hooks; required because ignore-scripts blocks auto-
   install) → `winget install gitleaks` if absent → restart shells.
6. Open one trivial PR to make the five checks exist, confirm the org
   ruleset now enforces them.
7. **Condensed drills (10 min, log results in docs/phase-0-drills.md):**
   a. Direct push to main → expect GH013 rejection.
   b. Stage a bare fake key id (AKIA + 16 chars, non-example) → commit →
      expect hook block; verify RuleID with `-v`.
   c. PR containing `eval(` → expect lint AND security checks red.
8. Skim org spending limit / Actions defaults still sane (annual-ish).

## D. Division of labor for building it

The template repo itself is a fine agent task **except** `.github/**` and
`AGENTS.md` (human-authored, per the contract those files enforce).
Practical split: you create the repo, commit AGENTS.md/CLAUDE.md and
`.github/` by hand (mostly copy-paste from terminal-run), then dispatch a
Sonnet session to assemble and genericize the rest from a charter listing
the files above — with the usual acceptance: fresh-clone `pnpm install
--frozen-lockfile && pnpm prepare && pnpm validate` passes, and a staged
fake key is blocked.