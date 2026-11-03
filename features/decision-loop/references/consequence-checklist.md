# Consequence checklist

Run every candidate through this list. Write down only what applies. "Nothing" is a fine answer for most rows.

| # | Check | Ask |
|---|---|---|
| 1 | **Dependencies** | Which accepted decisions does it build on? Are they still compatible with it? |
| 2 | **Conflicts** | Does it contradict an accepted decision, or another candidate in this loop? If so, it's a Supersede, or a question for the user. |
| 3 | **Knock-on decisions** | Does it force or invite another decision? That becomes a new candidate. |
| 4 | **Deferred items** | Does it resolve, change or trigger any row in `deferred.md`? Does a revisit trigger now fire? |
| 5 | **Approval (0025, 0028)** | What tier would the resulting features or changes need? Does it lower a tier? Lowering a tier needs its own decision that gives a reason. |
| 6 | **Testing (0012)** | How would the result be tested? Is that possible yet, given no sandbox (D02)? |
| 7 | **Models (0005, 0020)** | Does it tie anything to a specific model or provider? Does it need frontier or local models? |
| 8 | **Resources (0015)** | Tokens, the user's attention, local compute, cash. Does it trade one for another? |
| 9 | **Style and conventions (0010, 0030, 0032)** | Does it fit the feature types, casing and feature layout? Does it need a new feature type? |
| 10 | **Security (0014, D34)** | Secrets, data sent to cloud models, physical-world actions (D27). Early protections are cheap. |
| 11 | **External dependencies** | Does it add a runtime, tool, service or account? If so, it goes in `docs/dependencies.md` when built. |
| 12 | **Tasks** | Which existing tasks change, become unblocked, or become unnecessary? What new work does it imply? Note the work only; T11 creates the tasks. |
| 13 | **Docs** | Which docs would no longer match (`architecture.md`, `roadmap.md`, `AGENTS.md`, …)? List them; don't edit them here. |
