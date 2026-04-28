# Slack Post Draft — Context Engineering Part 4: Skills

## For: #tmt-solutions (adjust channel tag for #ai-club)

---

Hey TMT - CMRCL - SEs — Part 4 of the context engineering series. This one took a while because it changed how I build.

Part 1 gave Claude memory.
Part 2 showed what happens when that memory is missing.
Part 3 connected it to CRM, Slack, and GitHub.
This one is about what happens when you give it the actual Salesforce development playbook.

:hammer_and_wrench: Teaching Claude to Build: Context Engineering Part 4 :hammer_and_wrench:

Claude knows Salesforce from training data. It can write Apex, design Flows, scaffold LWC components. But training data has three problems that compound in production: it's outdated, it's approximate, and for some things it's completely missing.

Agent Script — the language for authoring Agentforce agents — launched in 2025 with zero training data in any model. Without the right context, Claude pattern-matches from Python syntax and produces code that looks correct but breaks on the platform. Confident and wrong — the same failure mode from Part 2, but with higher stakes.

The fix is a four-layer stack:

Layer 1: Model training — Apex, LWC, Flow, SOQL. The foundation, broad but imprecise.
Layer 2: sf CLI — live org execution. Not generating from memory, running `sf agent validate` and `sf apex run test` against a real org.
Layer 3: 65 production skills — 30 from Salesforce's official `forcedotcom/afv-library` (just graduated from a community project) + 35 community skills. Structured workflows with templates, scoring rubrics, and hard-stop constraints. These override training data when they conflict.
Layer 4: Agent Script reference files — 24 docs and 18 asset files inside the skill. The entire language spec, execution model, anti-patterns, and known issues. None of it exists in any model's training data.

The case study that convinced me: I'd spent weeks manually wiring 63 agent actions across 7 Agentforce topics through the Agent Builder UI. Scanning 130 Apex classes for @InvocableMethod annotations, mapping I/O parameters through trial and error, debugging routing issues one action at a time. Three skills replace that entire workflow — `/developing-agentforce` auto-scans backing logic, generates .agent files with proper action bindings, validates with `sf agent validate`, previews with live actions (catching the isLocal issue before publish), and scores on a 100-point rubric with a 7-category safety review.

The .agent file becomes version-controlled in git. Diffable. Reviewable. The weeks become minutes.

I also cover the collaboration model — how the SE describes what they need in natural language, skills auto-trigger, Claude builds autonomously through the skill pipeline, and stops at approval gates before anything touches the org. Design decisions and go/no-go stay with the human. Construction and validation are automated.

Part 4 — https://jtehrani84.github.io/context-engineering-skills/
Part 3 — https://jtehrani84.github.io/context-engineering-mcp/
Part 2 — https://jtehrani84.github.io/context-engineering-agentscript/
Part 1 — https://jtehrani84.github.io/claude-context-architecture/
