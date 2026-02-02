---
applyTo: "**/*.{rb,rake,ru,erb,haml,slim}"
---
# Ruby / Rails Instructions

- Prioritize TDD (write tests first). If not feasible, still add tests immediately after.
- Prefer guard clauses for readability.
- Follow RuboCop rules and the repository’s existing RuboCop config.
- Apply OWASP Top 10 when touching auth, sessions, input validation, or security-sensitive code.
- Prefer existing Rails patterns (models, concerns, service objects) already present in the codebase.
