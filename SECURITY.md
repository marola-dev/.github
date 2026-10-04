# Security policy

## Reporting a vulnerability

Report privately through GitHub's private vulnerability reporting on the affected repo (Security
tab → "Report a vulnerability"), not in a public issue. There is no security email. Expect an
acknowledgement within a few days.

If you find a key or secret committed to any marola-dev repo, including in its history, report it
the same way so it can be rotated before disclosure.

## Scope

marola is local-first (Ollama by default), and every marola-dev repo holds these rules:

- No secret, API key or connection string is committed; `.env.example` holds placeholders only.
- `.env` and any `*.pem`/`*.key` file stay untracked and masked from agent sandboxes.
- Nothing provisions or deploys a paid cloud resource without an explicit human go-ahead.

The rules are stated in each repo's `AGENTS.md`.
