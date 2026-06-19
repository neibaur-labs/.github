# Security Policy

This is the organization-wide security policy for `neibaur-labs`. A repository
may provide its own `SECURITY.md`, which takes precedence.

## Reporting a vulnerability

Please report security vulnerabilities privately — not in public issues or pull
requests. Use GitHub's private vulnerability reporting on the affected
repository (the "Report a vulnerability" button on the repository's Security
tab) where it is enabled. If that is unavailable, contact the maintainer
directly.

Include enough detail to reproduce the issue. We aim to acknowledge reports
promptly and will coordinate disclosure with you.

## Handling of secrets

- Secrets, credentials, and tokens must never be committed to any repository.
  Automated secret scanning runs in CI, and a committed secret is treated as
  compromised: rotate it immediately — scrubbing history is not remediation.
- Configuration secrets belong in a vault or in CI secrets, never in the
  working tree.

## Scope

This policy covers repositories owned by the `neibaur-labs` organization.
