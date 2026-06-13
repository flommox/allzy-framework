---
id: "allzy.framework.docs.06.state-management"
title: "06 — State Management"
artifact_type: "Framework Documentation"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - state-management
---

# 06 — State Management

## Summary

State Management in the Allzy Framework means preserving the right project state for AI-assisted work without polluting the next task.

AI development sessions are stateless by default. Each new chat, coding agent, IDE assistant, CLI agent, or model session starts with limited or no reliable memory of previous decisions, confirmed implementation state, failed fixes, active contracts, or current task boundaries.

Without deliberate state management, the same problems repeat:

- the user re-explains the same context
- the AI repeats ineffective fixes
- confirmed architecture decisions are forgotten
- old assumptions return as if they were still true
- implementation agents inspect too broadly
- token usage grows
- context quality degrades
- bugs become harder to resolve

The Allzy Framework solves this with minimal external state artifacts:

```text
plan.md              = current task focus
memory.md            = confirmed project and architecture memory
context_retrieval.md = reusable deterministic retrieval method
context_package.md   = temporary task-specific context package
Search Log           = audit trail for context selection
metadata_index       = optional generated lookup index
skills/              = optional reusable agent helper rules
handoff              = scoped execution context for one agent or task
```

These files are not app runtime state. They are project/session state for AI-assisted work.

The goal is not to record everything. The goal is to preserve exactly the information future agents need while removing noise before it becomes a cost and quality problem.

---

## Source Authority

This document is based on the current Allzy Framework workflow, finalized prompts, finalized templates, finalized examples, and practical usage decisions.

Older documentation and previous master specifications are useful input, but they are not automatically correct. When old wording conflicts with the current Triage workflow, Yin/Yang contract rules, prompt template structure, or practical state workflow, the current workflow wins.

This document is explanatory framework documentation. It is not a source-code implementation guide for application runtime state.

---

## What State Management Means in the Allzy Framework

State Management in this document means:

```text
Project State / AI Session State
```

It answers:

- What is the current AI task?
- What has already been confirmed?
- Which module or category is being worked on?
- What changed recently?
- Which contracts or files are affected?
- Which attempted fix did not work and should not be repeated?
- Which state is still relevant for the next AI agent?
- Which old information should be compressed or removed?
- How can work continue across models and platforms without losing context?

It does not mean React state, database state, cache state, queue state, or application state architecture.

Those belong to Architecture documents, Yin/Yang contracts, implementation files, and runtime system design.

---

## Project / AI Session State vs. Application Runtime State

The word `state` can mean two different things. The framework separates them.

### Project / AI Session State

Project / AI Session State is external context used to guide AI-assisted work.

Examples:

- current task scope
- current plan
- active category or module
- confirmed architecture decisions
- confirmed implementation status
- relevant files changed
- known contracts
- prior fix attempts that were ineffective
- current blockers
- relevant handoff context
- compression status
- task history that still matters

This state lives in:

- `plan.md`
- `memory.md`
- Agent-2 handoffs
- temporary context packages
- relevant excerpts from contracts or documentation

### Application Runtime State

Application Runtime State is the state inside the software being built.

Examples:

- logged-in user state
- UI state
- database records
- caches
- queues
- jobs
- session state
- workflow state
- persisted settings
- client-side stores
- backend state machines
- event streams

Application Runtime State is specified through Architecture documents and Yang Core Modules.

In the Yang model, runtime facts are injected into the Functional Core through `StateSnapshot`. The Functional Core does not fetch or mutate runtime state directly. The Imperative Shell reads, writes, persists, and executes side effects.

This document may reference Application Runtime State when explaining bugs or maintenance, but it does not define runtime state architecture.

---

## Core Principle

Use different artifacts for different jobs.

```text
plan.md              = current task focus
memory.md            = confirmed current project / architecture memory
context_retrieval.md = reusable deterministic retrieval method
context_package.md   = temporary task-specific context package
Search Log           = retrieval audit trail
metadata_index       = optional generated lookup index
skills/              = optional reusable helper rules for AI agents
handoff              = scoped execution context for a specific agent/task
```

Do not merge all three into one file.

A single overloaded file becomes noisy, repetitive, expensive, and unreliable. It eventually recreates the same problem as a long, stale chat: too much history, too little signal.

---

## State Artifacts


### Workspace Context Initialization

Workspace Context Initialization is the setup, inspection, or repair step for the workspace context layer.

Operational prompt:

```text
workspace_context_initialization_prompt.md
```

Its job is to prepare the target implementation workspace so future AI agents can work from defined context instead of guessing.

It may create or check:

```text
plan.md
memory.md
context_retrieval.md
context_package_template.md
search_log_template.md
metadata_index.md / metadata_index.json
skills/
```

It does not:

- write application code
- implement features
- fix bugs
- perform Triage
- create Yin Pages
- create Yang Core Modules
- create Yin/Yang documents
- rewrite architecture
- refactor a repository
- replace application runtime state architecture

Workspace Context Initialization belongs to the **target implementation workspace**.

It is not the same thing as the Framework GitHub repository prompt organization.

### Workspace Context Initialization Modes

The initialization prompt supports three usage paths:

| Mode | Meaning |
|---|---|
| Website / Preconfigured Mode | A website or prompt builder fills the config block before execution |
| Manual Config Mode | The user manually edits the config block before running the prompt |
| Assistant Mode | The config is empty or incomplete, so the assistant asks targeted setup questions |

The config block is fundamental.

If the config is filled, the assistant should execute according to the config and avoid redundant setup questions.

If the config is empty or incomplete, the assistant should ask one targeted setup question at a time.

### Workspace Setup Profiles

Recommended setup profiles:

| Profile | Creates/checks |
|---|---|
| `inspect_only` | Inspect existing context setup only; do not create files |
| `minimal` | `plan.md` + `memory.md` |
| `standard` | `plan.md` + `memory.md` + `context_retrieval.md` |
| `full` | Standard setup + context package template + Search Log template + optional metadata index + optional skills |
| `custom` | Explicit config choices |

Use `standard` as the normal baseline for AI-assisted implementation work.

Use `full` for larger projects, Framework-based workspaces, Yin/Yang workflows, Triage-heavy projects, or multi-agent workflows.

Use `inspect_only` when the user wants a report but no file creation or modification.

### Workspace State Maintenance

Workspace State Maintenance is the cleanup, compression, update, or review step for living workspace state.

Operational prompt:

