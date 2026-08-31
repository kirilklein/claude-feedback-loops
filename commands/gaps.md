---
description: Review accumulated pipeline gaps and tighten the /ship pipeline
---

Turn the gap log into pipeline improvements. Run this every week or two, or when `.claude/workflow-gaps.md` has 5+ entries.

## Steps

1. **Read** `.claude/workflow-gaps.md`. If empty or missing, report that the pipeline has no recorded gaps and stop.

2. **Cluster** entries by root cause, not by step number. Examples: "lint config doesn't cover async rules", "test mapping misses the `cli/` directory", "review keeps catching unformatted docstrings".

3. **Propose one fix per cluster**, preferring the cheapest layer that closes it:
   - a linter/formatter config change (closes the gap mechanically — best)
   - an addition to the project CLAUDE.md test mapping
   - a calibration entry in `.claude/review-calibration.md`
   - a lessons entry (last resort — relies on being remembered)

4. **Apply** fixes the user approves. For config changes, show the diff first.

5. **Prune the log**: move addressed entries under a `## Resolved` heading with a one-line note of what fixed them. Leave unresolved ones in place.

6. **Report**: clusters found, fixes applied, gaps remaining.

$ARGUMENTS
