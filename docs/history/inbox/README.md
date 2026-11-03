# Triaged inbox items

Items from [inbox/](../../../inbox/) that [inbox-triage](../../../features/inbox-triage/SKILL.md) has routed or dropped ([0036](../../decisions/0036-inbox-triage.md)). Parked items stay in the inbox.

Each item keeps its file name and its body, unchanged (0034). Triage adds this front matter, merged into any front matter the item already has:

```markdown
---
triaged: 2026-11-03
route: decision-loop        # decision-loop | task-planner | existing-task | drop
route_ref: loop-2026-11-03-<slug>   # the loop record, the task ID (e.g. T23), or the reason for a drop
---
```

A `.txt` item gets the same front matter as its first lines.