```text
workspace_state_maintenance_prompt.md
```

It maintains only active workspace context files such as:

```text
plan.md
memory.md
skills/
skills_index.md
skills_bundle.md
```

It may optionally health-check these when explicitly provided or requested:

```text
context_retrieval.md
metadata_index.md
metadata_index.json
context packages
search logs
```

Optional targets are not rewritten by default.

Workspace State Maintenance does not:

- initialize a workspace
- write application code
- fix bugs
- perform Triage
- rewrite framework templates
- rewrite Genesis prompts
- rewrite Triage prompts
- rewrite Yin/Yang templates
- maintain application source code

### Initialization vs. Maintenance

Initialization and maintenance are different operations.

| Operation | Purpose | Main prompt |
|---|---|---|
| Initialization | Create, inspect, or repair the workspace context layer | `workspace_context_initialization_prompt.md` |
| Maintenance | Clean, compress, and update living workspace state | `workspace_state_maintenance_prompt.md` |

Initialization may create missing structures.

Maintenance keeps existing active state useful, current, compressed, and safe.

Do not use the maintenance prompt as a substitute for initialization.

Do not use the initialization prompt as a recurring cleanup tool.


### `plan.md`

`plan.md` is the active task plan.

It answers:

```text
What is being worked on right now?
```

It should be short, current, and actionable.

### `memory.md`

`memory.md` is the persistent project and architecture memory.

It answers:

```text
What is currently true about this project or area?
What changed, why, and where?
What should the next agent know before working here?
```

It should be organized, confirmed, compressed, and category-based.

### Handoff / Temporary Context Package

A handoff or temporary context package is the scoped context given to a specific agent for a specific task.

It answers:

```text
What does this agent need for this one session?
```

It should be generated from:

- the current `plan.md`
- relevant `memory.md` excerpts
- relevant Yin/Yang contracts
- relevant files or references
- the current task prompt

It should not become a permanent catch-all `context.md` by default.

---

### `context_retrieval.md`

`context_retrieval.md` is the reusable deterministic search method for the project.

It answers:

```text
How should agents search the documentation graph before broad semantic search or broad file discovery?
```

It should define:

- metadata fields to search
- tag rules
- layer rules
- document type rules
- relationship traversal order
- exclusion rules
- example commands
- optional scripts
- how to build a context package
- how to log a search

It is separate from `memory.md`.

`memory.md` stores confirmed project state.

`context_retrieval.md` stores the retrieval method.

This separation prevents memory compression from accidentally deleting or changing the search procedure.

### `context_package.md`

`context_package.md` is a temporary task-specific context package.

It answers:

```text
What context was selected for this specific task?
```

It may include:

- task
- search goal
- filters used
- documents matched
- links followed
- relevant excerpts
- exclusions
- Search Log
- open questions
- handoff context

It should not become permanent memory by default.

Confirmed lasting facts move into `memory.md`.

Search method stays in `context_retrieval.md`.

### Metadata Index

A large project may also maintain a generated metadata index.

Possible files:

```text
metadata_index.json
metadata_index.md
context_index.md
```

The index may contain:

- document ID
- path
- title
- document type
- layer
- module ID
- submodule ID
- status
- tags
- parent/child links
- paired Yin/Yang links
- related documents
- updated date

The index is optional. It should be generated from document metadata when possible instead of manually maintained forever.


### `skills/`

`skills/` is an optional workspace helper system for reusable AI-agent instructions.

It is not Memory 2.0.

It does not replace `memory.md`.

It does not replace `context_retrieval.md`.

It stores reusable objective helper rules such as:

- local procedures
- recurring fix patterns
- verification checklists
- mistake-prevention rules
- tool usage notes
- stable workflow lessons
- small reusable task procedures

Skills help future agents avoid repeating the same mistakes and reduce context/token use.

They should not store:

- project status
- raw chat history
- temporary handoffs
- full memory
- plan items
- search method
- context packages
- secrets
- speculative notes

Search and retrieval logic belongs in:

```text
context_retrieval.md
```

not in `skills/`.

### Recommended Skills Structure

Preferred workspace structure:

```text
context/skills/
├── README.md
├── skills_index.md
├── skills_bundle.md
├── candidates/
│   └── <skill-name>/
│       └── SKILL.md
├── approved/
│   └── <skill-name>/
│       └── SKILL.md
└── archived/
```

Each individual `SKILL.md` is the source of truth.

```text
context/skills/**/SKILL.md
```

`skills_bundle.md` is generated. It may be used for maintenance, export, or optimization, but it must not become the source of truth.

### Skill Lifecycle

Recommended lifecycle:

```text
candidate → review → approved → archived
```

New skills should normally enter as candidates.

Approved skills should require human review.

Archived skills remain available for history but should not be used as active instructions.

### Default Skills Safety Policy

Recommended default policy:

```yaml
create_skills_structure: false
skills_format: "agentskills.io"
allow_skill_candidates: true
allow_auto_create_approved_skills: false
require_skill_review_before_activation: true
allow_external_skill_lookup: false
allow_skill_scripts: false
create_skills_index: true
create_skills_bundle: true
skills_bundle_is_generated: true
```

External skills may be checked or adapted later, but they must not be blindly imported.

Skill scripts are disabled by default.


## Why Not a Permanent `context.md`?

A permanent `context.md` sounds useful, but it easily becomes another unbounded context dump.

The problem:

- it duplicates `plan.md`
- it duplicates `memory.md`
- it accumulates old context
- it is hard to know what is current
- agents may paste it by default
- token cost grows
- stale assumptions survive

The framework therefore avoids a permanent `context.md` as a primary artifact.

Use temporary scoped context packages instead.


A temporary context package is different from a permanent `context.md`.

Use:

```text
context_retrieval.md = how to search
context_package.md   = what was selected for one task
memory.md            = confirmed current project truth
```

Do not merge these into one permanent context file.


A temporary context package may be created for:

- one Agent-2 implementation handoff
- one review session
- one model switch
- one debugging cycle
- one documentation update
- one focused module or category

After the task is complete, the temporary context package should be discarded, archived, or replaced. Confirmed facts move into `memory.md`. Active task state remains in `plan.md`.

---

## Files Outside Default State Maintenance Scope

Workspace State Maintenance must not clean or rewrite these by default:

```text
context_retrieval.md
context_package_template.md
search_log_template.md
metadata index templates
Yin/Yang templates
Genesis prompts
Triage prompts
Workspace initialization prompts
application source code
AGENTS.md
agenten.md
```

