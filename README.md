# VS Code Copilot Instructions Split (by language)

Place these files under `.github/instructions/` (recommended) or anywhere in the workspace.

## Global implementation

Place these files under this directory:

`C:\Users\YourUserName\AppData\Roaming\Code\User\prompts`

Suggested structure:

```
.github/
  copilot-instructions.md          # optional global repo-wide
  instructions/
    common.instructions.md
    security.instructions.md
    ruby.instructions.md
    python.instructions.md
    fastapi-sqlalchemy.instructions.md
```

Notes:
- `applyTo` scopes which files each set of instructions applies to.
- VS Code combines instructions that match the current context.
