# claude-feedback-loops

**Feedback loops your memory plugin doesn't close.**

Memory tools (claude-mem, Claude Code's native memory) are great at *capturing* what happened. They hoard; they don't calibrate. This plugin adds the missing half: three small loops that turn what happened into behavior that actually changes.

```
human PR feedback ──/retro──▶ review-calibration.md ──▶ sharper /review
pipeline misses  ──/ship───▶ workflow-gaps.md ───────▶ /gaps tightens the pipeline
repeated gotchas ──────────▶ lessons.md ─────────────▶ /promote moves them up the ladder
```

Five slash commands, three markdown files, no runtime, no database. Works *alongside* whatever memory setup you already have.

## Install

```
/plugin marketplace add kirilklein/claude-feedback-loops
/plugin install feedback-loops@claude-feedback-loops
```

## The loops

### 1. Review calibration — `/retro` → `/review`

After humans review your PR, run `/retro`. It reads their comments, asks *"could `/review` have caught this?"*, and writes each miss as a concrete pattern to `.claude/review-calibration.md`:

```
## Bugs
- Watch for off-by-one at pagination boundaries when page_size divides the total — learned from PR #17
```

`/review` loads these patterns every time it runs and tags findings they produce with `[calibrated]`, so you can see the loop paying for itself. Your reviews get sharper with every PR that gets human eyes.

### 2. Pipeline gap tracking — `/ship` → `/gaps`

`/ship` runs format → lint → test → review → commit → push. Its real job is noticing when a **later step catches what an earlier one should have** — review flagging what lint missed, CI failing on what tests passed — and logging one line to `.claude/workflow-gaps.md`.

`/gaps` clusters the log by root cause and closes each cluster at the cheapest layer: a lint config change beats a calibration entry beats a lesson that relies on being remembered. The pipeline tightens itself.

### 3. The confidence ladder — `lessons.md` → `/promote`

The problem with accumulated lessons is that they're all treated equally — a hunch from March sits next to a rule that prevented a production bug. The ladder fixes that:

| Level | Meaning | How an entry gets here |
|---|---|---|
| **Hard Rules** | Mandatory. | A violation caused a real failure |
| **Proven Patterns** | Default to following. | Confirmed 2+ times |
| **Observations** | Context, not gospel. | Noticed once |

`/promote` audits the file: promotes entries with fresh evidence, demotes ones the code has moved past, retires ones about deleted code. Your lessons file stays small and trustworthy instead of growing into a second codebase.

## Files it maintains (per project, in `.claude/`)

| File | Written by | Read by |
|---|---|---|
| `review-calibration.md` | `/retro` | `/review` |
| `workflow-gaps.md` | `/ship` | `/gaps` |
| `lessons.md` | `/retro`, you | `/review`, `/promote` |

All plain markdown, checked into git, shared with your team. Templates in [`templates/`](templates/).

## What this is not

- Not a memory system — pair it with one; it calibrates what memory captures.
- Not a framework — five prompts and three markdown files you can read in ten minutes.
- Not magic — the loops only close if you run `/retro` after human reviews and `/gaps` occasionally. That's the whole discipline.

## License

MIT
