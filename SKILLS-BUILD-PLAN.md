# Skills Build Plan — Demo Org Enhancement

**Purpose:** Real-world builds using AFV skills that (1) enhance the demo org, (2) strengthen AIP, (3) advance the Headless 360 demo, and (4) produce case studies for the Part 4 write-up.

**Demo Org Current State:**
- 127 Apex classes (66 @InvocableMethod, 36 test classes, 12 @AuraEnabled)
- 12 custom objects, 194 fields, 3 triggers
- 7 Agentforce topics, 63 agent actions (Flows + Apex)
- 13 LWC, 2 permission sets
- No .agent files (all config was manual Agent Builder)
- No custom FlexiPages for AIP objects
- Data Cloud: schema exists, 0 configured

---

## Track 1: Agentforce Agent Rebuild (Highest Impact)

**Goal:** Reverse-engineer the existing 7-topic, 63-action agent into `.agent` files using `/developing-agentforce`. First real test of the skill pipeline against a production-complexity agent.

| Step | Skill | What it produces | Value |
|------|-------|-----------------|-------|
| 1a | `/developing-agentforce` (Comprehend) | Agent Spec documenting current 7 topics, 63 actions, routing logic | First-ever design doc for AIP's agent layer |
| 1b | `/developing-agentforce` (Create) | `.agent` file with full topic graph, action bindings, instructions | Version-controlled agent config in git |
| 1c | `/testing-agentforce` (Mode B) | Test spec YAML covering all 7 topics | Regression suite — catches breaks on future changes |
| 1d | `/observing-agentforce` | Baseline session trace analysis | Production health snapshot before any changes |

**Case study value:** "We rebuilt a 63-action agent from Agent Builder into a `.agent` file in one session. Here's the scoring report."

**Bonus:** Once the .agent file exists, adding Topic 8 (Headless 360 demo scenario) becomes a code change, not a UI walkthrough.

---

## Track 2: Apex Quality Uplift (Scoring Showcase)

**Goal:** Run `/generating-apex` and `/generating-apex-test` against real AIP code to demonstrate the 150-point scoring and validation pipeline.

| Step | Skill | What it produces | Value |
|------|-------|-----------------|-------|
| 2a | `/generating-apex` (Review) | Scoring report on 3-5 key service classes | Baseline quality score for AIP Apex |
| 2b | `/generating-apex-test` | New/improved test classes for coverage gaps | Better test coverage (36 tests for 127 classes is thin) |
| 2c | `/generating-apex` (Create) | New service class for Headless 360: `WhaleHunterLifecycleService.cls` | Whale Hunter 10-stage orchestration in Apex, scored and validated |
| 2d | `/trigger-refactor-pipeline` | Refactored handler for one of the 3 triggers | Before/after of trigger modernization |

**Case study value:** "Here's an Apex class scored at 142/150, with code analyzer clean and 95% test coverage. Generated in 4 minutes."

**Specific classes to review/generate:**
- Review: `AccountIntelligenceService.cls` (core service)
- Review: `PlaybookGenerationService.cls` (complex orchestration)
- Generate: `WhaleHunterLifecycleService.cls` (new — 10-stage lifecycle with state machine)
- Generate: `HeadlessContextService.cls` (new — unified context assembly for Headless 360)
- Refactor: `AccountIntelligenceTrigger.trigger` → handler pattern

---

## Track 3: Metadata & Lightning Pages (Visual Polish)

**Goal:** Use metadata generation skills to fill gaps in the demo org that make demos look unfinished.

| Step | Skill | What it produces | Value |
|------|-------|-----------------|-------|
| 3a | `/generating-flexipage` | Custom Record Page for Account_Intelligence__c | Proper Lightning page instead of default layout |
| 3b | `/generating-flexipage` | Custom Record Page for Opportunity_Plan__c | Showcase the Opp Plan system with proper UX |
| 3c | `/generating-flexipage` | App Home Page for Meridian Intelligence app | Branded landing page with dashboards and quick actions |
| 3d | `/generating-custom-field` | 5-10 fields on Account for Headless 360 signals | External signal capture (tech adoption, hiring, earnings) |
| 3e | `/generating-permission-set` | `Headless_360_User` permission set | Proper access control for the H360 demo |
| 3f | `/generating-validation-rule` | 2-3 rules on Opportunity_Plan__c | Data quality for the Opp Plan system |
| 3g | `/generating-list-view` | Account Intelligence list views (by status, by tier) | Demo-ready filtered views |

**Case study value:** "Seven pieces of metadata generated from natural language descriptions. Each deployed on first attempt."

---

## Track 4: Flow Generation (Grounded Pipeline Demo)

**Goal:** Use `/generating-flow` to build Flows that extend AIP and support Headless 360 scenarios.

| Step | Skill | What it produces | Value |
|------|-------|-----------------|-------|
| 4a | `/generating-flow` | Record-Triggered Flow on External_Signal__c (after insert) → create Intelligence_Request__c | Auto-trigger analysis when signals arrive |
| 4b | `/generating-flow` | Screen Flow for Whale Hunter stage progression | Interactive demo flow for SE walk-throughs |
| 4c | `/generating-flow` | Scheduled Flow for stale intelligence cleanup | Ops hygiene — archive old analyses |

