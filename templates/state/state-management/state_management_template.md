---
id: "allzy.framework.templates.state.state-management"
title: "06 — State Management Template"
artifact_type: "Template"
template_family: "state.state-management"
status: "Draft"
version: "0.2.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - template
  - state-management
  - workspace-context
---

# 06 — State Management Template

## Purpose

State Management in the Allzy Framework means preserving the right project/session state for AI-assisted work without polluting the next task.

AI development sessions are stateless by default. Each new chat, coding agent, IDE assistant, CLI agent, or model session starts with limited or no reliable memory of previous decisions, confirmed implementation state, failed fixes, active contracts, or current task boundaries.

This template document defines reusable structures for:

```text
plan.md
memory.md
context_retrieval.md
context_package.md
Search Log
metadata_index
skills/
handoff
```

These artifacts are **Project State / AI Session State**.

They are not application runtime state.

---

## Scope Boundary

This template covers workspace/project context for AI-assisted work.

It does **not** define:

- React state
- database state
- cache state
- queue state
- application workflow state
- session storage
- backend runtime state machines
- product runtime architecture

Application Runtime State belongs in Architecture documents and Yang Core Modules.

Project / AI Session State belongs in the external workspace context layer and supports AI agents across sessions.

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

Do not merge all jobs into one overloaded file.

A single overloaded file becomes noisy, repetitive, expensive, and unreliable. It eventually recreates the same problem as a long, stale chat: too much history, too little signal.

---

## Template Body

Copy only the artifact sections you need.

---

# 1. `plan.md` Template

Use `plan.md` as the active task focus.

It answers:

```text
What is being worked on right now?
```

`plan.md` should be short, current, and actionable.

It is not a roadmap, backlog, changelog, debug diary, or permanent memory file.

```markdown
---
id: "[project-or-workspace].plan"
title: "Plan"
document_type: "Workspace State"
document_role: "Current Task Focus"
layer: "Workspace Context"
status: "Active"
version: "0.1.0"
metadata_version: "1.0.0"
created: "[YYYY-MM-DD]"
updated: "[YYYY-MM-DD]"
language: "English"
technical_identifiers_language: "English"
tags:
  - plan
  - current-task
  - workspace-context
summary: "[One sentence describing the current task focus.]"
retrieval_description: "Retrieve this file at the start of a focused AI work session to understand the active task, scope, constraints, inputs, and acceptance criteria."
scope:
  project: "[project-name]"
  product: ""
  module_id: ""
  submodule_id: ""
  feature_id: ""
retrieval:
  retrieval_ready: true
  retrieval_priority: "[primary | normal | supporting | low | exclude]"
  excluded_from_retrieval: false
validation:
  metadata_inferred: false
  uncertain_fields: []
  missing_context: []
  needs_human_review: false
---

# Plan

_Last updated: YYYY-MM-DD_

## Current Task

[One sentence describing what is being built, changed, fixed, reviewed, or documented.]

## Module / Area

[Which module, file, page, component, system, workflow, or document this task affects.]

## Goal

[What done looks like. Be specific and testable.]

## In Scope

- [In-scope item]
- [In-scope item]
- [In-scope item]

## Out of Scope

- [Out-of-scope item]
- [Out-of-scope item]
- [Out-of-scope item]

## Constraints

- [Constraint]
- [Constraint]
- [Constraint]

## Required Inputs / Dependencies

[Relevant files, documents, contracts, modules, APIs, screenshots, logs, or previous decisions.]

- [Input or dependency]
- [Input or dependency]

## Expected Output

[What files, functions, behavior, documentation, handoff, or review result should exist when the task is complete.]

## Acceptance Criteria

- [ ] [Criterion]
- [ ] [Criterion]
- [ ] [Criterion]

## Notes / Cautions

[Known pitfalls, prior decisions, relevant warnings, or scope cautions.]
```

---

# 2. `memory.md` Template

Use `memory.md` as persistent confirmed project and architecture memory.

It answers:

```text
What is currently true and intentionally kept?
```

`memory.md` is not an append-only changelog, transcript, scratchpad, backlog, roadmap, or failed-attempt diary.

