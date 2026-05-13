# Slack Post Draft — Context Engineering Part 5: Skills

## For: #tmt-solutions, #tmt-cmrcl-solutions, #ai-club

---

:hammer_and_wrench: **Context Engineering Part 5 — Teaching Claude to Build Agentforce Agents** :hammer_and_wrench:

Part 1 gave Claude memory. Part 2 showed what happens without it. Part 3 connected it to CRM, Slack, and GitHub. Part 4 added a knowledge graph. This one teaches it how to build Salesforce — and proves it with a real agent build.

**The problem:** Claude knows Apex and Flows from training data. But Agent Script — the language for authoring Agentforce agents — launched with zero training data in any model. Without the right context, Claude produces code that looks correct but breaks on the platform.

**The fix:** A four-layer stack:
1. Model training (broad but imprecise)
2. sf CLI (live org execution)
3. 65 production skills (override training data when they conflict)
4. Salesforce Docs MCP (live documentation search mid-session)

:test_tube: **Proof point — May 12:**

Built a full 7-topic, 68-action Agentforce agent from scratch. No Agent Builder UI. Pure CLI + Agent Script.

6 iterations to converge:
:x: Multi-file split — wrong. Agent Script is one file.
:x: Actions by name only — wrong. Need target definitions.
:x: Targets in reasoning block — "Unexpected ://"
:x: Top-level actions block — wrong. Per-topic only.
:warning: Correct structure! But output schema mismatches.
:white_check_mark: Parsed flow XML for ground-truth schemas. Published. Live.

The breakthrough: Salesforce Docs MCP searched live documentation mid-session and found the canonical pattern no training data had. Skills caught the easy errors. The docs resolved the hard one.

:chart_with_upwards_trend: **Result:**
- 7 persona topics, 68 actions bound
- Published via `sf agent publish authoring-bundle`
- Version-controlled. Diffable. Reproducible.
- ~3 hours total (original Agent Builder approach: weeks)
- Human involvement: said "go" + one OAuth click

:rocket: **New: labs.agentforce.com** — zero-friction headless access to Agentforce from Claude Code, Codex, or Cursor. No org provisioning. Connect and build in minutes.

For those internal to Salesforce — there's a Slack canvas from CKO with the full coding agent toolkit (ADLC plugin, ADL Data Libraries, Custom Scorers, Custom Connections). Search "Build Fast with Coding Agents" in Slack.

:link: Full interactive breakdown: https://jtehrani84.github.io/context-engineering-skills/

Series:
Part 5 (this) — https://jtehrani84.github.io/context-engineering-skills/
Part 4 — https://jtehrani84.github.io/context-engineering-knowledge-graph/
Part 3 — https://jtehrani84.github.io/context-engineering-mcp/
Part 2 — https://jtehrani84.github.io/context-engineering-agentscript/
Part 1 — https://jtehrani84.github.io/claude-context-architecture/

---

## LinkedIn Version

**Teaching Claude to Build Salesforce Agents (Context Engineering Part 5)**

Claude knows Salesforce. It can write Apex, design Flows, scaffold components. But Agent Script — the language for authoring Agentforce agents — launched with zero training data in any AI model.

Without proper context engineering, Claude pattern-matches from Python and produces code that looks syntactically correct but fails on the platform. Confident wrong code is worse than no code.

The fix is a four-layer stack:
1. Model training — broad foundation
2. sf CLI — live org execution, not memory
3. 65 production skills — structured workflows that override training data when they conflict
4. Live documentation search — MCP server queries Salesforce docs mid-session

I tested this by building a full Agentforce agent from scratch. 7 topics. 68 actions. No UI. Pure CLI.

It took 6 iterations. That's the real story — not "it worked perfectly," but "the system caught errors early, gave actionable feedback, and converged." Skills don't write perfect code on try 1. They give you the iteration loop that converges.

Result: a production agent published via `sf agent publish authoring-bundle` in ~3 hours. The same build took weeks through the Agent Builder UI. Version-controlled in git. Diffable. Reproducible.

The gap isn't model intelligence. It's context. Same model, dramatically different output based on what it knows about YOUR platform, YOUR patterns, YOUR constraints.

Interactive breakdown with architecture diagrams and iteration details:
https://jtehrani84.github.io/context-engineering-skills/

#ContextEngineering #AgentScript #Agentforce #ClaudeCode #SalesforceAI #SolutionsEngineering