`AGENTS.md` and `agenten.md` are outside the Workspace Context Initialization and Workspace State Maintenance scope unless the user explicitly includes them.

This boundary matters because these files can contain agent/runtime instructions for a specific tool or repository. They should not be silently rewritten by a general workspace state maintenance prompt.

`context_retrieval.md` is also not a normal cleanup target.

It is a stable method file.

It may be health-checked or explicitly revised, but it should not be compressed like `memory.md` or cleaned like `plan.md`.


# 1. `plan.md`

## Purpose

`plan.md` is the clean current-task file.

It tells an AI agent what to do now, where the task belongs, what is in scope, what is out of scope, and how completion will be checked.

It exists to prevent:

- task drift
- repeated explanation
- accidental scope expansion
- unfinished task confusion
- agents working on the wrong category
- mixing current work with long-term memory

`plan.md` is intentionally short.

It is not where the full history goes.

---

## What `plan.md` Is

`plan.md` is:

- a current task brief
- a focused execution checklist
- a category-based task organizer
- a scope boundary
- a short operational plan
- a handoff aid when switching agents
- a live task status file

It may contain checkboxes.

It may contain short notes.

It may contain one active task or a small set of tightly related tasks inside one category.

---

## What `plan.md` Is Not

`plan.md` is not:

- a roadmap
- a backlog
- a changelog
- a debug diary
- a transcript
- a long-term memory file
- a place for raw failed attempts
- a place for speculative reasoning
- a list of unrelated future tasks
- a replacement for `memory.md`
- a replacement for Yin/Yang contracts

Do not accumulate many unrelated tasks in `plan.md`.

If the user wants a backlog, use a backlog or issue tracker. Do not turn `plan.md` into one.

---

## Category Organization

`plan.md` should be organized by category, module, feature, or area when useful.

Example categories:

```text
Settings
Dashboard
Auth
Provider
Input
Layout Shell
Prompt Library
State Management
```

The goal is fast orientation.

If the current work is in Settings/Input, the agent should immediately see the Settings/Input task block and not read unrelated plans.

---

## Recommended `plan.md` Structure

```markdown
# Plan

_Last updated: YYYY-MM-DD_

---

## Current Focus

[One sentence describing the active task.]

---

## [Category / Module / Area]

### Task

[One short sentence describing what must be done.]

### Goal

[What done looks like.]

### Status

- [ ] [Step 1]
- [ ] [Step 2]
- [ ] [Step 3]

### Scope

In scope:

- [Item]
- [Item]

Out of scope:

- [Item]
- [Item]

### Inputs / References

- [Relevant file, contract, screenshot, handoff, or note]

### Acceptance Criteria

- [ ] [Criterion]
- [ ] [Criterion]

### Notes

[Short notes only.]
```

---

## Practical `plan.md` Example

```markdown
# Plan

_Last updated: 2026-06-06_

---

## Current Focus

Fix the Settings/Input collapsible block height issue.

---

## Settings / Input

### Task

Fix the panel height change when the default collapsed setting is toggled.

### Goal

The Settings/Input panel keeps a stable height regardless of default collapsed state.

### Status

- [x] Inspect Settings/Input collapse state handling
- [x] Apply layout/state fix
- [ ] Verify stable panel height after toggling default collapsed state

### Scope

In scope:

- Settings/Input category
- collapsible input blocks
- default collapsed state behavior
- panel height or min-height behavior

Out of scope:

- Settings/Provider category
- global Settings layout
- Dashboard layout
- provider creation flow

### Inputs / References

- Agent-2 handoff: Settings/Input collapse height bug
- Relevant component: unknown; inspect Settings/Input feature area only

### Acceptance Criteria

- [ ] Toggling default collapsed state does not change panel height.
- [ ] Existing collapse/expand behavior still works.
- [ ] No unrelated Settings categories are modified.

### Notes

If the first layout fix does not work, check whether the height change is caused by derived collapse state rather than CSS alone.
```

---

## `plan.md` Lifecycle

### 1. Create or Update at Task Start

Before starting a focused AI session, create or update `plan.md`.

The plan should tell the agent:

- what is being worked on
- where it belongs
- what is allowed
- what is not allowed
- what completion means

### 2. Use During the Task

The active agent uses `plan.md` to stay focused.

When a step is completed, it may be checked off.

Do not add long reasoning.

Do not add raw logs.

### 3. Update After Completion

When the task is complete:

1. check off completed items
2. verify acceptance criteria
3. move confirmed lasting facts into `memory.md`
4. remove or replace completed task detail from `plan.md`
5. start the next focused task

### 4. Reset or Replace When Moving On

`plan.md` should not grow indefinitely.

Once the task is done, clear the active task or replace it with the next one.

---

## When to Inject `plan.md`

Inject `plan.md` when:

- continuing an in-progress task
- switching from one agent to another
- moving from Agent 1 triage to Agent 2 execution
- asking an implementation agent to work in a specific area
- resuming after a model/platform limit
- verifying whether the current task is complete
- reviewing scope boundaries

Do not inject `plan.md` when it is irrelevant.

Do not inject old `plan.md` content from completed tasks.

---

# 2. `memory.md`

## Purpose

`memory.md` is the confirmed project and architecture memory.

It preserves what future agents need to know so they do not repeat mistakes, re-open settled decisions, or reimplement completed work.

It is the external memory that survives clean chats, model switches, coding-agent switches, and session resets.

It exists to answer:

```text
What is currently true here?
What changed?
Why was it changed?
Which files or contracts are affected?
What should the next agent know before touching this area?
What has already been tried and found ineffective, if the issue is still unresolved?
```

`memory.md` is more detailed than `plan.md`.

`plan.md` is current focus. `memory.md` is confirmed memory.

---

## What `memory.md` Is

`memory.md` is:

- confirmed project state
- confirmed architecture state
- category-organized memory
- compact implementation history
- a record of current behavior
- a record of relevant changed files
- a record of affected contracts
- a continuity bridge across AI tools
- a guard against repeating ineffective work
- a compressed context source for future agents

It should be organized by category, module, feature, or system area.

---

## What `memory.md` Is Not

`memory.md` is not:

- an append-only changelog forever
- a raw debug log
- a transcript
- a scratchpad
- a backlog
- a roadmap
- a place for secrets
- a place for uncertain guesses
- a place for every failed attempt
- a place for full stack traces by default
- a place for old states that are no longer true
- a replacement for Yin/Yang contracts
- a replacement for Git history