**Case study value:** "The Flow skill grounded against our actual object metadata before generating. It knew External_Signal__c has a Source__c field because it queried the org first."

---

## Track 5: Headless 360 Agent (Net-New Build)

**Goal:** Build a brand-new Agentforce agent for Headless 360 using `/developing-agentforce` from scratch. This is the cleanest case study — zero manual work, full skill pipeline.

| Step | Skill | What it produces | Value |
|------|-------|-----------------|-------|
| 5a | `/developing-agentforce` (Create) | Agent Spec for Headless 360 agent: 3-4 topics (Signal Detection, Context Assembly, Deal Strategy, Execution Planning) | Design doc from natural language |
| 5b | `/generating-apex` | 3-4 new invocable Apex classes for H360 actions | Backing logic with scoring |
| 5c | `/generating-custom-lightning-type` | CLTs for complex action I/O (signal payloads, context objects) | Proper type-safe agent I/O |
| 5d | `/developing-agentforce` (Deploy) | Published, activated Headless 360 agent | Working agent, live in org |
| 5e | `/testing-agentforce` (Mode A + B) | Ad-hoc preview + batch test suite | Validated with evidence |

**Case study value:** "A four-topic Agentforce agent built from a one-paragraph description. No Agent Builder. No manual wiring. 20 minutes."

---

## Track 6: UI Bundle App (Visual Wow)

**Goal:** Build a React-based Headless 360 dashboard on Salesforce using the UI Bundle skill chain.

| Step | Skill | What it produces | Value |
|------|-------|-----------------|-------|
| 6a | `/building-ui-bundle-app` | Full React app: H360 Intelligence Dashboard | Visual showpiece for demos |
| 6b | `/using-ui-bundle-salesforce-data` | Data access to Account_Intelligence__c, External_Signal__c | Live Salesforce data in React |
| 6c | `/implementing-ui-bundle-agentforce-conversation-client` | Embedded Agentforce chat in the dashboard | "Talk to your data" UX |
| 6d | `/deploying-ui-bundle` | Deployed to Experience Site | Accessible URL for demos |

**Case study value:** "A complete React dashboard with live Salesforce data and embedded Agentforce chat. Built and deployed in one session."

---

## Track 7: Data Cloud Activation (sf-* Only)

**Goal:** Activate Data Cloud as the intelligence fabric for Headless 360. No AFV skills here — sf-* only.

| Step | Skill | What it produces | Value |
|------|-------|-----------------|-------|
| 7a | `/sf-datacloud-connect` | Data streams from Account_Intelligence__c, External_Signal__c | Data Cloud ingestion |
| 7b | `/sf-datacloud-harmonize` | DMOs for intelligence data | Unified customer data model |
| 7c | `/sf-datacloud-segment` | Segments: high-intent accounts, stale intelligence, at-risk renewals | Actionable audience segments |
| 7d | `/sf-datacloud-act` | Activations: trigger Flows, update records, Agentforce Data Graphs | Close the loop |

**Case study value:** "Data Cloud activated using 4 skills in sequence. The same pipeline that AIP uses for intelligence now feeds into Agentforce via Data Graphs."

---

## Recommended Build Order

**Phase 1 — Quick Wins (1 session):** Tracks 2a, 3a-3b, 3g
- Review 2-3 Apex classes for scoring screenshots
- Generate FlexiPages for Account_Intelligence__c and Opportunity_Plan__c
- Create list views
- **Produces:** Scoring reports + deployed Lightning pages for write-up screenshots

**Phase 2 — The Main Event (1-2 sessions):** Track 1 (full) + Track 5a-5b
- Rebuild AIP agent as .agent file
- Start Headless 360 agent design
- **Produces:** The centerpiece case study for Part 4

**Phase 3 — Deep Build (2-3 sessions):** Tracks 2c-2d, 4, 5c-5e, 3d-3f
- New Apex services for H360
- Trigger refactor
- Flow generation
- Complete H360 agent build
- **Produces:** Full-stack demo org enhancement

**Phase 4 — Visual + Data (2 sessions):** Tracks 6, 7
- UI Bundle dashboard
- Data Cloud activation
- **Produces:** The "wow" demo + intelligence fabric

---

## What This Produces for Part 4 Write-Up

After completing Phases 1-2, the write-up gains:

1. **Apex scoring screenshot** — real 150-point report from `/generating-apex`
2. **Agent rebuild story** — 63 actions from Agent Builder UI → .agent file in one session
3. **Before/after FlexiPages** — default layout → polished Lightning page
4. **Grounded Flow generation** — the 3-step MCP pipeline in action
5. **Net-new agent from scratch** — the cleanest demo of the full pipeline

Each becomes a section on the Part 4 GitHub Pages site with screenshots, timing, and scoring data.
