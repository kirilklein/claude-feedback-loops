## Pipeline gaps

When a later stage catches what an earlier one should have — CI fails on what passed locally, a reviewer or bot finds what tests or `/review` missed, a bug reaches production — run `/gap <should-have> <caught-by> <what>` before fixing it. Run `/gaps` when the log has 5+ entries.