`memory.md` should not preserve noise.

It should preserve useful, confirmed, compressed context.

---

## Category Organization

`memory.md` should be organized by the areas future agents will actually work in.

Example:

```markdown
# Memory

_Last updated: 2026-06-06_
_Last compressed: 2026-06-01_
_Rounds since compression: 8_
_Compression status: OK_

---

## Settings

### Input

### Provider

---

## Dashboard

---

## Auth

---

## Layout Shell
```

This lets an agent working on Settings/Input read only the Settings/Input memory block instead of the entire project history.

---

## Recommended `memory.md` Structure

```markdown
# Memory

_Last updated: YYYY-MM-DD_
_Last compressed: YYYY-MM-DD_
_Rounds since compression: 0_
_Compression status: OK_

---

## [Category / Module / Area]

### Current State

[What is currently true about this area.]

### Confirmed Changes

#### [YYYY-MM-DD] — [Short change title]

**Status:** Confirmed  
**Reason:** [Why this change was made.]  
**Changed:** [What changed.]  
**Files affected:** [Files, if known.]  
**Contracts affected:** [Yin/Yang/API/other contracts, if any.]  
**Dependencies:** [Relevant dependencies.]  
**Verification:** [How it was verified.]  

### Useful Troubleshooting Notes

[Only include compact notes that still help future agents.]

### Open Follow-Up

[Only unresolved follow-up relevant to this area.]
```

---

## Practical `memory.md` Example

```markdown
# Memory

_Last updated: 2026-06-06_
_Last compressed: 2026-06-01_
_Rounds since compression: 9_
_Compression status: OK_

---

## Settings

### Input

#### Current State

Settings/Input contains collapsible input blocks. The panel height must remain stable when default collapsed state is toggled. Collapse/expand behavior may change visible block content but must not resize the surrounding panel.

#### Confirmed Changes

##### 2026-06-06 — Stable height for default collapsed toggle

**Status:** Confirmed  
**Reason:** Toggling default collapsed state changed the visible panel height, causing layout shift.  
**Changed:** The Settings/Input collapsible block layout now keeps a stable panel height independent of default collapsed state.  
**Files affected:** `src/settings/input/...`  
**Contracts affected:** None confirmed.  
**Dependencies:** Settings/Input collapse state handling.  
**Verification:** Manual UI check: toggling default collapsed no longer changes panel height.

#### Useful Troubleshooting Notes

- A wrapper-only min-height change was attempted first and did not fully fix the issue. If the bug reappears, inspect derived collapse state and panel layout synchronization rather than only CSS height.
```

This note is useful while the issue is active or likely to recur. Once the area is stable for long enough, compress it:

```markdown
#### Current State

Settings/Input collapsible blocks keep stable panel height when default collapsed state changes. This behavior is intentional and should not regress.
```

The detailed troubleshooting note can then be removed or archived.

---

## Failed Attempts and Troubleshooting Notes

The framework does not preserve raw failed attempts by default.

However, it may preserve compact troubleshooting notes when they prevent repeated ineffective fixes.

Use this rule:

```text
Do not store raw failed attempts.
Do store compact, useful “already tried / ineffective” facts while they are still diagnostically useful.
```

Bad memory entry:

```markdown
I tried changing the CSS and it did not work. Then I tried another thing and maybe the state was weird. The model thought maybe the parent div was wrong but then it changed something and it still did not work...
```

Good memory entry:

```markdown
A wrapper-only min-height fix did not resolve the Settings/Input collapse height issue. If the issue persists, inspect derived collapse state and panel layout synchronization instead of only CSS height.
```

Once the issue is resolved and stable, compress or remove the troubleshooting note.

---

## `memory.md` Lifecycle

### 1. Update Only After Confirmation

Do not write speculative findings into `memory.md` as truth.

Add or update memory only when:

- a change is implemented
- the change is verified
- the result is intentionally kept
- the fact will help future work

### 2. Record Current Truth

Prefer current truth over historical detail.

If a previous state was replaced, remove or compress it.

`memory.md` should answer what matters now, not preserve every step taken to get there.

### 3. Keep Useful Troubleshooting Only While Useful

If a fix attempt failed and the issue is still unresolved, preserve a compact note only if it prevents repetition.

When the issue is resolved, compress or remove that note.

### 4. Organize by Area

Put each entry where future agents will look.

Do not put every change at the top in chronological order only.

Chronological order is useful inside a category, but category-based retrieval is more important for AI work.

### 5. Compress Periodically

Memory that is never compressed becomes another long chat.

Compression is mandatory for long-running projects.

---

## When to Inject `memory.md`

Inject `memory.md` when:

- the agent works in an area with relevant prior decisions
- a bug repeats
- a previous fix may affect the current task
- switching between AI tools
- resuming after a limit
- asking a model to continue work
- checking whether something was already tried
- preventing reimplementation
- providing context for a Yin/Yang update
- preparing a Triage handoff

Do not inject full `memory.md` by default.

Inject only relevant excerpts.

If working in Settings/Input, provide the Settings/Input memory block, not the entire project memory.

---

# 3. Handoffs and Temporary Context Packages

## Purpose

A handoff or temporary context package is scoped context for one agent and one task.

It is generated from:

- current `plan.md`
- relevant `memory.md` excerpts
- relevant Yin/Yang contracts
- current issue description
- relevant references
- acceptance criteria
- output requirements

It is not a permanent memory file.

---

## When to Create a Temporary Context Package

Create a temporary context package when:

- switching from Agent 1 to Agent 2
- moving from one model to another
- moving from one platform to another
- handing a task from ChatGPT to Claude Code
- handing a task from Claude to Codex
- handing a task from Cursor to ChatGPT
- preparing a focused review
- preparing a focused implementation task
- continuing a task after a usage limit
- extracting only relevant context for a specific module

---

## What to Include

Include:

- task
- category/module/area
- current goal
- current status
- relevant constraints
- relevant acceptance criteria
- relevant memory excerpts
- relevant contract references
- relevant metadata IDs
- relevant module/submodule IDs
- relevant tags
- known files or discovery boundaries
- Search Log when deterministic retrieval was used
- known blockers
- output format

---

## What Not to Include

Do not include:

- unrelated memory sections
- full old chats
- unrelated plans
- stale assumptions
- raw failed attempts
- long logs unless needed
- screenshots unless Agent 2 truly needs them
- secrets
- entire repository maps by default
- broad roadmap context

