---
id: "allzy.framework.docs.05.triage-and-maintenance"
title: "05 — Triage and Maintenance"
artifact_type: "Framework Documentation"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - triage
  - maintenance
---

# 05 — Triage and Maintenance

## Summary

Triage and Maintenance define how the Allzy Framework handles bugs, regressions, UI mismatches, incomplete implementation work, and targeted corrections without falling into Eager Execution.

Maintenance is not a smaller version of feature development. It is often more dangerous. Bugs arrive with screenshots, vague descriptions, voice-to-text fragments, partial error messages, misleading visual symptoms, and pressure to fix the visible problem quickly. If an implementation agent receives that raw context directly, it tends to search broadly, inspect too much, consume unnecessary context, patch symptoms, and mix unrelated concerns.

The Allzy Framework separates the work into two agents:

```text
Agent 1 = Triage Intake / Diagnostician / Handoff Compiler
Agent 2 = Executor / Surgeon
```

Agent 1 absorbs messy, visual, exploratory, or expensive context and converts it into one or more scoped Agent-2 handoff blocks. Agent 1 does not write code. Agent 1 does not produce patches. Agent 1 does not modify files.

Agent 2 receives a compact, scoped handoff and performs the implementation work. Agent 2 should normally not receive raw screenshots, long conversations, unrelated context, or broad browser/computer-use tasks. It should receive only what it needs to inspect, change, verify, and report.

The goal is simple:

```text
Move expensive diagnosis to Agent 1.
Give Agent 2 the smallest safe implementation scope.
```

This reduces token usage, context pollution, wrong-file discovery, hallucination risk, subscription/usage pressure, and follow-up rework.

---

## Source Authority

This document is based on the current Allzy Framework workflow, finalized prompts, finalized templates, finalized examples, repository structure, and practical usage decisions.

Older documentation and previous master specifications are useful input, but they are not automatically correct. When old wording conflicts with the finalized Triage Intake Prompt, the current Yin/Yang contract rules, State Management rules, Prompt Library / Reference Package workflow, or practical Agent-1/Agent-2 workflow, the current workflow wins.

This document is explanatory framework documentation. It is not itself a copy-ready Triage Intake Prompt. The copy-ready operational prompt is stored separately in the prompt templates.

---


---

## Relationship to Workspace / Context Prompts

Triage may use workspace/context artifacts, but it is not the same workflow as workspace context setup or state maintenance.

The related prompt families have separate jobs:

| Prompt/workflow | Role in relation to Triage |
|---|---|
| `workspace_context_initialization_prompt.md` | Prepares the target implementation workspace before future agents work there |
| `workspace_state_maintenance_prompt.md` | Cleans and compresses living state such as `plan.md`, `memory.md`, and `skills/` |
| `context_retrieval_builder_prompt.md` | Retrieves and packages relevant context before or during Triage |
| `document_metadata_enrichment_prompt.md` | Adds metadata/frontmatter to documents so they can participate in deterministic retrieval |
| Triage prompts | Diagnose maintenance input and produce scoped Agent-2 handoffs |

Triage can consume outputs from these workflows.

Triage does not replace them.

### Context Retrieval Builder Before Triage

The Context Retrieval Builder may be used before Triage when the user needs a source pack, review context, or context package for a maintenance issue.

It may produce outputs such as:

```text
agent_context_package
patch_handoff_context
review_context
document_source_pack
deep_brief
summary
```

When such a package is provided, Agent 1 should use it as selected context rather than asking Agent 2 to rediscover everything.

### Context Packages in Triage

A task-specific context package may support an Agent-2 handoff.

It may include:

- task
- search goal
- documents matched
- relevant excerpts
- memory excerpts
- paired Yin/Yang references
- exclusions
- Search Log
- open questions
- handoff notes

A context package is temporary task context.

It is not permanent memory.

Confirmed lasting facts should be moved into `memory.md` through the state-management workflow.

### Workspace State Maintenance Is Not Triage

Workspace State Maintenance maintains living workspace state.

It should not be used to diagnose bugs or create Agent-2 implementation handoffs.

It should not rewrite application code.

It should not perform Triage.

Triage may recommend that `plan.md`, `memory.md`, or `skills/` be updated after a fix, but the actual cleanup/compression of those files belongs to the state-maintenance workflow.

### Document Metadata Enrichment Before Triage

If relevant documents exist but lack useful metadata, Document Metadata Enrichment may be used before deterministic retrieval.

This makes the documents easier to select later through:

- `id`
- `document_type`
- `layer`
- `module_id`
- `submodule_id`
- `tags`
- `aliases`
- `paired_yin`
- `paired_yang`
- `retrieval_description`

Document Metadata Enrichment does not diagnose bugs and does not create Triage handoffs.


## Core Maintenance Principle

Maintenance must be treated as controlled diagnosis followed by scoped execution.

The default sequence is:

```text
Observe bug
→ collect screenshot / description / errors / rough location
→ Agent 1 diagnoses and scopes
→ Agent 1 generates one or more Agent-2 handoff blocks
→ Agent 2 executes one scoped handoff
→ verify against acceptance criteria
→ update contracts or state documentation if behavior changed
```

Do not start maintenance by giving Agent 2 raw screenshots and saying "fix this."

That pattern creates three failures:

1. Agent 2 spends too much context rediscovering what the user already observed.
2. Agent 2 may browse the repository too broadly and modify the wrong area.
3. Agent 2 may patch visible symptoms without understanding contract, state, or scope boundaries.

Triage exists to prevent that.

---

## Why Maintenance Needs Structure

Feature work usually starts from an intended behavior. Maintenance starts from a failure. That changes the risk profile.

A bug report rarely arrives as a clean specification. It may contain:

- a screenshot with no technical location
- a visual mismatch
- a UI behavior that is hard to describe
- a voice-to-text explanation with rough wording
- a stack trace without product context
- a console error without root cause
- several unrelated issues visible at once
- an unclear distinction between expected and actual behavior
- a user request that mixes bugfix, polish, and new feature work

Without triage, an AI agent is likely to optimize locally: fix what is visible, touch what is easiest to find, and ignore hidden contracts or state boundaries.

The Allzy Framework turns messy maintenance input into a structured execution artifact before implementation begins.

---

## Maintenance Failure Modes

### Eager Execution

Eager Execution happens when an AI agent starts modifying code before the problem has been scoped.

Symptoms:

- the visible symptom is patched
- the root cause remains
- adjacent behavior breaks
- the fix touches unrelated files
- state synchronization becomes worse
- the implementation diverges from Yin/Yang contracts
- the next bug appears from the same cause

Triage prevents Eager Execution by requiring Agent 1 to diagnose and scope before Agent 2 implements.

### Context Collapse

Context Collapse happens when a maintenance session accumulates too much noisy material:

- screenshots
- failed attempts
- partial patches
- speculative reasoning
- unrelated observations
- long chat history
- old errors
- abandoned hypotheses

The model begins to reason from contaminated context. Later outputs are influenced by earlier failed attempts or unrelated details.

Triage prevents Context Collapse by compressing raw material into a clean handoff.

### Scope Drift

