---
description: Format → lint → test → review → commit → push, tracking gaps between stages
---

Run the full pre-push pipeline autonomously. Fix issues inline; do not pause for confirmation between steps.

## Steps

1. **Understand changes**: `git status` and `git diff`; identify changed source files.
2. **Verify branch**: STOP if on `main`/`master`/`dev` — tell the user to switch to a feature branch.
3. **Format**: run the project's formatter on changed files; stage the result.
4. **Lint**: run the linter on changed files; fix and re-run until clean.
5. **Test**: run tests relevant to the changed files (use the project CLAUDE.md's test mapping if one exists; otherwise infer from directory structure). Not the whole suite. Fix failures before proceeding.
6. **Review**: invoke `/review` on the changes. Fix reported issues, then re-run steps 3–5.
7. **Commit**: descriptive message matching the repo's style (`git log --oneline -10`).
8. **Push**: to the current feature branch.

If a step fails, fix and retry from that step.

## Gap tracking (the point of this pipeline)

Whenever a later step catches something an earlier step should have caught — review finds what lint/tests missed, tests fail on what format/lint passed, CI later fails on what this pipeline passed — append one line to `.claude/workflow-gaps.md` (create from the plugin's `templates/workflow-gaps.md` if missing):

```
- [YYYY-MM-DD] step N (name) missed [what] — caught by step M (name)
```

Terse, one line per gap. Run `/gaps` periodically to turn the accumulated entries into pipeline improvements.