Only store confirmed current truth.

```markdown
---
id: "[project-or-workspace].memory"
title: "Memory"
document_type: "Workspace State"
document_role: "Confirmed Project Memory"
layer: "Workspace Context"
status: "Active"
version: "0.1.0"
metadata_version: "1.0.0"
created: "[YYYY-MM-DD]"
updated: "[YYYY-MM-DD]"
language: "English"
technical_identifiers_language: "English"
tags:
  - memory
  - confirmed-state
  - workspace-context
summary: "[One sentence describing what this memory file preserves.]"
retrieval_description: "Retrieve relevant sections of this file when an AI agent needs confirmed current project state, architecture decisions, active contracts, resolved implementation facts, or still-relevant lessons from prior work."
scope:
  project: "[project-name]"
  product: ""
retrieval:
  retrieval_ready: true
  retrieval_priority: "[primary | normal | supporting | low | exclude]"
  excluded_from_retrieval: false
maintenance:
  last_cleanup: ""
  entries_since_cleanup: 0
  compression_status: "[not-needed | recommended | required | completed]"
  rounds_since_compression: 0
validation:
  metadata_inferred: false
  uncertain_fields: []
  missing_context: []
  needs_human_review: false
---

# Memory

_Last updated: YYYY-MM-DD_  
_Last cleanup: YYYY-MM-DD or Not yet cleaned_  
_Compression status: not-needed / recommended / required / completed_

---

## Current Project Baseline

[Short summary of the current confirmed project state.]

---

## [Module / Category / Feature Name]

### Current State

[Describe what currently exists and how it behaves.]

### Confirmed Change: [Short title]

**Date:** YYYY-MM-DD  
**Status:** Confirmed

**Before:**  
[What existed before, only if the contrast is still useful.]

**After:**  
[What exists now and how it behaves.]

**Why:**  
[One or two sentences explaining the reason for the decision.]

**Contracts / Interfaces affected:**  
[Function signatures, API endpoints, event formats, data shapes, module contracts, or documentation contracts affected.]

**Dependencies:**  
[What this change relies on, or what relies on this change.]

**Relevant files or documents:**  
[Important file paths, Yin/Yang documents, specs, references, or context packages.]

**Still-relevant lessons / avoid repeating:**  
[Only include failed attempts or cautions if they are still necessary to prevent repeated waste or regression.]

---

## Cleanup Notes

[Notes for the next Workspace State Maintenance run.]

- [ ] Remove superseded entries.
- [ ] Merge duplicate module entries.
- [ ] Compress long history into current truth.
- [ ] Keep still-relevant "avoid repeating" notes only while useful.
```

---

# 3. `context_retrieval.md` Template

Use `context_retrieval.md` as the reusable deterministic retrieval method for a workspace.

It answers:

```text
How should agents find the right context without guessing?
```

This file is procedure, not memory.