Scope Drift happens when a narrow bug report expands into adjacent changes.

Example:

```text
Original issue:
Settings → Input category → collapsible blocks change container height.

Scope drift:
Also redesign Provider settings, add icons, change links, create new provider flow,
and adjust Dashboard layout.
```

This is not one maintenance task. It is several scopes.

Triage prevents Scope Drift by splitting unrelated work into separate handoffs.

### Contract-Blind Fixing

Contract-Blind Fixing happens when Agent 2 fixes code without knowing whether the code or the contract is wrong.

The correct classification must happen first:

| Situation | Correct response |
|---|---|
| Implementation violates correct Yang | Fix implementation against the contract |
| Yang omits required behavior | Update Yang before implementation |
| Yin omits domain intent | Update Yin before Yang or code |
| Yin and Yang conflict | Reconcile documents before implementation |
| State handoff is wrong | Fix state context or handoff |
| Issue is unrelated to current task | Split into a separate handoff |

A code fix must not silently become a contract change.

---

## The Triage System

The Allzy Triage System uses two agents.

```text
User observes issue
      │
      ▼
Agent 1
Triage Intake / Diagnostician / Handoff Compiler
      │
      ▼
Scoped Agent-2 handoff block(s)
      │
      ▼
Agent 2
Executor / Surgeon
      │
      ▼
Targeted implementation
```

The central artifact is no longer a JSON Bug Report.

The central artifact is the **Agent-2 handoff**.

Optional JSON metadata may be included for tooling, automation, future Prism adapters, registries, or structured processing, but JSON is not the primary human handoff.

---

## Agent 1 — Triage Intake / Diagnostician / Handoff Compiler

Agent 1 is the assistant currently processing the triage prompt.

Examples:

- If the prompt is used in ChatGPT, ChatGPT is Agent 1.
- If the prompt is used in Claude, Claude is Agent 1.
- If the prompt is used in Gemini, Gemini is Agent 1.
- If the prompt is used in another assistant, that assistant is Agent 1.

Agent 1 must never assume that Agent 2 is the same model, platform, tool, environment, or chat session.

Agent 2 must be named separately.

### Agent 1 Receives

Agent 1 may receive:

- screenshots
- screen recordings
- visual descriptions
- rough voice-to-text descriptions
- bug reports
- stack traces
- console errors
- network errors
- logs
- expected behavior
- current behavior
- suspected page, module, category, or component
- file names or file hints if known
- relevant constraints
- relevant `plan.md` excerpts
- relevant `memory.md` excerpts
- model prompting reference documents
- platform / execution-environment reference documents

Agent 1 may use vision if available. Agent 1 may interpret screenshots. Agent 1 may reason from visual evidence.

### Agent 1 Does

Agent 1:

1. identifies the observed symptom
2. identifies the expected behavior
3. separates confirmed facts from assumptions
4. identifies the likely product area
5. classifies the work type
6. detects whether the issue is a code bug, contract gap, state issue, visual issue, interaction issue, or unknown
7. checks whether multiple unrelated scopes are present
8. splits unrelated scopes into separate handoff blocks
9. determines Agent-2 target setup
10. checks model/platform reference availability
11. labels optimization or fallback status
12. produces one or more scoped Agent-2 handoff blocks
13. optionally produces JSON metadata
14. warns about blockers or missing references when needed

### Agent 1 Must Not Do

Agent 1 must not:

- write code
- produce patches
- produce diffs
- modify files
- invent file paths as facts
- claim model optimization without a model reference
- claim platform optimization without a platform reference
- silently combine unrelated scopes
- silently decide architecture
- hide contract gaps by turning them into code fixes
- repeat secrets from logs or screenshots
- expose sensitive values in the handoff

Agent 1 is not the fixer. Agent 1 prepares the fix for Agent 2.

---

## Agent 2 — Executor / Surgeon

Agent 2 is the implementation agent.

Agent 2 receives the handoff produced by Agent 1 and executes the scoped work.

Agent 2 may be:

- Claude Code
- Cursor
- Codex CLI
- Codex app
- ChatGPT with files/tools
- Gemini / Antigravity-style execution environment
- a CLI coding agent
- an IDE assistant
- a web-based coding assistant
- a custom API workflow
- another implementation environment

Agent 2 is not defined only by the AI model. It is defined by:

```text
AI model + platform / execution environment
```

### Agent 2 Receives

Agent 2 should receive:

- task
- relevant context
- likely affected area
- file discovery boundaries
- implementation instructions
- scope boundaries
- forbidden actions
- acceptance criteria
- output format
- relevant contract references
- relevant state excerpts
- model/platform-adapted instructions when references are available

Agent 2 should normally not receive:

- raw screenshots
- long visual debugging conversations
- unrelated issue lists
- broad repo-search instructions
- full `memory.md` by default
- full `plan.md` by default
- unfiltered logs containing secrets
- unrelated user speculation

### Agent 2 Does

Agent 2:

1. reads the handoff
2. inspects only the relevant files or narrow discovery area
3. verifies the root cause when possible
4. makes the smallest safe change
5. avoids unrelated refactors
6. avoids architecture decisions not covered by the handoff or contracts
7. reports changed files
8. reports verification results
9. reports unresolved blockers

### Agent 2 Must Not Do

Agent 2 must not:

- expand scope
- fix adjacent issues
- browse the repository broadly unless instructed
- act on unrelated visual observations
- change public contracts without instruction
- modify architecture without an updated contract
- hide uncertainty
- invent missing requirements
- resolve Yin/Yang gaps silently
- process unrelated sub-scopes as one mixed task

---

## Visual Context Compression

A major purpose of Agent 1 is to absorb expensive visual and exploratory context before Agent 2 performs implementation work.

Typical workflow:

1. The user captures screenshots or screen recordings.
2. The user describes the issue in rough natural language, often by dictation.
3. The user gives location context such as page, category, component, or visible UI area.
4. Agent 1 interprets the visual evidence and rough description.
5. Agent 1 converts the messy input into a compact Agent-2 handoff.
6. Agent 2 receives the handoff, not the entire visual debugging session.

This saves context and reduces implementation risk.

Screenshots, browser inspection, repeated visual comparison, and computer-use style exploration can consume large amounts of context. Agent 2 should spend its context on reading and modifying the relevant code, not on rediscovering the visual problem from raw evidence.

Agent 1 should identify:

- observed visual symptom
- expected behavior
- likely product area
- likely affected component or file area
- relevant state or layout boundary
- what Agent 2 should inspect
- what Agent 2 must not touch
- how the fix will be verified

### Example

User input to Agent 1 may look like this:

```text
I am in Settings → Input.
The collapsible input blocks have a default collapsed toggle.
When I enable or disable the default collapsed state, the container height changes.
That should not happen. The panel should keep a fixed height.
Screenshot 1 shows the correct height. Screenshot 2 shows the changed height.
```

Agent 1 should convert that into a scoped handoff:

```text
Likely area:
Settings → Input category → collapsible input blocks

Observed issue:
Toggling default collapsed state changes the container/panel height.

Expected behavior:
The panel keeps a stable fixed height regardless of collapsed/default state.

Agent 2 should inspect:
- Settings Input category component
- collapsible block layout handling
- default collapse state logic
- container height / min-height / overflow behavior

Do not touch:
- Provider settings
- global Settings layout
- Dashboard layout
- unrelated collapse behavior elsewhere
```

This is the value of triage: the implementation agent starts from a precise scope instead of rediscovering the problem.

---

## Token and Computer-Use Cost Control

Triage is also a cost-control mechanism.

The expensive part of AI-assisted maintenance is often not the code edit itself. The expensive part is:

- visual inspection
- browser/computer-use exploration
- screenshot comparison
- broad repository search
- long context reconstruction
- repeated explanation of what the user already knows
- unrelated issue bundling
- failed patches that require rework

Agent 1 can often operate in a high-quota assistant environment where visual diagnosis and rough conversational input are cheap or already included in the user's workflow.

Agent 2 may run in an environment where context, tokens, tool calls, browser inspection, or repository exploration are more constrained.

The framework therefore pushes messy diagnosis to Agent 1 and gives Agent 2 a compact implementation task.

This does not guarantee lower cost in every environment, but it strongly reduces unnecessary context consumption and reduces the probability of rework.

---

## Atomic Scope and Same-Area Bundling

Triage must keep implementation scope small.

The default rule is:

```text
One bug.
One topic.
One narrow functional area.
One Agent-2 handoff.
```

This is not only an organizational preference. It is a model-safety and cost-control rule.

AI agents do not reliably execute unrelated fixes in a clean sequential order. When multiple unrelated issues are bundled into one prompt, the model tends to reason across them at the same time. This increases:

- attention dilution
- context contamination
- wrong-file discovery
- hallucination risk
- token usage
- implementation drift
- output inconsistency
- follow-up rework

A smaller handoff usually produces a better fix.

### Same-Area Bundles

Multiple small changes may be grouped only when they belong to the same narrow context.

Allowed grouping examples:

- several copy fixes inside the same Settings category
- a visual spacing fix and nearby button placement inside the same component
- multiple related controls inside the same form section
- related validation fixes in the same workflow
- several small changes required to complete one clearly bounded bug fix
- one layout bug plus one adjacent label change inside the same component
- two visual adjustments that share the same DOM/container boundary
- multiple small fixes caused by the same root cause

A same-area bundle must share at least one of the following:

- same page
- same category
- same component
- same file area
- same workflow
- same state boundary
- same root cause

Same-area bundling is allowed because Agent 2 can reason from the same context and inspect the same narrow code area.

### Unrelated Scope Must Be Split

Do not bundle unrelated issues by default.

Forbidden grouping examples:

- Settings/Input collapse bug plus Settings/Provider feature work
- Settings issue plus Dashboard layout issue
- login bug plus notification bug
- UI polish plus backend state migration
- several unrelated bugs visible in the same screenshot
- "fix everything on this page" without a narrow scope
- unrelated Settings categories with different state logic
- visual bug plus new feature request
- code cleanup plus functional bugfix
- provider icon changes plus provider creation flow changes unless they share one defined component/root cause

Different category means separate handoff.

Different module means separate handoff.

Different root cause means separate handoff.

Different workflow means separate handoff.

---

## Multi-Scope Detection and Automatic Splitting

Agent 1 must detect when a user request contains multiple unrelated scopes.

When multiple unrelated topics, categories, modules, or root causes are detected, Agent 1 should automatically split them into separate copy-ready Agent-2 handoff blocks.

Agent 1 should not simply refuse. It should help the user by producing safe, usable blocks.

### Scope Types

Each handoff should be labeled with a scope type:

```text
Scope Type:
- SINGLE_ISSUE
- SAME_AREA_BUNDLE
- AUTO_SPLIT_MULTI_SCOPE
- USER_REQUESTED_COMBINED_SCOPE
```

| Scope Type | Meaning |
|---|---|
| `SINGLE_ISSUE` | One bug, one change, one narrow implementation target |
| `SAME_AREA_BUNDLE` | Multiple small changes that share the same page/category/component/root cause/context |
| `AUTO_SPLIT_MULTI_SCOPE` | Agent 1 detected unrelated work and split it into separate handoff blocks |
| `USER_REQUESTED_COMBINED_SCOPE` | The user explicitly requested one combined handoff despite unrelated scopes |

### Automatic Split Output

When splitting, Agent 1 should output separate blocks, for example:

```text
Detected scopes:
1. Settings / Input — collapse height bug
2. Settings / Provider — provider icon/link changes
3. Dashboard — unrelated layout issue

Recommended output:
- Agent-2 Handoff Block 1
- Agent-2 Handoff Block 2
- Agent-2 Handoff Block 3
```

Each block should be individually copy-ready.

Each block should contain its own:

- Agent-2 setup status
- task
- context
- scope boundaries
- instructions
- acceptance criteria
- output format

### User Choice for Combined Scope

At the end of an automatic split, Agent 1 may offer a combined version if the user still wants one.

The explanation should be factual, not frightening.

Suggested wording:

```text
I split these into separate handoff blocks because they affect different areas and likely require different context. This usually reduces context usage, token cost, wrong-file discovery, hallucination risk, and rework.

If you still want one combined handoff, I can generate it. A combined handoff may consume more context/tokens, affect usage limits, reduce output quality, and increase the chance that Agent 2 mixes unrelated changes.
```

Agent 1 should not shame, scare, or block the user. It should present the safer default and leave the user an informed choice.

### User-Requested Combined Scope

If the user explicitly requests one combined handoff despite the warning, Agent 1 may produce it.

The combined handoff must:

- label `Scope Type: USER_REQUESTED_COMBINED_SCOPE`
- list each sub-scope separately
- warn Agent 2 not to mix implementation logic between sub-scopes
- require Agent 2 to process sub-scopes independently
- require Agent 2 to stop if a sub-scope requires unrelated broad exploration
- require separate verification per sub-scope

A combined handoff must not hide the fact that it contains multiple scopes.

---

## Agent-2 Target Setup

Agent 2 has two separate target dimensions:

```text
1. AI model
2. Platform / execution environment
```

These are not the same.

The AI model controls how the handoff should be written.

The platform controls how the handoff will be executed.

### AI Model

The AI model affects:

- prompt shape
- reasoning style
- instruction density
- output structure
- verbosity
- formatting conventions
- tool-use assumptions
- uncertainty handling
- preferred evidence style
- anti-patterns
- model-specific strengths and weaknesses

Examples of model or model-family references may include:

- Claude
- GPT
- Codex-style models
- Gemini
- Perplexity
- DeepSeek
- local models
- other target models

Do not assume model-specific behavior without a provided model reference.

### Platform / Execution Environment

The platform or execution environment affects:

- where Agent 2 runs
- file access behavior
- whether the agent can inspect a repository
- whether commands can be executed
- whether patches can be applied directly
- whether browser/computer-use is available
- whether screenshots can be used
- whether output must be a diff, patch, checklist, prompt, or explanation
- IDE/app/CLI workflow rules
- how the user will apply the output

Examples:

- Claude Code
- Cursor
- Codex CLI
- Codex app
- ChatGPT with files/tools
- Gemini / Antigravity-style environment
- IDE assistant
- GitHub web workflow
- API-based coding workflow
- Raycast-style command launcher
- custom internal execution system

Do not assume platform behavior from model name.

`Claude` is not automatically `Claude Code`.

`GPT` is not automatically `Codex CLI`.

`Gemini` is not automatically a specific execution platform.

The target setup must name both dimensions where possible.

---

## Prompt Library, Model References, and Platform References

The Allzy Framework supports model- and platform-aware prompt rendering through reference files.

The current workflow is manual. A user may download or open a Prompt Library / Reference Package, select the relevant AI model and platform references, and provide their contents to Agent 1.

This is the manual operational precursor to the future Prism Registry.

### Reference Package

A Reference Package may contain:

- AI model prompting references
- platform / execution-environment references
- model-specific prompt shape guidance
- platform-specific file access rules
- platform-specific tool-use rules
- output format conventions
- handoff rendering examples
- model/platform compatibility notes
- known model anti-patterns
- known platform anti-patterns
- task-mode-specific rendering guidance
- fallback rendering guidance

A Reference Package can be used manually without Prism.

Prism may later automate reference resolution through a registry.

### Manual Reference Loading Workflow

Current workflow:

1. The user identifies the Agent-2 AI model.
2. The user identifies the Agent-2 platform / execution environment.
3. The user downloads or opens the relevant Prompt Library / Reference Package.
4. The user selects the matching model reference.
5. The user selects the matching platform reference.
6. The user attaches, pastes, or otherwise provides the reference contents to Agent 1.
7. Agent 1 checks which references are actually present.
8. Agent 1 labels the handoff as model-optimized, platform-optimized, both, or fallback.
9. Agent 1 renders the Agent-2 handoff accordingly.

A reference counts as available only if its content is present in the current Agent-1 context.

A link, repository name, file name, or statement that a reference exists is not enough.

### Future Prism Registry

In the future, Prism may resolve model and platform references automatically through a registry.

A future Prism Registry may select reference profiles based on:

- task type
- target AI model
- target platform
- output type
- execution mode
- prompt shape
- model family
- platform capability
- user-selected constraints

Until the registry exists and the relevant profiles are available, Agent 1 must treat references as unavailable unless their contents are actually present in the current context.

This mechanism is not limited to triage.

Triage uses it for Agent-2 handoffs, but the same model/platform reference principle can apply to any Allzy Framework prompt that must be adapted to a specific AI model, platform, execution environment, or output target.

Examples:

- Genesis prompt adapted to a specific assistant
- Yin/Yang review prompt adapted to Claude or GPT
- implementation handoff adapted to Claude Code or Cursor
- research prompt adapted to a search-grounded assistant
- prompt optimization workflow adapted to a target model
- system prompt generation adapted to a provider or platform

The future Prism Registry should automate the reference-selection step. It must not weaken the rule that optimization claims require actual reference content.

---

## Reference Document Rule

Agent 1 cannot reliably know every model and platform rule by default.

Therefore:

1. Model-optimized output requires a matching AI model reference.
2. Platform-optimized output requires a matching platform / execution-environment reference.
3. The reference content must be present in the current context.
4. Agent 1 must read and use the reference before claiming optimization.
5. A link or file name alone does not count.
6. A mismatched reference does not count.
7. Missing references require fallback or a stop, depending on user requirements.

### Reference Availability

| Case | Result |
|---|---|
| Model named, matching model reference provided | `Model-optimized: YES` |
| Platform named, matching platform reference provided | `Platform-optimized: YES` |
| Model named, no model reference provided | `Model-optimized: NO` |
| Platform named, no platform reference provided | `Platform-optimized: NO` |
| Reference named but content not present | Treat as missing |
| Reference content present but does not match target | Treat as mismatch |
| User accepts fallback | Use Universal Markdown fallback |
| User requires optimization and reference is missing | Stop and request the missing reference |

### Reference Mismatch Handling

If the selected Agent-2 model and provided model reference do not match, Agent 1 must not claim model optimization.

Example:

```text
Agent-2 model: Claude
Provided model reference: GPT/Codex reference
Status: Model-optimized: NO — reference mismatch
```

If the selected Agent-2 platform and provided platform reference do not match, Agent 1 must not claim platform optimization.

Example:

```text
Agent-2 platform: Cursor
Provided platform reference: Claude Code
Status: Platform-optimized: NO — reference mismatch
```

Agent 1 may still produce fallback output if the user allows it.

### Reference Provenance

Where possible, the handoff should record which references were used.

Example:

```text
AI model reference: claude_prompting_reference.md — provided and used
Platform reference: claude_code_reference.md — provided and used
Reference version/date: 2026-06-06
```

This makes future debugging possible. If a handoff performs poorly, the user can see whether it was rendered from stale, mismatched, or missing reference material.

---

## Handoff Rendering Modes

Agent 1 should label the rendering mode.

### Universal Markdown Fallback

Use when:

- no model reference is available
- no platform reference is available
- the user allows fallback
- the handoff must remain generic and portable

Rules:

- clearly label fallback
- do not claim model optimization
- do not claim platform optimization
- avoid platform-specific assumptions
- use clear Markdown
- keep instructions explicit and portable

### Model-Optimized

Use when:

- Agent-2 AI model is known
- matching model reference is provided
- Agent 1 has read and used it
- platform reference may still be missing

Rules:

- label `Model-optimized: YES`
- label platform status separately
- do not invent platform assumptions

### Platform-Optimized

Use when:

- Agent-2 platform is known
- matching platform reference is provided
- Agent 1 has read and used it
- model reference may still be missing

Rules:

- label `Platform-optimized: YES`
- label model status separately
- do not invent model-specific prompting rules

### Model + Platform Optimized

Use when:

- matching model reference is provided
- matching platform reference is provided
- both are read and used

Rules:

- label both as optimized
- adapt handoff shape to model
- adapt execution instructions to platform
- preserve Allzy safety rules
- do not let model/platform references override scope boundaries

---

## Agent-2 Handoff Status Block

Every Agent-2 handoff should begin with a status block.

```text
Agent-2 Setup Status

Agent-2 AI model: [provided / missing / value]
Agent-2 platform: [provided / missing / value]
AI model reference: [provided and used / missing / mismatch]
Platform reference: [provided and used / missing / mismatch]
Model-optimized: [YES / NO]
Platform-optimized: [YES / NO]
Fallback: [Universal Markdown / NO]
Mode: [Fast / Standard / Deep]
Scope Type: [SINGLE_ISSUE / SAME_AREA_BUNDLE / AUTO_SPLIT_MULTI_SCOPE / USER_REQUESTED_COMBINED_SCOPE]
Metadata context: [provided / missing / not applicable]
Context package: [provided / not provided / not needed]
Search Log: [included / not used / unavailable]
Retrieval initialized: [YES / NO / UNKNOWN / not needed]
Blockers: [none / list blockers]
```

The status block prevents false precision.

A user should be able to see immediately whether the handoff is:

- target-specific
- partially optimized
- fallback
- blocked
- one issue
- same-area bundle
- auto-split
- user-forced combined scope

---

## Triage Modes

Triage uses three operational modes:

```text
Fast
Standard
Deep
```

The mode controls diagnostic depth and output length.

It does not change the core safety model.

All modes preserve:

- Agent-1 / Agent-2 separation
- Agent 1 no-code rule
- privacy/security check
- scope classification
- honest model/platform reference handling
- fallback labeling
- no unrelated scope bundling
- no false optimization claims
- contract/state gap handling where relevant

### Fast Mode

Fast Mode is implemented by:

```text
prompts/Triage/fast/000_universal.md
```

Use Fast Mode for small, low-risk, visually obvious, or narrowly scoped issues.

The user may request it with:

```text
FAST TRIAGE
```

Fast Mode may shorten output.

Fast Mode must not remove:

- Agent-2 setup status
- AI model / platform handling
- model/profile availability status
- scope boundaries
- acceptance criteria
- warnings or blockers
- security/privacy check
- no-code rule for Agent 1
- no invented file paths
- no unrelated-issue bundling
- no false optimization claims
- no fallback label

Fast Mode is not a weaker workflow. It is a shorter output mode for safe low-risk cases.

### Standard Mode

Standard Mode is implemented by:

```text
prompts/Triage/standard/000_universal.md
```

Standard Mode is the default.

Use Standard Mode for most normal maintenance work:

- normal bugs
- normal UI fixes
- normal interaction issues
- bounded state issues
- implementation flaws against existing contracts
- moderate data-flow issues
- normal Agent-2 handoffs
- cases where metadata retrieval is useful but not unusually complex

When no mode is specified, use Standard Mode unless the issue is clearly safe for Fast or clearly requires Deep.

### Deep Mode

Deep Mode is implemented by:

```text
prompts/Triage/deep/000_universal.md
```

Use Deep Mode for:

- unclear bugs
- risky changes
- multi-layer issues
- contract-heavy issues
- state-heavy issues
- persistence-related issues
- permission/security/privacy-sensitive issues
- architecture-sensitive issues
- issues with unclear root cause
- issues requiring deeper metadata retrieval
- issues requiring Yin/Yang comparison
- issues requiring memory/history review
- issues likely to produce rework if diagnosed shallowly

Deep Mode should include stronger:

- evidence separation
- confirmed facts vs assumptions
- uncertainty handling
- metadata/retrieval analysis
- Search Log
- contract/state implications
- scope splitting
- risk notes
- blocker handling
- acceptance criteria

Deep Mode is still Triage.

Agent 1 still does not write code, produce patches, or modify files.

---

## Triage Inputs

A useful triage input may include:

- current page or product area
- category or component name
- screenshot(s)
- screen recording
- observed behavior
- expected behavior
- trigger action
- before/after state
- console error
- stack trace
- network error
- log excerpt
- suspected files or modules
- target Agent-2 model
- target Agent-2 platform
- model/platform reference files
- relevant contract file
- relevant state excerpt

The user does not need to provide all of this.

Agent 1 should work with available evidence and mark uncertainty clearly.

---

## Security and Privacy Check

Before producing a handoff, Agent 1 must check whether the input contains secrets or sensitive data.

Examples:

- API keys
- passwords
- private tokens
- bearer tokens
- refresh tokens
- session cookies
- database URLs
- private credentials
- private keys
- production secrets
- private infrastructure values
- sensitive personal data
- confidential operational details

If real secrets are present:

1. Stop.
2. Do not repeat the secret.
3. Warn the user that a secret or sensitive value appears to be present.
4. Ask the user to remove or replace it with a placeholder.
5. Do not include the secret in any handoff.

Use placeholders such as:

```text
$ENV_API_KEY
$ENV_DATABASE_URL
$ENV_SESSION_SECRET
process.env.SERVICE_TOKEN
```

Screenshots and logs often contain sensitive values. Agent 1 must be careful not to copy them into Agent-2 handoffs.

---

## Relationship to Deterministic Metadata Retrieval

Triage should use deterministic metadata retrieval before broad file discovery when a project provides metadata, a metadata index, or a `context_retrieval.md` artifact.

The default order is:

```text
metadata first
narrow document context second
narrow file discovery third
broad repository search only as a last resort
```

Agent 1 should not ask Agent 2 to rediscover the whole project when the documentation graph can already identify the relevant area.

When available, Agent 1 should use:

- `context_retrieval.md`
- metadata/frontmatter
- `metadata_index.json`
- `metadata_index.md`
- `context_index.md`
- module IDs
- submodule IDs
- document types
- layers
- tags
- parent/child links
- paired Yin/Yang links
- related memory sections
- prior handoffs
- Search Logs from previous context packages

The purpose is not to make Triage heavier. The purpose is to reduce uncertainty before implementation.

A good triage handoff should say:

```text
These documents were selected because their metadata matches the issue.
These files or folders should be inspected because they are inside the matched scope.
These unrelated areas were excluded.
```

This makes the handoff auditable and prevents Agent 2 from spending context on broad exploration.

### Metadata Retrieval Is Not File Discovery

Metadata retrieval and file discovery are related, but not identical.

| Step | Purpose |
|---|---|
| Metadata retrieval | Find relevant documentation, contracts, memory sections, and graph nodes |
| File discovery | Find implementation files inside the scoped codebase area |
| Implementation | Modify only the files needed for the scoped task |

Agent 1 may not know exact implementation files. That is acceptable.

Agent 1 should still provide narrow metadata-derived boundaries:

```text
module_id: settings
submodule_id: settings.input
tags: settings, input, collapse, ui-state
related_yin: core.settings.input.yin
related_yang: core.settings.input.yang
memory_section: Settings / Input
```

Agent 2 can then perform narrow file discovery inside that area instead of searching the entire repository.

### Search Log Requirement

When Agent 1 uses deterministic retrieval, the handoff or accompanying context package should include a short Search Log.

A Search Log records:

- user issue or query
- metadata filters used
- files or documents matched
- links followed
- relevant memory sections
- excluded areas
- unresolved retrieval uncertainty

Example:

```text
Search Log:
- Query: Settings/Input collapse height bug
- Filters: module_id=settings, submodule_id=settings.input, tags=collapse/ui-state
- Documents matched: core.settings.input.yin, core.settings.input.yang
- Memory matched: memory.md → Settings / Input
- Links followed: paired_yang, parent module
- Excluded: Settings/Provider, Dashboard, archived drafts
```

A Search Log prevents invisible context selection and helps the next agent understand why the handoff contains the chosen context.


## Triage Protocol

Agent 1 follows this protocol.

### Step 1 — Validate Agent-2 Setup

Determine whether the user has provided:

- Agent-2 AI model
- Agent-2 platform / execution environment
- whether optimized output is required
- whether fallback is acceptable
- model reference availability
- platform reference availability

If setup is missing and needed, ask for it.

If the user allows Universal Markdown fallback, proceed with fallback.

If the user requires optimization and references are missing, stop and request the missing references.

### Step 2 — Understand the Issue

Separate:

- confirmed facts
- observed symptoms
- expected behavior
- assumptions
- unknowns
- out-of-scope observations

Do not treat assumptions as facts.

### Step 3 — Perform Security / Privacy Check

Sanitize or stop if secrets are present.


### Step 3A — Use Deterministic Metadata Retrieval When Available

If the project provides metadata, a metadata index, or `context_retrieval.md`, use deterministic retrieval before broad file discovery.

Search for:

- exact `id`
- `module_id`
- `submodule_id`
- `document_type`
- `layer`
- high-signal tags
- paired Yin/Yang links
- related memory sections
- relevant handoff history

Then follow only necessary explicit links.

Do not include every related document by default. Include only what helps Agent 2 execute the scoped task.

If deterministic retrieval was used, record a short Search Log.

### Step 4 — Classify Work Type

Assign a work type.

Possible values:

```text
VISUAL_UI_FIX
INTERACTION_FIX
STATE_FIX
DATA_FLOW_FIX
CONTRACT_FLAW
IMPLEMENTATION_FLAW
COPY_OR_LABEL_FIX
UNKNOWN
```

### Step 5 — Detect Scope Shape

Determine:

- single issue
- same-area bundle
- multi-scope request
- user-requested combined scope

If multiple unrelated scopes exist, split automatically.

### Step 6 — Detect Contract / State Implications

Determine whether the issue may require:

- Yin update
- Yang update
- State Management update
- `memory.md` update after confirmation
- no documentation update

Do not hide contract gaps in implementation instructions.

### Step 7 — Define Metadata and File Discovery Boundaries

If metadata context exists, define it first:

- layer
- module ID
- submodule ID
- document type
- tags
- related Yin
- related Yang
- related memory section
- related prior handoff
- search log or context package

If likely implementation files are known, name them.

If exact implementation files are unknown, define narrow discovery boundaries:

- page
- category
- component
- route
- module
- state store
- feature folder
- related contract
- likely search terms

Do not tell Agent 2 to search the entire repository unless unavoidable.

Broad file discovery is a blocker unless the user explicitly accepts the cost/risk or the platform workflow requires it.

### Step 8 — Produce Agent-2 Handoff Block(s)

Each block should be copy-ready.

### Step 9 — Produce Optional JSON Metadata

Only if useful.

JSON metadata may help:

- future Prism adapters
- registries
- renderers
- automation tools
- issue trackers
- internal indexing

JSON is optional. The handoff remains primary.

### Step 10 — Explain Split / Fallback / Blockers

If split occurred, explain why.

If fallback was used, label it.

If blockers exist, list them.

---

## Work Type Classification

### `VISUAL_UI_FIX`

Use for visual problems that do not primarily involve state or data flow.

Examples:

- spacing
- alignment
- inconsistent height
- wrong color token
- layout overflow
- clipped content
- visual regression

May be direct prompt, Fast Mode, or small handoff if scope is narrow.

### `INTERACTION_FIX`

Use when the problem appears during user interaction.

Examples:

- button click does nothing
- toggle changes wrong UI state
- dropdown does not close
- accordion/collapse behavior is wrong
- modal opens incorrectly
- focus handling fails

May require state inspection.

### `STATE_FIX`

Use when the problem likely involves state synchronization, stale state, persistence mismatch, state propagation, store updates, or UI state boundary.

Examples:

- toggle changes layout state unexpectedly
- UI resets after navigation
- settings do not persist
- collapsed/expanded state updates wrong container
- visible UI does not match stored state
- derived state recalculates incorrectly

State fixes often need careful boundaries and may connect to `06_State_Management.md` concepts.

### `DATA_FLOW_FIX`

Use when data moves incorrectly between layers.

Examples:

- API response is mapped incorrectly
- form values are transformed wrongly
- frontend and backend data shape mismatch
- data appears in one component but not another
- event payload has wrong field

May require contract review.

### `CONTRACT_FLAW`

Use when the issue reveals a missing, wrong, or outdated contract.

Examples:

- Yang does not define behavior for this edge case
- Yin says one thing, Yang says another
- implementation behavior is undocumented
- API behavior changed but contract did not
- state transition missing from Yang
- action behavior is undefined

Agent 1 must not convert this into a pure code fix. The contract must be updated or flagged first.

### `IMPLEMENTATION_FLAW`

Use when the contract is correct but implementation violates it.

Examples:

- code does not follow Yang decision matrix
- action is missing
- test expectation defined in contract fails
- shell performs a decision that belongs in core
- UI violates documented Yin behavior

Agent 2 can fix against the contract.

### `COPY_OR_LABEL_FIX`

Use for low-risk copy changes.

Examples:

- wrong label
- typo
- static text mismatch
- untranslated string
- button wording adjustment

Can often be direct prompt or Fast Mode.

### `UNKNOWN`

Use when evidence is insufficient.

Agent 1 may still produce a diagnostic handoff if uncertainty is labeled, or ask for one targeted clarification if needed.

---

## File Discovery Boundaries

A good Agent-2 handoff reduces broad repository exploration.

Agent 1 should specify one of:


### Metadata Before File Discovery

When metadata exists, Agent 1 should identify metadata context before asking Agent 2 to inspect code.

Example:

```text
Metadata / Retrieval Context:
- layer: Core
- module_id: settings
- submodule_id: settings.input
- related_yin: core.settings.input.yin
- related_yang: core.settings.input.yang
- memory_section: Settings / Input
- tags: settings, input, collapse, ui-state
```

Then file discovery can be narrow:

```text
Search only inside Settings/Input implementation areas.
Do not inspect Settings/Provider, Dashboard, or global layout unless directly required.
```

Metadata does not replace code inspection. It prevents unbounded code inspection.


### Exact File Scope

Use when likely files are known.

```text
Inspect only:
- src/settings/input/InputBlocks.tsx
- src/settings/input/inputSettingsStore.ts
```

### Narrow Discovery Scope

Use when exact files are unknown but the area is clear.

```text
Search only within:
- Settings feature folder
- Input category components
- collapsible block layout/state handling

Suggested search terms:
- defaultCollapsed
- InputBlock
- collapse
- settings input
- minHeight
```

### Contract Scope

Use when a contract likely exists.

```text
Check relevant contract:
- docs/03_Yin_Yang_Contracts.md
- auth.user-login Yang
- Settings/Input Yin or Yang if present
```

### Forbidden Broad Scope

Avoid:

```text
Search the whole repository and fix anything related.
```

Broad exploration should be a blocker unless the user explicitly accepts it or the platform workflow requires it.

---

## Agent-2 Handoff Structure

A standard Agent-2 handoff should include:

```text
# Agent-2 Handoff — [Short Title]

## Agent-2 Setup Status
...

## Task
...

## Context
...

## Observed Behavior
...

## Expected Behavior
...

## Work Type
...

## Scope Type
...

## Likely Affected Area
...

## Metadata / Retrieval Context
...

## File Discovery Boundaries
...

## Search Log
...

## Instructions
...

## Scope Boundaries
...

## Forbidden Actions
...

## Acceptance Criteria
...

## Output Format
...

## Blockers / Uncertainty
...
```

### Task

