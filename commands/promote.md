---
description: Audit lessons.md — promote, demote, or retire entries on the confidence ladder
---

Maintain `.claude/lessons.md` so it stays small, current, and trustworthy. Memory tools capture; this command calibrates.

The ladder: **Observation** (noticed once) → **Proven Pattern** (confirmed 2+ times) → **Hard Rule** (a violation caused a real failure). Higher levels override lower ones on conflict.

## Steps

1. **Read** `.claude/lessons.md`. If missing, offer to create it from the plugin's `templates/lessons.md` and stop.

2. **Verify each entry still holds**: if it names a file, function, flag, or command, check it still exists in the repo. Entries about deleted code get retired (removed, with a one-line note in the report).

3. **Promote**:
   - An **Observation** confirmed again since it was written (evidence in recent git history, PR comments, or gap log) → move to **Proven Patterns**, noting both confirmations.
   - A **Proven Pattern** whose violation caused a real failure (a bug, a reverted commit, a CI incident) → move to **Hard Rules**, citing the failure.
   Promote only with evidence you can point to. When it's ambiguous, ask the user rather than guessing.

4. **Demote or retire**:
   - A pattern contradicted by how the code actually works now → demote one level or retire.
   - Duplicates → merge into the highest-confidence copy.

5. **Report**: a short table of moves (entry, from → to, evidence). If nothing moved, say the ladder is current.

$ARGUMENTS
