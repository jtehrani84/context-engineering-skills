# Slack Post Draft — Context Engineering Part 5: Skills

## For: #tmt-solutions, #tmt-cmrcl-solutions, #ai-club

---

Good morning #tmt-solutions - fresh off day 1 of CKO2, where @Ryan Schellack illustrated the fast path to Agentforce adoption with coding agents. I wanted to share my own experience, including the failures, so none of you have to go through it.

:claude-wave::hammer_and_wrench: Context Engineering Part 5 — Teaching Claude to Build Agentforce Agents :hammer_and_wrench::claude-wave:

Weeks back, I worked with Claude to programmatically build a custom Agentforce agent deployed to both a Slack Demo org and an SDO. This wasn't a typical employee or service agent using OOB actions. It was an employee agent with 7 subagents (topics) bound with custom Apex actions calling endpoints of a Node.js application hosted on Cloud Run.

Opus 4.6's training had it thinking it knew how to do this programmatically. It didn't - and I was too new to Claude Code to know that it didn't. We spent 4-5 days debugging and never got there. Turns out our platform and tooling never actually had the capability to programmatically bind custom actions without the legacy Builder or Agentforce Studio. Neither Claude nor I knew this until we finally bound the agent actions manually. After lots of trial and error we got to a successfully deployed agent that works incredibly well for its use case.

Then Agent Script dropped at TDX. Yesterday's CKO2 session showed the GTM motion. And on Tuesday I rebuilt the entire agent - 3 hours, zero Agent Builder clicks.

:test_tube: The rebuild — May 12:
Full 7-topic, 68-action Agentforce agent from scratch. No UI. Pure CLI + Agent Script.
6 iterations to converge:
:x: Multi-file split — wrong. Agent Script is one file.
:x: Actions by name only — wrong. Need target definitions.
:x: Targets in reasoning block — "Unexpected ://"
:x: Top-level actions block — wrong. Per-topic only.
:warning: Correct structure! But output schema mismatches.
:white_check_mark: Parsed flow XML for ground-truth schemas. Published. Live.

The breakthrough was the Salesforce Docs MCP — Claude searched live documentation mid-session and found the canonical pattern that no training data had. 65 production skills caught the structural errors. The docs MCP resolved the hard one.

:chart_with_upwards_trend: Result:
- 7 persona topics, 68 actions bound
- Published via `sf agent publish authoring-bundle`
- Version-controlled. Diffable. Reproducible.
- ~3 hours total (vs. 5 days of failed attempts before Agent Script existed)
- Human involvement: said "go" + one OAuth click

What used to be tedious is now a fun Tuesday afternoon.

:rocket: New: labs.agentforce.com — zero-friction headless access to Agentforce from Claude Code, Codex, or Cursor. No org provisioning. Connect and build in minutes.

Here's the <https://salesforce.enterprise.slack.com/docs/T01G0063H29/F0B33T0T8D8|Slack canvas from CKO> with the full coding agent toolkit (ADLC plugin, ADL Data Libraries, Custom Scorers, Custom Connections).

:link: Full interactive breakdown: https://jtehrani84.github.io/context-engineering-skills/

This is Part 5 of the context engineering series:
:one: https://jtehrani84.github.io/claude-context-architecture/
:two: https://jtehrani84.github.io/context-engineering-agentscript/
:three: https://jtehrani84.github.io/context-engineering-mcp/
:four: https://jtehrani84.github.io/context-engineering-knowledge-graph/
:five: https://jtehrani84.github.io/context-engineering-skills/

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