```markdown
---
id: "[project-or-workspace].context-retrieval"
title: "Context Retrieval"
document_type: "Workspace Context"
document_role: "Deterministic Retrieval Procedure"
layer: "Workspace Context"
status: "Active"
version: "0.1.0"
metadata_version: "1.0.0"
created: "[YYYY-MM-DD]"
updated: "[YYYY-MM-DD]"
language: "English"
technical_identifiers_language: "English"
tags:
  - context-retrieval
  - deterministic-retrieval
  - workspace-context
  - metadata
summary: "[One sentence describing the retrieval method for this workspace.]"
retrieval_description: "Retrieve this file before searching project documents, selecting context for an AI task, building a context package, or creating a Search Log."
scope:
  project: "[project-name]"
  product: ""
retrieval:
  retrieval_ready: true
  retrieval_priority: "[primary | normal | supporting | low | exclude]"
  excluded_from_retrieval: false
validation:
  metadata_inferred: false
  uncertain_fields: []
  missing_context: []
  needs_human_review: false
---

# Context Retrieval

## Purpose

This file defines how to retrieve relevant context for this workspace using explicit metadata, IDs, tags, document types, layers, modules, submodules, relationships, and source links.

Use deterministic metadata first.

Use semantic search only as a helper.

Do not treat semantic similarity as source of truth for document relationships.

---

## Retrieval Roots

| Root | Purpose | Notes |
|---|---|---|
| `[docs/]` | Source documentation | [Notes] |
| `[templates/]` | Templates | [Notes] |
| `[context/]` | Workspace context | [Notes] |
| `[examples/]` | Filled examples | [Notes] |
| `[src/]` | Source code, if relevant | [Notes] |

---

## Required Metadata Fields

Relevant documents should be filtered by:

- `id`
- `title`
- `document_type`
- `document_role`
- `layer`
- `status`
- `tags`
- `aliases`
- `scope.module_id`
- `scope.submodule_id`
- `scope.feature_id`
- `yin_yang.paired_yin`
- `yin_yang.paired_yang`
- `retrieval.retrieval_priority`
- `source.source_documents`
- `source.source_blocks`

---

## Retrieval Order

1. Read the current task or user query.
2. Identify explicit keys:
   - module ID
   - submodule ID
   - feature ID
   - layer
   - document type
   - tags
   - file path
   - artifact type
3. Check `plan.md` if the task depends on current task state.
4. Check metadata index if available.
5. Retrieve directly matching documents by metadata.
6. Retrieve paired Yin/Yang documents where relevant.
7. Retrieve parent or child context if needed.
8. Retrieve relevant `memory.md` excerpts only if confirmed project state matters.
9. Retrieve relevant skills only if a reusable procedure or lesson applies.
10. Produce a Search Log.
11. Produce a context package when the task needs handoff-ready selected context.

---

## Retrieval Depth

| Depth | Use when | Includes |
|---|---|---|
| `minimal` | Small narrow task | Direct matching docs only |
| `standard` | Normal AI work | Matching docs + paired Yin/Yang + relevant memory |
| `deep` | Review, triage, architecture, risky change | Standard + parents/children + related docs + Search Log |
| `source_pack` | Documentation or audit work | Selected sources + excerpts + source traceability |

---

## Exclusion Rules

Exclude:

- deprecated documents unless the task asks for history
- superseded documents unless needed for comparison
- unrelated examples
- old drafts with conflicting terminology
- files containing secrets
- unverified generated content unless marked as such

---

## Search Log Requirement

Every non-trivial retrieval run should produce or update a Search Log.

The Search Log records:

- retrieval goal
- search inputs
- derived retrieval keys
- searches performed
- sources selected
- sources excluded
- relevant findings
- uncertainty
- confidence
- notes for context package or handoff

---

## Context Package Rule

Create a context package when selected context must be handed to another agent, reviewer, or implementation session.

A context package is temporary task context.

It is not `memory.md`.

Confirmed lasting facts should be moved into `memory.md` through the state workflow.

---

## Open Questions

- [Question]
```

---

# 4. `context_package.md` Template

Use a context package as temporary task-specific context.

It answers:

```text
What selected context should this agent use for this task?
```

```markdown
---
id: ""
title: "Context Package — [Task / Topic]"
document_type: "Context Package"
document_role: "Temporary Task Context"
layer: "Workspace Context"
status: "Active"
version: "0.1.0"
metadata_version: "1.0.0"
created: ""
updated: ""
language: "English"
technical_identifiers_language: "English"
tags:
  - context-package
  - workspace-context
retrieval_description: "[When should this context package be used?]"
source:
  generated_from: ""
  source_document_id: ""
  search_log: ""
validation:
  metadata_inferred: false
  uncertain_fields: []
  missing_context: []
  needs_human_review: false
---

# Context Package — [Task / Topic]

## Purpose

[Explain why this context package exists and which task it supports.]

## Target Audience

[Human / Agent 2 / reviewer / documentation agent / custom.]

## Intended Use

[Explain how the receiver should use this package.]

## Task

[Describe the specific task.]

## Scope Boundaries

### In Scope

- [Item]

### Out of Scope

- [Item]

## Selected Sources

| Source | Type | Status | Why included |
|---|---|---|---|
| [Source] | [Type] | [Current / Draft / Stable / Deprecated] | [Reason] |

## Relevant Context Summary

[Summarize selected context. Keep this compact and task-specific.]

## Direct Excerpts

Use direct excerpts only when necessary.

### Source: [Name]

```text
[Excerpt]
```

## Memory Excerpts

Include only relevant `memory.md` excerpts when needed.

```text
[Relevant memory excerpt]
```

## Skills Used

List any selected skills from `skills_index.md` or `context/skills/`.

| Skill | Why relevant |
|---|---|
| [Skill] | [Reason] |

## Search Log

[Paste or link the Search Log for this context package.]

## Exclusions

| Excluded source | Reason |
|---|---|
| [Source] | [Reason] |

## Assumptions

- [Assumption]

## Open Questions

- [Question]

## Confidence

[High / Medium / Low / Unknown]

## Handoff Notes

[Instructions for the next agent/human.]

## Rules

- This package is temporary task context.
- This package is not `memory.md`.
- This package is not `context_retrieval.md`.
- This package must not include secrets.
- Confirmed lasting facts should be moved to `memory.md` through the state workflow.
```

