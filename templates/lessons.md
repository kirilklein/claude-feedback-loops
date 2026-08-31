# Lessons

Organized by confidence level. Higher levels override lower ones on conflict.
Entries move up the ladder via `/promote`: Observation → (confirmed again) → Proven Pattern → (violation caused a real failure) → Hard Rule.

## Hard Rules
> Violations caused real bugs or failures. Mandatory.

<!-- - Never call `process()` without checking `is_initialized` — silent data corruption (PR #42) -->

## Proven Patterns
> Worked 2+ times. Default to following.

<!-- - New endpoints: copy the pattern from `users.py` — handles auth, validation, errors -->

## Observations
> Noticed once. Useful context, not yet proven.

<!-- - Test suite is faster with per-class DB fixtures -->
