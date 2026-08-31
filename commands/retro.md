---
description: Learn from human PR feedback — calibrate /review and update lessons
---

Close the loop on the current PR: what did human reviewers catch that `/review` missed?

## Steps

1. **Find the PR**: `gh pr view --json number,url,headRefName` for the current branch. If `$ARGUMENTS` names a PR number, use that instead.

2. **Fetch human feedback**:
   - `gh pr view --json reviews,comments` for top-level comments
   - `gh api repos/{owner}/{repo}/pulls/{pr}/comments` for inline comments
   Filter out bots (bugbot, coverage, CI).

3. **Categorize each comment**: bug/logic, missing edge case, design/architecture, convention violation, or clarification question.

4. **Identify review gaps**: for each bug, edge case, or convention comment, ask: *could `/review` have caught this?* If yes, distill a pattern specific enough to check for next time.

5. **Update calibration**: append to `.claude/review-calibration.md` (create from the plugin's `templates/review-calibration.md` if missing):
   ```
   ## [Category]
   - [Specific pattern to watch for] — learned from PR #NNN
   ```
   No vague entries. "Watch for off-by-one in pagination boundaries" — yes. "Be more careful" — no.

6. **Update lessons**: if a comment revealed a codebase gotcha rather than a review gap, add it to `.claude/lessons.md` under **Observations** (see the confidence ladder in `templates/lessons.md`). If the same gotcha is already there as an Observation, this second confirmation promotes it to **Proven Patterns**.

7. **Report**: what was learned, what was added where. If nothing actionable, say so — an empty retro is a valid result.

$ARGUMENTS
