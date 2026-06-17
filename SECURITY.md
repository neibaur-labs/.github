# Security Policy

## Security Model

Never commit credentials, private keys, or other sensitive material. Local
pre-commit hooks scan staged changes, and CI scans repository history as an
independent catch layer.

Treat any pushed real credential as exposed: rotate or revoke it immediately.
History rewriting is not a substitute for rotation.

## Reporting a Vulnerability

Use
[GitHub private vulnerability reporting](https://docs.github.com/en/code-security/security-advisories/guidance-on-reporting-and-writing/privately-reporting-a-security-vulnerability)
instead of opening a public issue.

Include:

- A description of the vulnerability and its potential impact.
- Steps to reproduce or a proof of concept.
- Any known mitigations.

Responses are handled as quickly as maintainer availability permits.
