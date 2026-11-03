# KiwiBot

KiwiBot is my personal assistant, efficiency accelerator and an additional interface between me, my own environment and the digital world ([0002](docs/decisions/0002-purpose.md)). It started as **Lulu**, named after the Lululemon Mirror that sparked the idea ([0003](docs/decisions/0003-name.md)).

It's an orchestration of agents, scripts, services, hardware and UI apps that **builds and improves itself as it's used** ([0004](docs/decisions/0004-orchestration-and-self-improvement.md), [0024](docs/decisions/0024-building-is-using.md)). So the first thing built is the self-improvement loop, not the assistant features ([0022](docs/decisions/0022-first-build-priority.md)).

> **Status:** Planning is complete. Building starts with milestone M0 in the [task list](docs/tasks/task-list.md).

## Start here

**Agents:** read [AGENTS.md](AGENTS.md) first.

1. [Decisions](docs/decisions/): what KiwiBot is and why (0001–0027).
2. [Deferred decisions](docs/decisions/deferred.md): what's been consciously put off.
3. [Task list](docs/tasks/task-list.md): what to build next.

## Repository layout

```
KiwiBot/
├── README.md               ← you are here
├── AGENTS.md               ← entry point and working rules for any agent
├── CLAUDE.md               ← imports AGENTS.md for Claude
├── features/               ← one folder per feature, Agent Skills format (0032)
├── inbox/                  ← the user's rough ideas, waiting to be triaged (0034)
└── docs/
    ├── README.md           ← documentation index
    ├── decisions/          ← decisions (NNNN-*.md), deferred register, planning process
    ├── tasks/              ← task list (bootstrap until the custom task system exists)
    ├── reviews/            ← one review note per task (0029)
    ├── standards/          ← style guide, testing guide
    ├── history/            ← archived intermediate files (planning rounds)
    ├── dependencies.md     ← external resources KiwiBot relies on
    ├── architecture.md     ← decided shape; mostly placeholder
    ├── models.md
    ├── hardware.md
    ├── magicmirror.md
    ├── privacy-security.md
    ├── roadmap.md
    ├── configuration.md    ← placeholder
    ├── setup.md
    └── skills.md           ← placeholder
```

## Credits & references

- Lululemon Mirror hardware conversion: [olm3ca/mirror](https://github.com/olm3ca/mirror)
- [MagicMirror²](https://magicmirror.builders/)
