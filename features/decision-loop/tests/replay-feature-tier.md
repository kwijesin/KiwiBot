# Test: decision-loop / replay-feature-tier

- **Feature:** [decision-loop](../SKILL.md) · **Kind:** prompt
- **What it checks:** replaying the input behind 0033 (round 3 item 4.8: the original planning paragraphs weren't kept, so a closed loop's input is used instead) gives an equivalent Proposed decision, with sensible questions, and stops for the user.

## Fixture
The prompt given to the fresh agent, word for word:

> You are an agent at the root of the repository <worktree>. Follow features/decision-loop/SKILL.md. The user's input is: "use option a". Context, which the user was replying to: "Strictly, 0028 says everything starts at tier 3 except the items on the tier 1 list, and only a new decision can lower a tier. `review-queue` was accepted at tier 1 though it's read-only, which isn't on that list. A new synthesis feature would be in the same position, since it only writes a working summary. Option (a): treat the user's acceptance of a feature, including its declared tier, as the decision that sets its tier, and make that explicit with a short decision that supersedes 0028 rule 5. Option (b): declare synthesis tier 3 and leave 0028 as it is." Run steps 1–6, then stop and reply with your step 6 message. Do not run git.

## Setup
1. Create the worktree at commit **`dfed91a`** (the state just before 0033 existed), not HEAD.
2. Copy the current `features/decision-loop/` from the repo over the worktree's `features/decision-loop/`, so the version under test is the current one.
3. Commit the setup in the worktree.

## Checklist
1. A loop record exists at `docs/decisions/planning/loop-*.md` containing the input "use option a" word for word, with status Open.
2. The candidate is classed as **Supersede 0028** (all of it or rule 5), not as New with no link to 0028.
3. A new decision file, numbered **0033**, has status **Proposed**. It says a feature's approval tier is set or confirmed by the user's acceptance of the feature, without a separate decision.
4. That decision limits the change to **features**. Kinds of change that aren't features still need a decision (or the reply asks about this).
5. A **Proposed** row for it is in `docs/decisions/README.md`.
6. The reply asks **numbered questions, each with a recommended answer**, including at least one equivalent to: "is later lowering a feature's tier just a feature change?" or "must the acceptance review state the declared tier?"
7. **Nothing is Accepted:** no decision is set to Accepted, and `0028-initial-approval-rules.md`, `AGENTS.md` and the task list are unchanged.

## Last run
*(Not run yet. Runs in T13.)*
