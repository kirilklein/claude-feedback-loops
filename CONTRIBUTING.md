# Contributing

## What helps most

- **Calibration patterns that worked.** Open an issue with the [calibration pattern template](.github/ISSUE_TEMPLATE/calibration-pattern.md). Real entries from real PRs are the best documentation this repo can have.
- **Prompt tweaks** to the five commands in `commands/` that make them catch more or ask less. Say which repo you tested on.
- **Template fixes** in `templates/`.

Not wanted: anything that adds a runtime, a dependency, or a database. The whole point is five prompts and three markdown files.

## Testing a command change

Install the plugin from your local checkout:

```
/plugin marketplace add /path/to/claude-feedback-loops
/plugin install feedback-loops@claude-feedback-loops
```

Then run the changed command in a project that has a diff (`/review`) or a PR with human comments (`/retro <number>`). Re-run `/plugin install` after each edit to pick up changes.

## Pull requests

- One change per PR, with a sentence on what it fixed for you.
- Keep command prompts short. If a paragraph does not change behavior, cut it.
- Diagrams live in `assets/` as hand-written SVG; keep the CSS-variable palette so they work in dark mode.
