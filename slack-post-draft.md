# Slack Post Draft — Context Engineering Part 4: Skills

## For: #tmt-solutions (adjust channel tag for #ai-club)

---

Hey TMT - CMRCL - SEs — Part 4 of the context engineering series. This one has real proof data.

Part 1 gave Claude memory.
Part 2 showed what happens when that memory is missing.
Part 3 connected it to CRM, Slack, and GitHub.
This one is about what happens when you give it the actual Salesforce development playbook — and then watch it fail, learn, and succeed.

:hammer_and_wrench: Teaching Claude to Build: Context Engineering Part 4 :hammer_and_wrench:

Claude knows Salesforce from training data. It can write Apex, design Flows, scaffold LWC components. But training data has three problems that compound in production: it's outdated, it's approximate, and for some things it's completely missing.

Agent Script — the language for authoring Agentforce agents — launched in 2025 with zero training data in any model. Without the right context, Claude pattern-matches from Python syntax and produces code that looks correct but breaks on the platform.

The fix is a four-layer stack:
- Layer 1: Model training (broad but imprecise)
- Layer 2: sf CLI (live org execution, not memory)
- Layer 3: 65 production skills (override training data when they conflict)
- Layer 4: Salesforce Docs MCP (live documentation search mid-session)

:test_tube: The Proof Point (this actually happened May 12)

I asked Claude to build a full 7-topic, 68-action Agentforce agent from scratch using Agent Script. No Agent Builder UI. Pure CLI.

It took 6 iterations to get right:
1. :x: Multi-file split — wrong. Agent Script is one file.
2. :x: Actions by name only — wrong. Need target definitions.
3. :x: Targets in reasoning block — wrong. "Unexpected ://"
4. :x: Top-level actions block — wrong. Per-topic only.
5. :warning: Correct structure! But output schema mismatches (Apex names vs Flow names).
6. :white_check_mark: Parsed flow XML for ground-truth schemas. Published. Live.

The breakthrough wasn't skill knowledge alone. It was the Salesforce Docs MCP — Claude searched the live Salesforce documentation mid-session and found the canonical two-level pattern that no training data had. Skills caught the easy errors. The docs MCP resolved the hard one.

:chart_with_upwards_trend: Result: Meridian Intelligence Agent

- 7 persona-based topics (Intelligence, Sales Coach, Service, Marketing, BDR, Quoting, Workspace)
- 68 actions bound (all 57 existing + new intelligence atoms)
- Published via `sf agent publish authoring-bundle` — no UI
- Version-controlled in git. Diffable. Reproducible.
- Total build time: ~3 hours (original estimate: "7-9 days")
- Human involvement: said "go" + clicked one OAuth prompt

The existing agent (built over weeks in Agent Builder UI) still runs as fallback. The new one runs alongside it — same actions, better routing, deterministic patterns for 80% of usage.

:brain: What This Proves About Skills

Skills didn't write perfect code on try 1. They:
- Caught structural errors before hitting the server (local validator)
- Gave actionable feedback at each step (exact line numbers, "did you mean?")
- Converged on the right answer through systematic elimination
- Resolved blockers programmatically (CLI update, permission assignment, orphan cleanup — all without opening a browser)

That's what makes them better than training data alone. Training data gives you a plausible first attempt. Skills give you the iteration loop that converges.

:link: The stack in action: skills + sf CLI + Salesforce Docs MCP + Tooling API = a full agent published from the terminal while the owner did yard work.

Part 4 — https://jtehrani84.github.io/context-engineering-skills/
Part 3 — https://jtehrani84.github.io/context-engineering-mcp/
Part 2 — https://jtehrani84.github.io/context-engineering-agentscript/
Part 1 — https://jtehrani84.github.io/claude-context-architecture/