One sentence describing the implementation goal.

### Context

Only the relevant context required for execution.

### Observed Behavior

What currently happens.

### Expected Behavior

What must happen after the fix.

### Work Type

One of the defined classification values.

### Scope Type

One of the defined scope types.

### Likely Affected Area

Page, feature, module, category, component, route, or state boundary.

### Metadata / Retrieval Context

Relevant graph metadata and documentation context, if available.

Examples:

- layer
- module ID
- submodule ID
- document type
- related Yin
- related Yang
- related schema
- related memory section
- source block ID
- tags
- status
- context package
- previous handoff ID

This section may be omitted only when no metadata graph or retrieval artifact exists.

### Search Log

A short record of how context was selected.

Include when deterministic retrieval was used.

If no deterministic retrieval was used, state:

```text
Search Log: not used / unavailable
```

### File Discovery Boundaries

Exact files or narrow discovery scope.

### Instructions

Implementation instructions for Agent 2.

### Scope Boundaries

What is allowed and forbidden.

### Forbidden Actions

Examples:

- do not refactor unrelated code
- do not redesign the page
- do not modify Provider settings
- do not change global layout
- do not add new dependencies
- do not change public APIs
- do not modify persistence
- do not update contracts unless instructed

### Acceptance Criteria

Concrete testable conditions.

### Output Format

What Agent 2 should return:

- summary
- files changed
- diff/patch if applicable
- tests run
- verification notes
- unresolved blockers

---

## Optional JSON Metadata

JSON metadata is optional.

It can support:

- future Prism adapters
- handoff indexing
- issue trackers
- automation
- tool processing
- model/platform renderers
- later registry workflows

It should not replace the human-readable handoff.

Example:

```json
{
  "workType": "STATE_FIX",
  "scopeType": "SINGLE_ISSUE",
  "area": "Settings/Input",
  "modelOptimized": false,
  "platformOptimized": false,
  "fallback": "Universal Markdown",
  "metadataContext": {
    "layer": "Core",
    "module_id": "settings",
    "submodule_id": "settings.input",
    "related_yin": "core.settings.input.yin",
    "related_yang": "core.settings.input.yang",
    "memory_section": "Settings / Input",
    "tags": ["settings", "input", "collapse", "ui-state"]
  },
  "searchLog": {
    "used": true,
    "filters": ["module_id=settings", "submodule_id=settings.input", "tags=collapse/ui-state"],
    "documentsMatched": ["core.settings.input.yin", "core.settings.input.yang"],
    "excluded": ["Settings/Provider", "Dashboard", "archived drafts"]
  },
  "likelyAffectedArea": [
    "Settings Input category",
    "collapsible input blocks",
    "default collapsed state"
  ],
  "forbiddenAreas": [
    "Settings Provider category",
    "Dashboard",
    "global layout"
  ]
}
```

JSON must not contain secrets.

---

## Relationship to the Deterministic Metadata Graph

Triage is one of the main consumers of the Deterministic Metadata Graph.

The Metadata Graph helps Agent 1 answer:

- which module is affected?
- which submodule is affected?
- which Yin document explains intent?
- which Yang document defines execution truth?
- which schemas are related?
- which memory section is relevant?
- which previous handoff may matter?
- which documents are archived or deprecated?
- which documents should be excluded?

The graph should not make Agent 1 blindly include every related document.

It should help Agent 1 select the smallest sufficient context.

Recommended triage retrieval order:

```text
1. Use exact IDs if provided.
2. Use module_id / submodule_id if known.
3. Use layer and document_type filters.
4. Use high-signal tags.
5. Follow paired Yin/Yang links.
6. Follow parent/child links only as needed.
7. Include relevant memory excerpts.
8. Exclude archived, deprecated, unrelated, or stale documents.
9. Generate a Search Log.
10. Produce the Agent-2 handoff.
```

If `context_retrieval.md` exists, Agent 1 should follow it before inventing its own search process.

If no metadata graph exists, Agent 1 may proceed with normal triage, but the handoff should not imply deterministic retrieval was performed.


## Relationship to Yin/Yang Contracts

Triage must respect Yin/Yang.

When a maintenance issue appears, Agent 1 should ask:

```text
Is this a code bug against a correct contract,
or is the contract itself incomplete?
```

### If Yin Is Missing or Wrong

If the bug reveals missing product/domain intent, update Yin first.

Examples:

- expected behavior was never documented
- user workflow meaning is unclear
- UI state expectation is missing
- out-of-scope boundary is missing
- domain rule was assumed but not written

### If Yang Is Missing or Wrong

If the bug reveals missing technical execution behavior, update Yang before implementation.

Examples:

- state transition undefined
- duplicate behavior undefined
- action missing
- shell/core boundary unclear
- decision matrix lacks branch
- error case not covered
- idempotency missing

### If Implementation Is Wrong

If Yin/Yang are correct and implementation violates them, Agent 2 may fix the code against the contracts.

### If Yin and Yang Conflict

Stop and reconcile the documents.

Do not choose one silently.

### Contract Gap Rule

If Agent 1 suspects a contract gap, it should classify the work as `CONTRACT_FLAW` or mark a possible contract flaw in the handoff.

Agent 2 must not silently turn contract gaps into code decisions.

---

## Relationship to State Management

State Management is handled in detail in `06_State_Management.md`.

This document only defines how Triage uses state artifacts.

Use:

```text
plan.md   = current task focus
memory.md = confirmed current project / architecture memory
handoff   = scoped execution context for Agent 2
```

Agent 1 and Agent 2 should receive only relevant excerpts from `plan.md` or `memory.md`.

Do not dump entire state files by default.

### Relevant State Excerpts

Include state excerpts when they help Agent 2 avoid rework or wrong assumptions.

Examples:

- current implementation status
- known architecture decision
- recently confirmed component behavior
- active contract boundary
- known dependency
- current task scope
- previous confirmed fix that affects this issue

### State Noise to Avoid

Do not include:

- failed attempts
- old chat history
- obsolete decisions
- unrelated feature plans
- unrelated memory sections
- large unfiltered logs
- uncertain guesses as confirmed facts

### After Implementation

After Agent 2 finishes:

- verify against acceptance criteria
- record confirmed current state in `memory.md` if relevant
- do not record failed attempts
- update Yin/Yang if documented behavior changed
- reset or update `plan.md` for the next task

---

## Verification and Documentation Follow-Up

Triage does not end when the handoff is produced.

After Agent 2 executes:

1. Review changed files.
2. Verify acceptance criteria.
3. Check that no out-of-scope files were modified.
4. Check that no unrelated issue was silently addressed.
5. Confirm whether the root cause was fixed.
6. Confirm whether contracts need updates.
7. Update `memory.md` only after the fix is verified and intentionally kept.
8. Open a new triage cycle for any unrelated issue discovered.

If the fix changes intended behavior, update documentation.

If the fix only corrects implementation against existing documentation, a documentation update may not be needed, but confirmed state may still be recorded in `memory.md` if future sessions need it.

---

## Practical Workflow Example

### Situation

The user is working in a local UI builder or app. A bug appears in Settings.