---

# 5. Search Log Template

Use a Search Log as the retrieval audit trail.

It answers:

```text
What was searched, selected, excluded, and why?
```

```markdown
---
id: ""
title: "Search Log — [Task / Query]"
document_type: "Search Log"
document_role: "Retrieval Audit Trail"
layer: "Workspace Context"
status: "Active"
version: "0.1.0"
metadata_version: "1.0.0"
created: ""
updated: ""
language: "English"
technical_identifiers_language: "English"
tags:
  - search-log
  - retrieval
  - workspace-context
retrieval_description: "[When should this Search Log be retrieved?]"
---

# Search Log — [Task / Query]

## Retrieval Goal

[What context was needed and why?]

## Requested Output Mode

[summary / deep_brief / agent_context_package / patch_handoff_context / document_source_pack / review_context / custom]

## Retrieval Initialization Check

| Check | Result |
|---|---|
| `context_retrieval.md` available | YES / NO / UNKNOWN |
| Metadata/frontmatter conventions available | YES / NO / UNKNOWN |
| Metadata-tagged documents available | YES / NO / UNKNOWN |
| Metadata index available | YES / NO / UNKNOWN / not used |
| Docs root available | YES / NO / UNKNOWN |
| Context root available | YES / NO / UNKNOWN |
| `memory.md` requested/available | YES / NO / not requested |
| Skills index requested/available | YES / NO / not requested |

## Search Inputs

- Topic:
- User query:
- Known module_id:
- Known submodule_id:
- Known layer:
- Known document_type:
- Known tags:
- Known aliases:
- Known folders:

## Derived Retrieval Keys

Derived keys are not confirmed truth.

| Key | Value | Confidence |
|---|---|---|
| topic |  |  |
| possible_module_ids |  |  |
| possible_submodule_ids |  |  |
| likely_layers |  |  |
| likely_document_types |  |  |
| derived_tags |  |  |
| aliases |  |  |
| likely_folders |  |  |

## Retrieval Signals Used

- [Signal]

## Searches Performed

| Step | Search / Filter | Result |
|---|---|---|
| 1 | [Search/filter] | [Result] |

## Sources Selected

| Source | Type | Status | Why selected |
|---|---|---|---|
| [Source] | [Type] | [Status] | [Reason] |

## Sources Excluded

| Source | Reason |
|---|---|
| [Source] | [Reason] |

## Relevant Findings

- [Finding]

## Uncertainty

- [Uncertainty]

## Confidence

[High / Medium / Low / Unknown]

## Open Questions

- [Question]

## Notes for Context Package / Handoff

[Notes.]

## Rules

- Search Log is not memory.
- Search Log is not a context package by itself.
- Confirmed lasting facts belong in `memory.md`.
- Do not include secrets.
- Do not pretend deterministic retrieval was available if initialization was missing.
```

---

# 6. Metadata Index Template

Use a metadata index as an optional generated lookup helper.

It answers:

```text
Which documents exist and what metadata identifies them?
```

The metadata index is not source of truth.

Source documents and their frontmatter remain source of truth.