The context package exists to reduce context, not to move the entire project into a new shape.

---

## Example Temporary Context Package

```markdown
# Temporary Context Package — Settings/Input Collapse Height

## Task

Fix Settings/Input panel height changing when default collapsed state is toggled.

## Current Plan Excerpt

Settings/Input: stable panel height after default collapse toggle.

## Relevant Memory Excerpt

Settings/Input collapsible blocks should keep stable panel height independent of default collapsed state. A wrapper-only min-height change did not fully solve this previously; inspect derived collapse state and panel layout synchronization if the issue persists.

## Metadata Context

- layer: Core
- module_id: settings
- submodule_id: settings.input
- related_yin: core.settings.input.yin
- related_yang: core.settings.input.yang
- tags: settings, input, collapse, ui-state

## Search Log

- Filters used: module_id=settings, submodule_id=settings.input, tags=collapse/ui-state
- Documents matched: core.settings.input.yin, core.settings.input.yang
- Memory matched: memory.md → Settings / Input
- Excluded: Settings/Provider, Dashboard, archived drafts

## Relevant Scope

In scope:
- Settings/Input category
- collapsible input blocks
- default collapsed state
- panel height behavior

Out of scope:
- Settings/Provider
- Dashboard
- global Settings layout

## Acceptance Criteria

- Toggling default collapsed state does not resize the panel.
- Existing collapse/expand behavior still works.
- No unrelated Settings categories are modified.

## Output Format

Return changed files, summary, verification, and blockers.
```

This can be pasted into an implementation agent without giving it the entire memory file.

---

---

# 4. Deterministic Retrieval State

State Management and deterministic retrieval are connected, but they are not the same thing.

State answers:

```text
What is currently true?
```

Retrieval answers:

```text
How do we find the relevant truth for this task?
```

The framework therefore separates:

| Artifact | Purpose |
|---|---|
| `memory.md` | Confirmed current project / architecture state |
| `plan.md` | Current task focus |
| `context_retrieval.md` | Reusable deterministic search method |
| `metadata_index.json/md` | Optional generated lookup index |
| `context_package.md` | Temporary selected context for one task |
| handoff | Scoped task instruction for one agent |

This prevents three common failures:

1. Search logic is lost during memory compression.
2. Memory becomes polluted with procedural retrieval instructions.
3. Each new agent invents a different search method.

## `context_retrieval.md`

`context_retrieval.md` should be treated as a stable project artifact when the project uses a Deterministic Metadata Graph.

It may define:

- metadata search priority
- allowed metadata fields
- layer filters
- document type filters
- tag vocabulary
- module/submodule matching
- graph traversal order
- paired Yin/Yang retrieval
- memory section retrieval
- exclusion rules
- archive/deprecated handling
- example `ripgrep` commands
- example Python scripts
- context package format
- Search Log format

Recommended search priority:

```text
1. Exact id, module_id, submodule_id, or document_type
2. Layer
3. High-signal tags
4. Paired Yin/Yang links
5. Parent/child links where needed
6. Related memory sections
7. Prior handoffs where relevant
8. Semantic search only as helper
```

## Search Log

When deterministic retrieval is used, the resulting context package or handoff should include a Search Log.

A Search Log records:

- task or query
- filters used
- documents matched
- memory sections matched
- links followed
- files excluded
- archived/deprecated documents skipped
- unresolved retrieval uncertainty

Example:

```markdown
## Search Log

Query:
Settings/Input collapse height bug

Filters used:
- layer: Core
- module_id: settings
- submodule_id: settings.input
- tags: settings, input, collapse, ui-state

Documents matched:
- core.settings.input.yin
- core.settings.input.yang

Memory matched:
- memory.md → Settings / Input

Links followed:
- paired_yang
- parent module

Excluded:
- Settings/Provider
- Dashboard
- archived drafts
```

## Relationship to `memory.md`

`memory.md` may reference metadata fields, but it should not store the full retrieval method.

Good memory reference:

```markdown
## Settings / Input

Related metadata:
- module_id: settings
- submodule_id: settings.input
- related_yin: core.settings.input.yin
- related_yang: core.settings.input.yang
- tags: settings, input, collapse, ui-state
```

Bad memory reference:

```markdown
Every time you search, run this full retrieval algorithm with all commands, traversal rules,
script examples, exclusion rules, and Search Log requirements...
```

Store that method in `context_retrieval.md`.

## Relationship to Agent Switching

When switching agents, provide:

- current `plan.md` excerpt
- relevant `memory.md` excerpt
- relevant metadata IDs
- context package or Search Log if available
- handoff

Do not require each agent to reinvent how retrieval works.

If `context_retrieval.md` exists, the next agent can use the same retrieval method.


# 5. State Update Workflow

## Before Starting a Task

1. Identify the category/module/area.
2. Update `plan.md` with current task focus.
3. Read relevant `memory.md` section.
4. Attach relevant Yin/Yang contracts if needed.
5. Prepare a scoped handoff if using a separate agent.
6. Do not include unrelated memory.

## During a Task

1. Use `plan.md` to track current steps.
2. Do not write speculative notes into `memory.md`.
3. If a fix attempt fails, keep the note temporary unless it becomes diagnostically useful.
4. Do not expand scope silently.
5. If a contract gap appears, stop and update the contract workflow.

## After Successful Completion

1. Verify acceptance criteria.
2. Check off task items in `plan.md`.
3. Add confirmed useful facts to `memory.md`.
4. Include files/contracts affected if useful.
5. Remove completed task detail from active `plan.md`.
6. If deterministic retrieval was used, keep the Search Log in the temporary context package or handoff record where useful.
7. Move only confirmed lasting facts into `memory.md`; do not move the entire Search Log into memory by default.
8. Increment `Rounds since compression`.
9. Check whether compression is recommended or mandatory.

## After a Failed Fix

1. Do not record raw failure in `memory.md`.
2. If the failure is diagnostically useful, add a compact troubleshooting note.
3. Keep the current task in `plan.md`.
4. Update next steps.
5. Avoid repeating the same failed strategy.

## After an Unresolved Issue

If the issue remains unresolved, `memory.md` may contain a compact note:

```markdown
### Useful Troubleshooting Notes

- Changing only the wrapper min-height did not resolve the issue. The remaining cause likely involves derived collapse state or parent layout recalculation.
```

This helps the next agent avoid technical stillstand.

