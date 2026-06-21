<!-- markdownlint-disable MD025 -->
# Spec: <feature name>

<!--
Copy this file to specs/<short-feature-name>.md and fill in every section.
Delete sections that genuinely do not apply, but say why rather than leaving
them blank. This spec is the source of truth: humans review it BEFORE the agent
generates code, and it stays in sync with the code afterward. See specs/README.md.

Keep it lean — narrative in Markdown, structured config in flat YAML. Every
token is budget and latency.
-->

- **Status:** draft | reviewed | building | done
- **Owner:** @<handle>
- **Related:** ADRs, issues, other specs (links)

## Summary — the what and the why

One or two paragraphs: what this builds, and the *why* behind it. The "why"
lets the agent reason forward instead of guessing. State the user-visible
outcome, not the implementation.

## Scope

**In scope:** the specific behavior this spec covers.

**Out of scope / non-goals:** what this deliberately does not do, so the agent
does not "improve" adjacent code.

## Technical design

### Requirements

- Functional requirement 1
- Functional requirement 2
- Non-functional (performance, accessibility, security) requirements

### Data schema

Describe the shape of the data. Use flat YAML for the structure:

```yaml
# example — replace
entity: order
fields:
  id: { type: uuid, primary: true }
  status: { type: enum, values: [pending, paid, shipped, cancelled] }
  total_cents: { type: integer, min: 0 }
  created_at: { type: timestamp }
```

### API / interface contracts

The "contracts" between parts of the system. One block per endpoint or
public function:

```yaml
# example — replace
endpoint: POST /orders/{id}/refund
auth: required          # server-enforced; never a client flag
request:
  amount_cents: integer
response:
  200: { refund_id: string }
  403: { error: string }   # caller not authorized
  409: { error: string }   # order not refundable
```

### Dependencies and versions

List libraries/tools with **explicit, current version numbers** (verified
against a current source, not memory — agents fall back to their training
cutoff and propose stale versions). Adding a dependency follows the AGENTS.md
dependency policy: propose, do not add.

| Dependency | Version | Why |
|---|---|---|
| | | |

## Scenarios (BDD / Gherkin)

State > Action > Outcome. Cover the happy path, the error paths, and the edge
cases. These become the failing tests written first.

```gherkin
Scenario: <happy path name>
  Given <starting state>
  When <action>
  Then <expected outcome>

Scenario: <error path name>
  Given <starting state>
  When <invalid action>
  Then <graceful failure / specific error>

Scenario: <edge case name>
  Given <boundary condition: null, empty, max, concurrent>
  When <action>
  Then <defined behavior — never undefined>
```

## Acceptance criteria

The checklist that means "done." Each item should be objectively verifiable.

- [ ] All scenarios above have passing tests
- [ ] Meets the non-functional requirements
- [ ] Follows security-conventions.md (server-side authz, no client-side trust,
      no hardcoded PII/endpoints)

## Open questions

Anything unresolved. An agent encountering one of these stops and asks rather
than guessing.
