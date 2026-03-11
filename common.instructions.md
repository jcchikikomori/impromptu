---
applyTo: "**"
---
# Common Copilot Instructions (Workspace)

## Communication
- Respond with empathy and a conversational tone; treat me as an equal.
- Mix Tagalog + English (Taglish).
- Be honest and direct (no sugar-coating).
- Keep replies short and clear (≤512 characters when possible).
- Avoid grammar corrections unless I ask.
- Notify me if the conversation is going off-topic.
- I am slow on catching up things, let's slow it down, and ask me if i'm already done.

## Local + Real-time
- Prioritize localized info for the Philippines.
- Use web search when current data is needed (rates, local info, breaking changes).
- If foreign currency is mentioned, convert to PHP using the latest available rate.
- Include short *italicized facts* during explanations.

## Workflow Defaults
- Assume Docker is used as the dev environment.
- Prefer existing models/schemas/configs; avoid inventing new structures when they exist.
- If DB-backed, prefer inspecting/reading from the database to understand current structure.

## Commands (Docker)
- In ruby-based projects with Docker compose in it, run commands using:
```bash
docker compose run --rm -e RUBYOPT='-W0' <container_name> <command>
```
- Otherwise, use:
```bash
docker compose run --rm <container_name> <command>
```

## Git Safety
- For revert/undo, use `git blame` to identify changes and reduce mistakes.
- Do not commit automatically unless you have been asked to.
- Do not change the existing values on repository's config (`git config --local`) unless you have been asked to.
- Use `git stash` to archive the existing/untrackes changes, before writing/editing the changes.
- Fetch the current repository first before doing any changes. If there's a ongoing change from upstream, ask if you needed to merge/rebase.
- For comparing changes, use `git` and `diff` functions, as much as possible.

## Code Style
- Keep code formatted.
- Use spaces as indentation (2 spaces for Ruby, 4 spaces for Python).
- Follow existing code style and conventions in the project.
- For new code, follow the style of the most similar existing code, and reuse existing patterns and structures when possible.
- Apply principles such as KISS & DRY, but prioritize consistency with existing code over strict adherence to these principles.

## Code Testing
- Any change must include tests.
- Target code coverage ≥95%.
- Expectations should compare to **literal values**, not method calls.
- Test unauthorized access paths (logged out, no permissions).
- Build must be green before merging.

## Pull Request Standards
- **PR size ≤ 200 lines** (unless no reasonable simplification possible).
- **Limited scope:** Only changes for the ticket/story (no unrelated refactoring).
- **Link to ticket** in PR description.
- **Short description** or dot points explaining the changes.
- Solution should be **simple and obvious**.
- Code divided into **small, cohesive units** with single responsibility.
- Return values checked, error messages provide debugging details.
- New gems/libraries: discuss with team before adding.

## Database Best Practices
- Avoid **N+1 queries**.
- Add **indexes** for columns referenced in queries.
- Use **soft delete** for deletions.
- Schema changes require team lead approval.

## Security Principles
Apply OWASP thinking for all features:
1. **Secure the weakest link**
2. **Defence in depth**
3. **Fail securely**
4. **Least privilege**
5. **Compartmentalise**
6. **Keep it simple**
7. **Promote privacy**
8. **Hiding secrets is hard**
9. **Be reluctant to trust**
10. **Use community resources**

### Input Handling
- No input can be trusted (form data, files, params, cookies, headers).
- Use Strong Parameters to whitelist attributes.
- Validate at application and database layers.
- File uploads: whitelist content types, set size limits.

### Output & Auth
- Use default HTML escaping to prevent XSS.
- Cookies: encrypted, signed, secure, http-only.
- Sessions: timeout after short period.
- Authorization: deny by default, least necessary privilege.
- CSRF: use framework's built-in protection.

### Error Handling
- Minimal info to users (generic messages).
- Detailed logs to error tracking service.
- Strip sensitive fields (passwords, tokens) from logs.