## After a Contract Update

If a Yin/Yang contract changes:

1. update the relevant contract
2. record the confirmed contract change in `memory.md`
3. note affected implementation areas
4. update `plan.md` if implementation remains
5. generate a scoped handoff for Agent 2 if needed

---

# 6. Compression and Cleanup

## Why Compression Matters

`memory.md` and `plan.md` solve context loss, but they can become a new context problem if never maintained.

An uncompressed `memory.md` can become like a long stale chat:

- too many old details
- obsolete decisions
- repeated entries
- unresolved contradictions
- failed attempts mixed with truth
- large token footprint
- lower attention quality
- repeated model mistakes

The purpose of memory is not to store everything. It is to preserve useful current truth.

Compression keeps memory valuable.

---

## The 10/20 Rule

Use the 10/20 rule:

```text
~10 meaningful rounds since compression = compression recommended
~20 meaningful rounds since compression = compression mandatory
```

A meaningful round is a completed task cycle that changes implementation, contracts, architecture, or useful project state.

At around 10 rounds, the agent should warn:

```text
memory.md has accumulated enough new state that compression is recommended soon.
```

At around 20 rounds, the agent should warn more strongly:

```text
memory.md compression is now mandatory before broad new work. Continuing without compression may increase token usage, stale-context risk, and repeated implementation mistakes.
```

The exact threshold can be adjusted by project size, but the principle remains: memory must be actively maintained.

---

## Compression Metadata

Add metadata at the top of `memory.md`:

```markdown
# Memory

_Last updated: 2026-06-06_
_Last compressed: 2026-06-01_
_Rounds since compression: 8_
_Compression status: OK_
```

Possible compression statuses:

| Status | Meaning |
|---|---|
| `OK` | No immediate cleanup needed |
| `RECOMMENDED` | Compression should happen soon |
| `REQUIRED` | Compression should happen before broad new work |
| `OVERDUE` | Memory is likely harming context quality |
| `ARCHIVED` | This file has been replaced by a compressed version |

After each meaningful completed task, increment `Rounds since compression`.

After compression, reset it to `0` and update `Last compressed`.

---

## Memory Lifecycle Stages

Memory entries can move through lifecycle stages.

| Stage | Meaning | Typical handling |
|---|---|---|
| `Hot` | Active or recently relevant | Keep detailed enough for current work |
| `Warm` | Recently changed, may still affect work | Keep concise but accessible |
| `Cold` | Stable, rarely needed | Compress to current truth |
| `Archive` | Historical, not normally injected | Move to archive or backup |
| `Remove` | Obsolete, wrong, superseded, or no longer useful | Delete from active memory |

This is not meant to create bureaucracy. It is a practical cleanup model.

---

## What to Compress

Compress:

- old detailed implementation notes
- resolved troubleshooting notes
- duplicate entries
- repeated decisions
- superseded states
- old task details
- long file lists no longer needed
- verbose explanations that can become one sentence
- older context that is no longer needed for implementation

Before:

```markdown
The model tried to fix the Settings/Input collapse issue by adding min-height to the wrapper. It also checked several components and then changed the panel container. This did not fix it. Then the next model found that the state update caused the panel to recalculate height and fixed it...
```

After:

```markdown
Settings/Input collapse panel height is stable after default collapsed state changes. Root cause was state/layout recalculation, not wrapper min-height alone.
```

---

## What to Preserve

Preserve:

- current architecture truth
- current module behavior
- active contracts
- important decisions
- still-relevant files
- still-relevant dependencies
- still-useful troubleshooting notes for unresolved issues
- constraints that prevent future mistakes
- confirmed state needed by future agents

---

## What to Remove

Remove:

- raw failed attempts
- old speculation
- resolved dead ends
- contradicted assumptions
- stale file paths
- outdated implementation details
- repeated entries
- old task checklist items
- obsolete temporary context
- anything the next agent does not need

---

## Compression Must Not Delete Retrieval Method

Memory compression must not delete the project's retrieval method.

If retrieval rules are stored in `context_retrieval.md`, leave that file alone unless the task is specifically to update retrieval rules.

During memory compression:

- preserve metadata references that are still useful
- preserve module/submodule IDs in memory sections
- preserve related Yin/Yang references where useful
- remove old Search Logs from memory unless they explain an unresolved issue
- do not paste full retrieval procedures into `memory.md`
- do not remove `context_retrieval.md`

This keeps memory small while keeping retrieval repeatable.


## Compression Workflow

### Manual Compression

1. Open `memory.md`.
2. Review each category.
3. Keep current truth.
4. Merge duplicates.
5. Remove obsolete entries.
6. Compress resolved troubleshooting notes.
7. Keep useful unresolved troubleshooting notes.
8. Update metadata.
9. Save a backup of the previous version.

### High-Quota Assistant Compression

A useful workflow is to compress `memory.md` outside the coding agent.

1. Upload `memory.md` and optionally `plan.md` to a high-quota assistant.
2. Ask it to compress the files according to Allzy State Management rules.
3. Require it to preserve current truth and remove stale noise.
4. Require it to keep useful unresolved troubleshooting notes.
5. Download the compressed replacement.
6. Archive the old file as a backup.
7. Replace the active `memory.md`.
8. Reset compression metadata.

This saves implementation-agent context and token budget.

The coding agent should spend context on code, not on compressing a large memory file unless that is the task.

### Backup Recommendation

Before replacing memory, create a backup:

```text
memory.backup.YYYY-MM-DD.md
```

or archive a group:

```text
state-backup-YYYY-MM-DD.zip
```

The backup is for recovery, not for normal injection into AI prompts.

---

# 7. Cross-Agent Continuity

State files make it possible to switch between agents without losing the project.

Examples:

- Claude usage limit is reached, continue in Codex
- a small task is better suited for a faster/cheaper coding agent
- ChatGPT performs triage, Cursor implements
- Claude reviews contracts, Codex applies code changes
- Gemini analyzes a UI screenshot, Claude Code fixes implementation
- a future Prism workflow renders a model/platform-specific handoff

Without `plan.md` and `memory.md`, every agent starts cold.

With them, the next agent can know:

- what the active task is
- what was already changed
- which area is involved
- which files may matter
- which attempts did not help
- which contracts apply
- what is out of scope

The state files are the continuity layer between AI tools.

---

## Agent Switching Workflow

When switching agents:

1. Update `plan.md`.
2. Extract only relevant `memory.md` sections.
3. Include relevant contracts or handoff.
4. State the target agent/platform if relevant.
5. Define output format.
6. Keep the scope narrow.
7. Do not paste the full project memory unless absolutely needed.

Example:

```text
Switching from Claude to Codex for Settings/Input fix.

Provide:
- current plan excerpt
- Settings/Input memory excerpt
- Agent-2 handoff
- relevant files or discovery boundaries

Do not provide:
- full memory.md
- old unrelated Settings/Provider notes
- Dashboard history
- old failed chats
```

---

# 8. Relationship to Triage and Maintenance

Triage uses State Management to prepare clean Agent-2 handoffs.

Agent 1 may use:

- current `plan.md`
- relevant `memory.md` excerpts
- relevant Yin/Yang contracts
- screenshots or bug reports
- model/platform references

Agent 2 should receive:

- a scoped handoff
- relevant state excerpts
- narrow file discovery boundaries
- acceptance criteria

Agent 2 should not receive:

- full project memory by default
- raw old chat history
- unrelated memory sections
- old failed attempts
- broad screenshots unless necessary


When a Deterministic Metadata Graph exists, Agent 1 should use `context_retrieval.md` and metadata filters before broad file discovery.

Useful retrieval inputs:

- active area from `plan.md`
- module ID
- submodule ID
- layer
- document type
- tags
- paired Yin/Yang links
- relevant `memory.md` section
- previous handoff IDs
- metadata index if available

The selected result should become a temporary context package or be embedded into the Agent-2 handoff with a Search Log.

After Agent 2 completes the task, confirmed state may be written back to `memory.md`.

This closes the loop:

```text
plan.md → triage handoff → implementation → verification → memory.md → next plan
```

---

# 9. Relationship to Yin/Yang Contracts

Yin/Yang contracts define intent and technical execution rules.

State files do not replace them.

Use this distinction:

| Artifact | Purpose |
|---|---|
| Yin | human intent, domain meaning, workflows, product rules |
| Yang | technical execution contract, schemas, decisions, actions, invariants |
| plan.md | current task focus |
| memory.md | confirmed current project/architecture state |
| handoff | scoped context for a specific agent/task |

If `memory.md` records a behavior that is not documented in Yin/Yang, decide whether the contract must be updated.

If a bug reveals a missing rule, update the contract rather than only recording it in memory.

If Yin/Yang changed, record the confirmed update in memory only as a current-state note.

`memory.md` is not the authoritative contract. It is the continuity layer.

---

# 10. Relationship to the Deterministic Metadata Graph

The Deterministic Metadata Graph can make state retrieval more precise by linking documents through stable metadata.

State files can reference graph objects such as:

- module IDs
- document IDs
- Yin documents
- Yang contracts
- schemas
- related contracts
- ADRs
- trace maps

Example memory entry:

```markdown
**Related contracts:**
- `settings.input.yin`
- `settings.input.core`
- `settings.input.state-schema`
```

This helps future tooling or AI preparation workflows load only the relevant graph neighborhood.

However, `memory.md` itself should not become a full graph database.

Use stable references where helpful. Keep memory readable.


The recommended artifact split is:

```text
metadata/frontmatter = identity and relationships inside documents
metadata_index       = optional generated lookup table
context_retrieval.md = reusable search method
context_package.md   = temporary selected context
memory.md            = confirmed project state
```

Do not make `memory.md` carry the entire retrieval system.

`memory.md` may point to graph IDs.

`context_retrieval.md` defines how to use those IDs.

`context_package.md` records what was selected for a specific task.


---

# 11. Anti-Patterns


## Retrieval Method Inside Memory

`memory.md` contains the full deterministic search procedure, example scripts, command snippets, and traversal rules.

Why it fails:

- memory compression may delete or distort retrieval logic
- memory becomes procedural instead of state-focused
- every agent must read more than necessary
- search rules are harder to version

Fix:

- store retrieval method in `context_retrieval.md`
- keep only relevant metadata references in memory

## Missing Search Log

A context package contains retrieved context but does not explain how it was selected.

Why it fails:

- later agents cannot audit selection
- wrong exclusions are hard to detect
- context may look arbitrary
- repeated searches may differ

Fix:

- include a short Search Log when deterministic retrieval is used


## Permanent Context Dump

A file contains everything: task, memory, logs, old chats, plans, failed attempts, and future ideas.

Why it fails:

- too much noise
- unclear current truth
- high token cost
- old assumptions survive
- agents repeat mistakes

Fix:

- separate `plan.md`, `memory.md`, and handoffs

## Append-Only Memory Forever

`memory.md` grows forever without compression.

Why it fails:

- memory becomes another long stale chat
- current truth is buried
- token cost grows
- outdated details confuse agents

Fix:

- apply the 10/20 rule
- compress periodically
- archive or remove old detail

## Raw Failed Attempt Logging

Every failed attempt is stored in memory.

Why it fails:

- noise accumulates
- speculative reasoning becomes misleading
- future agents follow bad paths

Fix:

- store only compact useful troubleshooting facts while unresolved
- remove or compress after resolution

## Plan as Backlog

`plan.md` becomes a long list of future tasks.

Why it fails:

- current task focus disappears
- agents see unrelated work
- scope drift increases

Fix:

- keep `plan.md` focused on current work
- use a backlog or issue tracker elsewhere

## Full Memory Injection

The entire `memory.md` is pasted into every AI session.

Why it fails:

- unnecessary tokens
- attention dilution
- stale cross-contamination

Fix:

- inject only relevant category sections

## No Compression Metadata

Agents cannot tell whether memory is stale or too large.

Why it fails:

- cleanup is delayed
- context quality silently degrades

Fix:

- track last compression and rounds since compression

## Memory as Contract

Agents treat memory notes as authoritative product or technical contracts.

Why it fails:

- contracts drift
- behavior becomes undocumented
- memory becomes hidden specification

Fix:

- update Yin/Yang when behavior or technical contract changes
- keep memory as continuity, not authority

## Over-Abstract Memory

Memory entries are too vague to help.

Bad:

```markdown
Fixed Settings bug.
```

Good:

```markdown
Settings/Input panel height remains stable when default collapsed state changes. Root cause involved collapse state/layout recalculation, not wrapper min-height alone.
```

Fix:

- include enough detail to prevent repeated mistakes
- remove unnecessary narrative

---

# 12. Quality Checklist

## `plan.md` Checklist

