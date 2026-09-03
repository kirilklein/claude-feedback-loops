---
description: Calibrated code review — applies patterns learned from past human PR feedback
allowed-tools: Read, Grep, Glob, Bash(git diff:*), Bash(git status:*)
---

You are doing a focused code review.

First, read the project's `CLAUDE.md` (and docs it links). Its instructions win over this prompt on conflict.

Then read `.claude/review-calibration.md` if it exists and apply its patterns alongside the standard checks — these were learned from human reviewers catching things past reviews missed. Also read the **Hard Rules** and **Proven Patterns** sections of `.claude/lessons.md` if present; flag violations of Hard Rules as findings.

Review the target(s) in **$ARGUMENTS** (files, dirs, globs). If empty, review the current diff (`git diff` + staged changes); if there is no diff either, ask for the target.

## What to look for (substantive issues first)

1. **Bugs & logic errors**: edge cases, error handling, validation, race conditions, off-by-one.
2. **Security**: injection, authz/authn mistakes, path traversal, SSRF, hardcoded secrets, insecure defaults.
3. **Performance**: unnecessary I/O, quadratic loops, repeated work, missing batching.
4. **Conventions**: project patterns per CLAUDE.md and lessons.
5. **Maintainability**: clarity, duplication, naming, testability.

## Output

- 1–3 sentence summary of overall risk.
- Issues as bullets, highest severity first. Each: **Severity** (Critical/High/Medium/Low), **Location** (`path:line`), **Problem**, **Fix**. Mark findings that came from a calibration pattern with `[calibrated]` so the loop's value stays visible.

## Decisions to verify

After issues, list places where the change makes a choice the author should consciously confirm — behavioral changes, implicit assumptions (thresholds, fallbacks), contract changes affecting callers, named tradeoffs. Each: **Location**, **Decision** (choice made + alternative), **Impact**. Omit the section if there are none.

Keep it concise; skip nitpicks.

Targets:
$ARGUMENTS
