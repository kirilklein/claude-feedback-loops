---
description: Log one pipeline gap — a later stage caught what an earlier one should have
allowed-tools: Read, Write, Edit, Glob
---

Append one line to `.claude/workflow-gaps.md` recording a pipeline gap. Do this *before* fixing the underlying issue, so the gap is logged even if the fix takes the rest of the session.

## Layers

Use exactly these names, in pipeline order:

```
format  lint  types  test  review  ci  bot-review  human-review  production  tooling
```

`tooling` is for when the pipeline itself broke (wrong lint flags, missing venv, a hook misreading the branch) rather than let something through. Use it as the should-have layer with `—` as caught-by.

## Format

```
- [YYYY-MM-DD] <should-have> → <caught-by>: <what slipped through, one line>
```

Example:

```
- [2026-03-12] review → bot-review: changed return type to tuple but only reviewed changed files, not callers
```

## Steps

1. Parse `$ARGUMENTS` as `<should-have> <caught-by> <what>`. If any part is missing, ask for it in one question. If the layer names aren't from the list above, map them to the closest one and say so.
2. If `.claude/workflow-gaps.md` doesn't exist, create it from the plugin's `templates/workflow-gaps.md`.
3. Append the line above the `## Resolved` heading (or at the end if there is none).
4. Confirm with the line written and the current count of unresolved gaps. If the count is 5 or more, mention `/gaps`.

Do not fix the underlying issue here; that happens after.

$ARGUMENTS