```markdown
---
id: ""
title: "Metadata Index"
document_type: "Metadata Index"
document_role: "Generated Lookup Index"
layer: "Workspace Context"
status: "Generated"
version: "0.1.0"
metadata_version: "1.0.0"
created: ""
updated: ""
language: "English"
technical_identifiers_language: "English"
tags:
  - metadata-index
  - retrieval
  - workspace-context
retrieval_description: "Generated lookup index derived from document frontmatter."
source:
  generated_from: "document frontmatter"
validation:
  metadata_inferred: false
  uncertain_fields: []
  missing_context: []
  needs_human_review: false
---

# Metadata Index

## Status

This file is a generated lookup helper.

It is not the source of truth.

Source documents and their frontmatter remain the source of truth.

## Index Metadata

```yaml
index_version: "0.1.0"
generated_at: ""
generated_by: ""
source_roots: []
documents_indexed: 0
documents_excluded: 0
```

## Indexed Documents

| ID | Path | Title | Type | Layer | Status | Module | Submodule | Tags | Retrieval Priority |
|---|---|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |  |  |

## Paired Yin/Yang Documents

| Yin | Yang | Module | Submodule | Status |
|---|---|---|---|---|
|  |  |  |  |  |

## Excluded Documents

| Path / ID | Reason |
|---|---|
|  |  |

## Missing / Incomplete Metadata

| Path / ID | Missing fields | Notes |
|---|---|---|
|  |  |  |

## JSON Shape

If generating JSON instead of Markdown, use this shape:

```json
[
  {
    "id": "",
    "path": "",
    "title": "",
    "document_type": "",
    "document_role": "",
    "layer": "",
    "status": "",
    "version": "",
    "updated": "",
    "tags": [],
    "aliases": [],
    "module_id": "",
    "submodule_id": "",
    "parent": "",
    "children": [],
    "paired_yin": "",
    "paired_yang": "",
    "related": [],
    "references": [],
    "retrieval_description": "",
    "retrieval_ready": true,
    "retrieval_priority": ""
  }
]
```

## Rules

- Generate this index from document frontmatter.
- Do not manually invent index truth.
- Do not let this file silently diverge from source documents.
- Rebuild the index when source frontmatter changes.
```

---

# 7. Skills Index Template

Use `skills_index.md` only when the workspace uses reusable helper rules, local procedures, search helpers, snippets, or lessons for AI agents.

Skills are not memory.

Skills are stable reusable helpers.

```markdown
---
id: "[project-or-workspace].skills-index"
title: "Skills Index"
document_type: "Workspace Context"
document_role: "Skills Index"
layer: "Workspace Context"
status: "Active"
version: "0.1.0"
metadata_version: "1.0.0"
created: ""
updated: ""
language: "English"
technical_identifiers_language: "English"
tags:
  - skills
  - skills-index
  - workspace-context
retrieval_description: "Retrieve this index when selecting reusable agent helper rules, local procedures, troubleshooting lessons, search helpers, snippets, or stable implementation cautions."
validation:
  metadata_inferred: false
  uncertain_fields: []
  missing_context: []
  needs_human_review: false
---

# Skills Index

## Purpose

This index lists reusable skills available to AI agents in this workspace.

Skills are not memory.

Skills store reusable objective helper rules, local procedures, search helpers, snippets, and still-useful lessons.

## Skills

| Skill ID | Title | Category | When to use | Source |
|---|---|---|---|---|
| `[skill-id]` | [Title] | [Category] | [When this applies] | [Source or reason] |

## Maintenance Rules

- Remove duplicate skills.
- Merge overlapping skills.
- Delete stale skills.
- Keep skills objective and reusable.
- Do not store project truth here; use `memory.md`.
- Do not store secrets.
```

---

# 8. Handoff Template

Use a handoff when one agent must execute one scoped task.

It answers:

```text
What exactly should the next agent do?
```