The user captures two screenshots and dictates:

```text
I am in Settings → Input.
The input collapse blocks have a default collapsed option.
When I toggle this option, the panel height changes.
It should stay fixed.
Screenshot 1 shows the correct height.
Screenshot 2 shows the wrong height.
Do not change Provider settings.
```

### Agent 1 Diagnosis

Agent 1 identifies:

```text
Work Type: STATE_FIX or INTERACTION_FIX
Scope Type: SINGLE_ISSUE
Area: Settings/Input
Likely affected boundary: collapsible input block state/layout
Expected behavior: fixed panel height
Forbidden area: Settings/Provider, global layout
```

### Agent 1 Handoff

Agent 1 produces a copy-ready handoff for Agent 2:

```text
Task:
Fix the Settings/Input collapsible block container height so toggling default collapsed state does not resize the panel.

Context:
The issue appears in Settings → Input. The default collapsed toggle changes the visible panel height. The panel should keep a stable height regardless of collapse default state.

File Discovery Boundaries:
Search only in Settings/Input components and collapse state/layout handling.
Suggested terms: defaultCollapsed, collapse, InputBlock, minHeight, container height.

Do not touch:
- Settings/Provider
- Dashboard
- global Settings layout
- provider creation flow

Acceptance Criteria:
- toggling default collapsed state does not change panel height
- existing collapse behavior still works
- no unrelated Settings categories are modified
```

### Agent 2 Execution

Agent 2 inspects the bounded area, fixes the layout/state handling, and reports changed files.

### Verification

The user verifies the toggle behavior. If confirmed, the result may be recorded in `memory.md` if relevant.

---

## Anti-Patterns


Additional Triage/context anti-patterns:

- using Workspace State Maintenance as if it were Triage
- asking Triage to clean `memory.md` or `plan.md` instead of producing a handoff
- treating a context package as permanent memory
- omitting Search Log status when retrieval was used
- pretending deterministic retrieval exists when `context_retrieval.md` or metadata conventions are missing
- asking Agent 2 to rediscover context that Agent 1 or Context Retrieval Builder already selected


### Raw Screenshot to Implementation Agent

Sending screenshots directly to Agent 2 and asking it to fix the issue without triage.

Why it fails:

- high visual context cost
- broad exploration
- ambiguous scope
- wrong-file risk
- repeated visual reasoning inside implementation context

### "Fix Everything Here"

A vague request that points to a page or screenshot and asks for all issues to be fixed.

Why it fails:

- multiple scopes
- no priority
- no acceptance criteria
- high hallucination risk
- easy scope drift

### Multi-Area Bundle

Combining unrelated changes in one handoff.

Why it fails:

- model reasons across unrelated work simultaneously
- file discovery expands
- output quality drops
- tests become unclear
- rework increases

### False Optimization Claim

Claiming a handoff is optimized for a model or platform without a matching reference.

Why it fails:

- fake precision
- wrong prompt shape
- wrong tool assumptions
- unreliable execution behavior

### Contract-Blind Patch

Fixing code without checking whether the contract is wrong.

Why it fails:

- documentation drift
- repeated bug patterns
- hidden behavior changes
- later AI sessions use stale source material

### State Dumping

Pasting full `memory.md`, full `plan.md`, old chats, and unrelated context into Agent 2.

Why it fails:

- context noise
- stale assumptions
- attention dilution
- more tokens
- lower output quality

### Silent Scope Expansion

Agent 2 fixes extra issues that were noticed while working.

Why it fails:

- unreviewed behavior changes
- unverifiable output
- hidden regressions
- harder rollback

---

## Quality Checklist

Before producing a triage handoff, Agent 1 should verify:

- [ ] Agent-2 AI model is known or fallback is accepted.
- [ ] Agent-2 platform / execution environment is known or fallback is accepted.
- [ ] Model reference availability is correctly labeled.
- [ ] Platform reference availability is correctly labeled.
- [ ] No false optimization claim is made.
- [ ] Reference mismatch is detected if present.
- [ ] Reference provenance is recorded where possible.
- [ ] Security/privacy check is complete.
- [ ] Secrets are not repeated.
- [ ] Observed behavior is clear.
- [ ] Expected behavior is clear.
- [ ] Deterministic metadata retrieval was used when available.
- [ ] `context_retrieval.md` was checked when present.
- [ ] Metadata / Retrieval Context is included when relevant.
- [ ] Search Log is included when deterministic retrieval was used.
- [ ] Archived/deprecated documents were excluded unless explicitly needed.
- [ ] Work type is classified.
- [ ] Scope type is classified.
- [ ] Multi-scope input is split automatically.
- [ ] Same-area bundle is justified if used.
- [ ] File discovery boundaries are narrow.
- [ ] Scope boundaries are explicit.
- [ ] Forbidden actions are explicit.
- [ ] Acceptance criteria are testable.
- [ ] Contract/state implications are noted.
- [ ] The handoff is copy-ready for Agent 2.
- [ ] Optional JSON metadata contains no secrets.
- [ ] User is offered a combined handoff only as an informed choice when scopes were split.

Before Agent 2 executes, verify:

- [ ] The handoff is the only task source.
- [ ] Agent 2 understands the scope boundary.
- [ ] Agent 2 knows where to inspect.
- [ ] Agent 2 knows what not to touch.
- [ ] Agent 2 has the right output format.
- [ ] Agent 2 knows to stop on contract gaps.

After Agent 2 executes, verify:

- [ ] Acceptance criteria pass.
- [ ] Out-of-scope files were not modified.
- [ ] No unrelated refactor was added.
- [ ] No hidden contract decision was made.
- [ ] Documentation update needs are identified.
- [ ] Confirmed state is recorded only if needed.

---

## Website-Ready Summary


Triage may use selected context from the Context Retrieval Builder, but it remains a diagnosis and handoff workflow. Workspace State Maintenance is separate and should be used for cleanup/compression of living state files after work is confirmed.


Triage and Maintenance are the Allzy Framework's method for turning messy bugs into safe implementation work.

Agent 1 receives screenshots, errors, rough descriptions, and visual context. It diagnoses the issue, splits unrelated scopes, compresses the context, and produces one or more copy-ready Agent-2 handoff blocks.

Agent 2 receives the handoff and executes the fix surgically.

The workflow keeps implementation tasks small, avoids broad repository exploration, reduces visual and computer-use context costs, prevents unrelated changes from being bundled, and makes model/platform-specific prompting possible through reference files.

When a Deterministic Metadata Graph, metadata index, or `context_retrieval.md` exists, Triage should use it before broad file discovery. Agent 1 should retrieve the relevant Yin/Yang documents, memory sections, module IDs, submodule IDs, tags, and Search Log context before producing the Agent-2 handoff.

Basic triage works with Universal Markdown fallback. Accurate model-optimized or platform-optimized handoffs require the matching reference files to be present in the current context. Today this is handled manually through a Prompt Library / Reference Package. Later, Prism may automate this through a registry.

The goal is not to slow down maintenance. The goal is to prevent the expensive pattern where an AI agent tries to diagnose, browse, interpret, patch, and refactor everything at once.
