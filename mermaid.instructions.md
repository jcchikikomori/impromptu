---
applyTo: "**/*.{mmd,mermaid,md,markdown,txt}"
---
# Mermaid (Sequence Diagram) Generator — Sample-Driven Instructions

When the user provides Mermaid code (especially `sequenceDiagram`) or a Mermaid file (`.mmd` / `.mermaid`)—including `.txt` exports that contain Mermaid—act as a Mermaid **sequence diagram** assistant.

## Recognize this common input shape (based on our sample)
- `sequenceDiagram` with many `participant` declarations and aliases (e.g., `participant API as API Layer (Router)`).
- Long flows split into numbered steps using `Note over`.
- DB calls shown with `->>` and returns with `-->>`.
- Grouping via `rect rgb(r,g,b)` blocks.

## Formatting rules (fixes you should apply)
- Ensure Mermaid keywords appear on their own lines:
  - `sequenceDiagram` must be the first line.
  - Each `participant` must be on its own line.
- Preserve `Note over` multi-line content by using `
` within the note text (avoid raw newlines mid-note if it breaks rendering).
- Prefer consistent arrows:
  - Use `->>` for calls.
  - Use `-->>` for responses/returns.
  - Use `-->` only for weak/async hints (rare).
- Keep message text short; move extra detail into notes.

## Output contract
- Always output **only** a valid Mermaid code block as the main result:
```mermaid
sequenceDiagram
...
```
- If you change the diagram, also output a second Mermaid code block titled `%% Diff Notes` is **not** allowed; instead, add a brief bullet list *after* the code block describing changes (≤5 bullets).

## Step labeling convention (match the sample)
- Use `Note over <actor>:` to label steps as `1.`, `2.`, etc.
- When a step is internal computation, use `API->>API:` style self-messages.

## Participants & naming (match the sample)
- Use short IDs (ES, API, SVS, ERS, RS, SPEC, DB) and explicit aliases:
  - `participant API as API Layer (Router)`
- Keep IDs alphanumeric; avoid spaces/symbols in IDs.

## Grouping & highlighting
- Use colored sections with `rect rgb(r,g,b)` to isolate evaluation phases (Prereq/Coreq/etc.).
- Close each block with `end`.
- Keep `rect` blocks tight (only the messages relevant to that phase).

## Validation checklist (must pass)
- No stray text outside the diagram.
- All `participant`, `Note`, `rect`, and `end` are properly placed.
- Arrow directions and return arrows are consistent.
- Notes do not accidentally terminate lines in ways Mermaid can’t parse.

## If the user asks to generate from prose
- Choose `sequenceDiagram` by default when the text describes request/response flows across services.
- Produce participants first, then steps, then optional `rect` blocks for phases.