```markdown
---
id: ""
title: "Handoff — [Task]"
document_type: "Handoff"
document_role: "Scoped Execution Context"
layer: "Workspace Context"
status: "Active"
version: "0.1.0"
metadata_version: "1.0.0"
created: ""
updated: ""
language: "English"
technical_identifiers_language: "English"
tags:
  - handoff
  - agent-context
  - workspace-context
retrieval_description: "Retrieve this handoff when executing or reviewing the scoped task it defines."
source:
  context_package: ""
  search_log: ""
  plan: ""
  memory_excerpt: ""
validation:
  metadata_inferred: false
  uncertain_fields: []
  missing_context: []
  needs_human_review: false
---

# Handoff — [Task]

## Receiver

[Agent 2 / reviewer / implementation agent / documentation agent / custom.]

## Goal

[One sentence describing the task.]

## Context Summary

[Only the context required for this task.]

## In Scope

- [Item]

## Out of Scope

- [Item]

## Required Inputs

- [File/document/context]
- [File/document/context]

## Allowed Files / Areas

- `[path-or-area]`

## Forbidden Changes

- [Forbidden change]
- [Forbidden change]

## Implementation / Work Rules

- [Rule]
- [Rule]
- [Rule]

## Verification

- [ ] [Check]
- [ ] [Check]
- [ ] [Check]

## Expected Output

[Patch, report, document, review, summary, etc.]

## Open Questions

- [Question]

## Final Reporting Requirements

[What the agent should report after completion.]
```

---

# 9. Maintenance and Compression Rules

## When to Compress `memory.md`

| Situation | Action |
|---|---|
| Around 10 confirmed entries for one area | Compression recommended |
| Around 20 confirmed entries for one area | Compression required |
| Repeated entries describe the same module | Merge into one authoritative current-state entry |
| Old before/after states are no longer useful | Remove superseded history |
| The file becomes too long to inject safely | Compress before the next AI session |

## What to Preserve During Compression

- current module behavior
- active contracts and interfaces
- current data shapes or event formats
- current architectural decisions
- active dependencies
- unresolved constraints that still affect implementation
- relevant links to Yin/Yang documents
- still-useful notes about ineffective fixes, only while the issue remains relevant

## What to Remove During Compression

- reverted attempts
- temporary debug notes
- abandoned alternatives
- duplicate history
- stale assumptions
- superseded architecture
- old before-states that no longer explain current behavior
- chat transcript residue
- secrets or sensitive values

## Compression Prompt

```text
You are compressing a memory file for an AI-assisted development project.

The goal is to reduce token length while preserving all information an AI agent needs to understand the current confirmed state of the project.

Rules:
- Keep final confirmed architecture for every module.
- Keep current behavior and active contracts.
- Keep active dependencies.
- Keep decisions that explain why the current architecture exists.
- Keep unresolved known constraints if they are still active.
- Keep still-useful "avoid repeating" notes only while they prevent repeated failed work.
- Discard failed attempts that were reverted.
- Discard temporary debug notes.
- Discard abandoned alternatives.
- Discard superseded before-states unless the contrast is still needed.
- Merge duplicate entries for the same module into one authoritative current-state entry.
- Preserve before/after structure only where the contrast still matters.
- Do not invent, infer, or add information not present in the source.
- Do not include secrets.

Here is the current memory.md:

[PASTE FULL memory.md CONTENT HERE]

Return the compressed version only. No explanation.
```

---

# 10. Quality Checklist

Before using these state/context artifacts, verify:

- [ ] `plan.md` contains only the current active task.
- [ ] `memory.md` contains only confirmed current truth and useful still-relevant lessons.
- [ ] `context_retrieval.md` explains how deterministic retrieval works in the workspace.
- [ ] Context packages are temporary task context, not memory.
- [ ] Search Logs record what was searched, selected, excluded, and why.
- [ ] Metadata indexes are generated from source frontmatter, not invented manually.
- [ ] Skills are reusable helper rules, not project memory.
- [ ] Handoffs are scoped to one execution task.
- [ ] No artifact contains real secrets, tokens, passwords, private keys, or sensitive operational values.
- [ ] Confirmed lasting facts discovered during work are moved into `memory.md` through the state workflow.
- [ ] Stale, duplicated, or noisy state is compressed before it pollutes future AI sessions.