- [ ] Current task is clear.
- [ ] Category/module/area is named.
- [ ] Goal is specific.
- [ ] Status checklist is short.
- [ ] Scope is explicit.
- [ ] Out-of-scope items are explicit.
- [ ] Inputs/references are relevant.
- [ ] Acceptance criteria are testable.
- [ ] No unrelated tasks are included.
- [ ] No long history is included.
- [ ] Completed task detail is removed after memory update.

## `memory.md` Checklist

- [ ] Organized by category/module/area.
- [ ] Current state is clear.
- [ ] Confirmed changes are recorded.
- [ ] Files affected are listed where useful.
- [ ] Contracts affected are listed where useful.
- [ ] Verification is noted where useful.
- [ ] Useful troubleshooting notes are compact.
- [ ] Raw failed attempts are not stored.
- [ ] Obsolete states are removed or compressed.
- [ ] No secrets are present.
- [ ] Compression metadata is present.
- [ ] Rounds since compression is updated.
- [ ] Old entries are compressed or archived.

## Context Package Checklist

- [ ] Built for one agent and one task.
- [ ] Uses relevant `plan.md` excerpt.
- [ ] Uses relevant `memory.md` excerpt.
- [ ] Includes relevant contracts if needed.
- [ ] Excludes unrelated memory.
- [ ] Excludes raw old chat history.
- [ ] Excludes secrets.
- [ ] Scope is narrow.
- [ ] Acceptance criteria are clear.
- [ ] Output format is clear.


## Retrieval Artifact Checklist

- [ ] `context_retrieval.md` exists for large or metadata-heavy projects.
- [ ] Retrieval method is stored outside `memory.md`.
- [ ] Metadata fields used for retrieval are documented.
- [ ] Search priority is defined.
- [ ] Exclusion rules are defined.
- [ ] Search Log format is defined.
- [ ] Temporary context packages include filters used.
- [ ] Temporary context packages include matched documents.
- [ ] Temporary context packages include exclusions.
- [ ] `memory.md` references metadata IDs where useful.
- [ ] Old Search Logs are not copied into memory by default.
- [ ] Metadata index is generated if project size requires it.


## Compression Checklist

- [ ] Backup created.
- [ ] Duplicate entries merged.
- [ ] Superseded states removed.
- [ ] Current truth preserved.
- [ ] Resolved troubleshooting compressed.
- [ ] Unresolved useful troubleshooting retained.
- [ ] Old task detail removed.
- [ ] Metadata updated.
- [ ] Rounds since compression reset.
- [ ] Compressed file reviewed before replacement.

---

# Operational Workspace / Context Prompt Family

State Management is supported by operational prompts.

The current primary prompts are:

| Prompt | Role |
|---|---|
| `workspace_context_initialization_prompt.md` | Create, inspect, or repair the workspace context layer |
| `workspace_state_maintenance_prompt.md` | Clean, compress, and maintain living workspace state |
| `context_retrieval_builder_prompt.md` | Retrieve and package selected context for a task, review, documentation job, or handoff |
| `document_metadata_enrichment_prompt.md` | Add or update metadata/frontmatter so documents can participate in retrieval |

The Workspace Context Initialization prompt may later be split into focused single-artifact prompts, for example:

```text
plan_md_prompt.md
memory_md_prompt.md
context_retrieval_prompt.md
context_package_generation_prompt.md
metadata_index_generation_prompt.md
skills_maintenance_prompt.md
```

These single-artifact prompts are optional operational convenience prompts.

They should not be treated as required source files until they exist.

The large initializer remains the universal setup/check/repair prompt.

The focused prompts are useful when a user wants to create or repair only one artifact.

---

# State Prompt Boundaries

Use the correct prompt for the correct job.

| Need | Use |
|---|---|
| Create/check the workspace context layer | `workspace_context_initialization_prompt.md` |
| Clean/compress `plan.md`, `memory.md`, or `skills/` | `workspace_state_maintenance_prompt.md` |
| Find and package relevant task context | `context_retrieval_builder_prompt.md` |
| Add retrieval metadata to a document | `document_metadata_enrichment_prompt.md` |
| Create final Yin/Yang specification prompt | `yin_yang_prompt_generator.md` |
| Diagnose bug and create Agent-2 handoff | Triage prompt family |

Do not use State Management prompts to implement code.

Do not use State Management prompts to create Yin/Yang documents.

Do not use State Management prompts to perform Triage.

Do not use State Management prompts to rewrite framework templates.

---

## Website-Ready Summary

State Management keeps AI-assisted projects coherent across sessions, models, and tools.

The Allzy Framework uses two core state files:

```text
plan.md   = current task focus
memory.md = confirmed project and architecture memory
```

For projects that use deterministic metadata retrieval, it may also use:

```text
context_retrieval.md = reusable search method
context_package.md   = temporary selected context for one task
metadata_index       = optional generated lookup index
```

`plan.md` tells the current agent what to do now. It is short, scoped, and temporary.

`memory.md` preserves confirmed project state, architecture decisions, relevant changes, affected files, contracts, and useful troubleshooting facts. It is organized by area so future agents can read only what matters.

Together, they prevent repeated fixes, lost context, stale assumptions, and unnecessary re-explanation. They also make it possible to move work between ChatGPT, Claude, Codex, Cursor, Gemini, or other agents without restarting from zero.

`context_retrieval.md` keeps the search method reusable and separate from memory. `context_package.md` records what was selected for a specific task. This prevents each agent from inventing a new search process and keeps memory focused on confirmed project truth.

State Management does not mean saving everything. Uncompressed memory becomes another token-heavy, stale context problem. The framework therefore uses compression, cleanup, and scoped handoffs to preserve current truth while removing noise.

The goal is not more documentation. The goal is controlled continuity.


## Cleanup and Compression Metadata

Workspace state files should track cleanup/compression metadata where useful.

Recommended fields:

```yaml
last_maintenance: "YYYY-MM-DD"
last_compressed: "YYYY-MM-DD"
entries_since_maintenance: 0
rounds_since_compression: 0
cleanup_status: "OK | REVIEW_NEEDED | STALE | OVERGROWN"
compression_status: "OK | NEEDED | DONE | REVIEW_NEEDED"
```

Recommended thresholds:

```text
0–9 new entries/rounds since compression  → OK
10–19                                      → compression recommended
20+                                        → compression required
```

Maintenance should reset counters only when compression or cleanup actually happened.

Do not pretend a file was cleaned if only inspected.

