# Skills / Tools

> **Placeholder.** Runtime skills (capabilities a model can call) aren't designed yet. The skill format is deferred ([D17](decisions/deferred.md)), and skills will be one of the feature types in the style and testing frameworks (0011, 0013).

## Relevant decisions

- **Grow code, not prompts (0007):** repeated work done by a model should become a skill, script or feature.
- **Approval tiers (0025):** every new skill considers what approval it needs. Physical-world actions are covered by D27.
- **Open source vs custom (0023):** use existing tools where they're easy to integrate.

## Candidate skills

These ideas came from the early drafts. None are decided.

`home.control`, `home.status`, `timer` / `alarm`, `reminder`, `calendar`, `weather`, `web.search`, `memory.remember` / `memory.recall`, `display.show` / `display.clear` (mirror), `ask_cloud`.
