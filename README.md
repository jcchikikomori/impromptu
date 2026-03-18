# impromptu

## Global implementation

Place these files under this directory:

`C:\Users\YourUserName\AppData\Roaming\Code\User\prompts`

### VSCode

Place these files under `.github/instructions/` (recommended) or anywhere in the workspace.

Suggested structure:

```
.github/
  copilot-instructions.md          # optional global repo-wide
  instructions/
    common.instructions.md         # always loaded (applyTo: "**)
    ruby.instructions.md           # Ruby/Rails files only
    python.instructions.md         # Python files only
    docker.instructions.md         # Container configs only
```

## Claude Code

Suggested structure:

For Claude Code, place instructions in the `.claude/` folder:

```
.claude/
  CLAUDE.md                        # main project instructions (always loaded)
  settings.json                    # optional, tool permissions
  skills/
    rails/
      SKILL.md                     # on-demand Rails workflow
    docker/
      SKILL.md                     # on-demand Docker workflow
```

**Key differences:**
- Claude Code uses `CLAUDE.md` instead of `copilot-instructions.md`
- Skills go in `.claude/skills/<name>/SKILL.md`
- No `applyTo` — Claude loads `CLAUDE.md` always, skills on-demand via description matching
- Use `CLAUDE.local.md` for personal overrides (gitignored)

📖 **Docs:** https://code.claude.com/docs

## OpenCode

For OpenCode, place instructions in the `.opencode/` folder:

```
.opencode/
  config.json                      # main config (model, provider, etc.)
  AGENTS.md                        # project instructions (always loaded)
```

**Key differences:**
- Uses `AGENTS.md` (similar to GitHub Copilot's format)
- Config in `.opencode/config.json` for model/provider settings
- Supports multiple providers (OpenAI, Anthropic, OpenRouter, etc.)

📖 **Docs:** https://opencode.ai/docs

## Official Documentation Links

| Tool | Docs |
|------|------|
| GitHub Copilot | https://code.visualstudio.com/docs/copilot/customization/overview |
| Claude Code | https://code.claude.com/docs |
| OpenCode | https://opencode.ai/docs |
| Cursor | https://cursor.com/docs |
| Windsurf | https://docs.windsurf.com/windsurf/getting-started |

Notes:
- `applyTo` scopes which files each set of instructions applies to.
- VS Code combines instructions that match the current context.
- **Avoid duplicate content** across files — if `common.instructions.md` has rules, don't repeat them in language-specific files.

## Recommended AI Assistants

| Use Case | Recommended | Why |
|----------|-------------|-----|
| **Complex Rails/legacy work** | Claude (Opus/Sonnet) | Better at nuanced context, multi-file refactoring, and reasoning through legacy patterns |
| **Quick edits/snippets** | GPT-4o or Claude Sonnet/Haiku | Faster response, lower cost per token |
| **Code review & explanation** | Claude | More thorough explanations, catches edge cases |
| **Simple scaffolding** | GitHub Copilot (GPT-4 or Claude Haiku) | Built-in, no context switching |
| **Long conversations** | Claude | 200K context window vs GPT's 128K |

### Token Optimization Tips
- Use **specific `applyTo` patterns** instead of `"**"` to avoid loading irrelevant instructions
- Only **one file should be `applyTo: "**"`** (currently `common.instructions.md`)
- Remove duplicate rules — trust inheritance from common instructions
- Use comments like `<!-- inherited from common.instructions.md -->` to remind yourself
