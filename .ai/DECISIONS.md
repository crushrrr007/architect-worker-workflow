# Architecture Decisions

Record only durable decisions that affect future tasks. Keep entries short and append new decisions instead of rewriting history.

## ADR-001: Use a file-based architect–worker protocol

- **Status:** Accepted
- **Date:** 2026-09-13
- **Decision:** Use `.ai/PROJECT.md` for stable context, `.ai/TASK.yaml` for exactly one active task, `.ai/RESULT.yaml` for worker evidence, and this file for durable decisions.
- **Reason:** Small, version-controlled contracts make task boundaries and reviews reproducible without maintaining a separate coordination service.
- **Consequence:** The architect must reset task and result files when dispatching work, and workers must stop rather than exceed the declared scope.

## Decision template

```markdown
## ADR-NNN: Short decision title

- **Status:** Proposed | Accepted | Superseded
- **Date:** YYYY-MM-DD
- **Decision:** What was decided.
- **Reason:** Why this option was selected.
- **Consequence:** What future work must account for.
```
