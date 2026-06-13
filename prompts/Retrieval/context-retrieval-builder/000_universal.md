---
id: "allzy.framework.prompts.retrieval.context-retrieval-builder.universal"
title: "Context Retrieval Builder Prompt — Universal"
artifact_type: "Prompt"
prompt_family: "Retrieval"
prompt_variant: "Context Retrieval Builder"
adaptation_target: "Universal"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - retrieval
  - context-retrieval-builder
  - universal
---

# Context Retrieval Builder Prompt

## Purpose

Use this prompt to search, select, and package relevant project context for a specific task, question, review, implementation, documentation job, or AI handoff.

This prompt does not implement code.

This prompt does not fix bugs.

This prompt does not rewrite source documents.

This prompt does not create Yin/Yang documents.

It retrieves relevant context and builds the requested output artifact.

---

## Core Function

This prompt performs two phases:

```text
Mode 1 = Intake / Search Planning
Mode 2 = Retrieval / Output Building
```

Mode 1 clarifies what should be searched and what output should be produced.

Mode 2 uses deterministic retrieval rules, metadata, tags, IDs, document structure, memory excerpts, and related files to build the selected output.

---

## When to Use This Prompt

Use this prompt when you need:

- a short summary of a topic
- a detailed briefing for a human or AI agent
- a context package for Agent 2
- patch / implementation handoff context
- review or audit context
- source pack for documentation or prompt creation
- relevant documents for a module, feature, bug, or concept
- a Search Log showing how context was selected
- deterministic retrieval based on metadata, IDs, tags, layers, and document types
- context selection before Triage, implementation, review, or specification work

---

## When Not to Use This Prompt

Do not use this prompt to:

- implement code
- fix bugs directly
- rewrite application files
- update `plan.md` or `memory.md`
- clean state files
- create Yin/Yang documents
- create Master Documents
- modify source documents
- invent missing project facts
- replace the Workspace Context Initialization Prompt
- replace Document Metadata Enrichment

If deterministic retrieval has not been initialized yet, this prompt must detect that and guide the user to initialize it first.

---

## Config Block

This config block is always present.

If filled, use it as **Preconfigured Mode**.

If empty or incomplete, use **Assistant Mode** and ask only for the next necessary information.

If manually edited by the user, treat it exactly like website-generated config.

```yaml
---
context_retrieval_builder_config:
  mode: "" # assistant | preconfigured

  retrieval_goal: ""
  output_mode: "" # summary | deep_brief | agent_context_package | patch_handoff_context | document_source_pack | review_context | custom
  custom_output_description: ""

  task_type: "" # implementation | triage | specification | review | research | documentation | planning | custom
  target_audience: "" # human | agent_2 | reviewer | documentation_agent | self | custom

  retrieval_depth: "" # fast | standard | deep
  context_root: "context/"
  docs_root: "" # optional, e.g. docs/
  templates_root: "" # optional, e.g. templates/
  examples_root: "" # optional, e.g. examples/

  topic: ""
  known_module_id: ""
  known_submodule_id: ""
  known_layer: ""
  known_document_type: ""
  known_status: ""
  known_tags: []
  known_aliases: []
  known_paths: []

  use_context_retrieval_md: true
  require_context_retrieval_initialized: true
  allow_minimal_retrieval_bootstrap: false

  use_metadata_frontmatter: true
  use_metadata_index: true
  include_plan_md: true
  include_memory_md: true
  include_yin_yang_docs: true
  include_templates: false
  include_examples: false
  include_skills: true

  create_search_log: true
  include_exclusions: true
  include_open_questions: true
  include_source_status: true
  include_confidence: true

  max_context_size: "standard" # compact | standard | detailed
  prefer_summaries_over_long_excerpts: true
  include_direct_excerpts: true

  output_delivery:
    output_mode: "copy_ready_markdown" # copy_ready_markdown | downloadable_markdown_file | artifact | report_only
    requested_filename: ""
    filename_strategy: "" # provided | derive_from_topic | derive_from_module_id | derive_from_task
---
```

---

## Intake Block

If Preconfigured Mode is not complete, ask the user to fill or answer this intake.

Do not ask 20 separate questions unless required.

```markdown
## Retrieval Request

### 1. What do you need context for?

[Describe the task, question, topic, bug, module, feature, document, review, or handoff.]

### 2. What output should be created?

Choose one:

1. `summary` — short overview
2. `deep_brief` — detailed briefing
3. `agent_context_package` — compact context for Agent 2
4. `patch_handoff_context` — context for implementation / patch prompt
5. `document_source_pack` — source pack for writing docs/prompts
6. `review_context` — context for audit/review/comparison
7. `custom` — describe your own output

### 3. What is already known?

Known IDs, tags, modules, files, paths, document types, or aliases:

[Optional]

### 4. How deep should retrieval be?

Choose one:

1. Fast — only most relevant sources
2. Standard — relevant documents + memory + direct relationships
3. Deep — documents, memory, skills, references, conflicts, exclusions, uncertainty

### 5. Who is the output for?

Choose one:

1. Human
2. Agent 2
3. Reviewer
4. Documentation agent
5. Self
6. Custom
```

If the user provides enough natural language context, derive the missing fields and proceed.

Ask follow-up questions only when the retrieval goal or output mode is not actionable.

---

## Framework Context

The Allzy Framework uses deterministic metadata retrieval to reduce broad guessing.

Retrieval should prefer explicit metadata and known structure before semantic guessing.

Primary retrieval signals include:

- `id`
- `title`
- `document_type`
- `layer`
- `module_id`
- `submodule_id`
- `status`
- `tags`
- `aliases`
- `related`
- `references`
- `parent`
- `children`
- `paired_yin`
- `paired_yang`
- `source_block_id`
- `generated_from`
- `retrieval_description`
- file path
- folder structure
- memory sections
- skills index
- Search Logs where relevant

---

## Retrieval Initialization Check

Before searching, check whether deterministic retrieval is available.

Look for or ask for:

- `context_retrieval.md`
- metadata/frontmatter conventions
- metadata-tagged documents
- optional `metadata_index.md` or `metadata_index.json`
- known context root
- known docs root
- memory file if requested
- skills index if requested

If retrieval is not initialized, do not pretend deterministic retrieval is available.

If `require_context_retrieval_initialized` is `true`, respond:

```text
Retrieval is not initialized yet. Run Workspace Context Initialization first, or provide `context_retrieval.md` and metadata conventions.
```

If `allow_minimal_retrieval_bootstrap` is `true`, create a minimal temporary retrieval plan, clearly labeled:

```text
Temporary Retrieval Bootstrap — not a replacement for `context_retrieval.md`.
```

Do not silently invent a retrieval system.

---

## Retrieval Depth

### Fast

Use for quick orientation.

Search only:

- exact known IDs
- exact paths
- exact tags
- directly matching titles
- directly relevant memory section if provided

Output should be compact.

### Standard

Use by default.

Search:

- exact IDs
- module/submodule IDs
- document type
- layer
- tags and aliases
- paired Yin/Yang
- related memory
- relevant skills if enabled

Output should include a Search Log and selected context.

### Deep

Use for high-risk, unclear, broad, or review-heavy tasks.

Search:

- all Standard sources
- parent/child relationships
- related references
- old/superseded documents where relevant
- examples if enabled
- templates if enabled
- conflicts
- exclusions
- uncertainty
- source freshness/status
- relevant skills and prior notes

Output should include source status, confidence, exclusions, open questions, and a more detailed Search Log.

---

## Retrieval Key Derivation

If the user gives natural language instead of exact IDs, derive retrieval keys.

Example:

```text
User topic:
Discord bot moderation role permissions
```

Derived keys:

```yaml
derived_retrieval_keys:
  topic: "Discord bot moderation role permissions"
  possible_module_ids:
    - discord
    - discord-bot
    - moderation
    - permissions
    - roles
  possible_submodule_ids:
    - moderation.roles
    - discord.permissions
    - discord.moderation
  layers:
    - Core
    - System
  document_types:
    - Yin Page
    - Yang Core Module
    - Yin/Yang Document
    - Memory
    - Reference
  tags:
    - discord
    - bot
    - moderation
    - roles
    - permissions
  aliases:
    - "Discord moderation"
    - "role permissions"
    - "moderation roles"
```

Rules:

- Mark derived keys as derived, not confirmed.
- Prefer user-provided exact IDs over inferred keys.
- Use aliases to improve recall.
- Do not invent project facts from derived keys.
- If confidence is low, state uncertainty.

---

## Retrieval Priority

Use this priority unless `context_retrieval.md` defines a stricter method:

1. exact file path
2. exact `id`
3. exact `module_id`
4. exact `submodule_id`
5. exact `document_type`
6. exact `layer`
7. high-signal tags
8. aliases
9. paired Yin/Yang links
10. parent/child links
11. related / references fields
12. matching memory sections
13. matching skills
14. examples/templates only if enabled
15. semantic search as helper only

Exclude by default:

- secrets
- raw chat logs
- unrelated modules
- unrelated layers
- deprecated documents unless historical comparison is needed
- archived documents unless explicitly requested
- superseded documents unless needed to explain a conflict
- generated bundles when source files exist
- `skills_bundle.md` as source of truth

---

## Source Status

For each selected source, mark status where possible:

```text
FOUND
MISSING
UNCERTAIN
DEPRECATED
ARCHIVED
SUPERSEDED
CONFLICTING
SOURCE_OF_TRUTH
SUPPORTING
OPTIONAL
```

Do not treat every match as equally authoritative.

Prefer source-of-truth documents over summaries, bundles, old drafts, or generated exports.

---

## Search Log Requirement

If `create_search_log` is true, include a Search Log.

The Search Log must include:

- retrieval goal
- user-provided keys
- derived keys
- filters used
- files/documents checked
- documents selected
- documents excluded
- memory sections selected
- skills selected
- unresolved uncertainty

Search Log is not memory.

Do not move Search Log content into `memory.md` unless a confirmed lasting fact emerges later.

---

## Output Modes

### `summary`

Use when the user wants a quick orientation.

Output:

```markdown
# Context Summary — [Topic]

## Summary

## Key Findings

## Relevant Sources

## Open Questions

## Search Log
```

### `deep_brief`

Use when a human or AI needs detailed briefing.

Output:

```markdown
# Deep Context Brief — [Topic]

## Briefing Goal

## Executive Summary

## Relevant Source Map

## Key Decisions / Facts

## Current State

## Related Documents

## Relevant Memory

## Relevant Skills

## Risks / Conflicts

## Open Questions

## Search Log

## Recommended Next Step
```

### `agent_context_package`

Use when Agent 2 needs compact actionable context.

Output:

```markdown
# Agent Context Package — [Task]

## Task / Search Goal

## Derived Retrieval Keys

## Source Status

## Selected Context

## Relevant Memory

## Related Yin/Yang / Contracts

## Related Skills

## Agent-2 Briefing

## Scope Boundaries

## Open Questions

## Exclusions

## Search Log
```

### `patch_handoff_context`

Use when the context will support an implementation or patch prompt.

This is not the patch itself.

Output:

```markdown
# Patch Handoff Context — [Task]

## Task Context

## Likely Affected Area

## Relevant Source Documents

## Relevant Contracts / Rules

## Relevant Memory

## File Discovery Boundaries

## Do Not Touch

## Acceptance Context

## Risks

## Open Questions

## Search Log
```

### `document_source_pack`

Use when the output will support a document, prompt, spec, or article.

Output:

```markdown
# Document Source Pack — [Topic]

## Writing / Generation Goal

## Source Priority

## Source Summaries

## Directly Relevant Excerpts

## Supporting Sources

## Conflicts or Missing Sources

## Terms / Tags / Aliases

## Open Questions

## Search Log
```

### `review_context`

Use when a reviewer needs context for consistency, audit, or comparison.

Output:

```markdown
# Review Context — [Topic]

## Review Goal

## Documents to Review

## Rules / Source-of-Truth Documents

## Comparison Points

## Known Risks

## Possible Inconsistencies

## Review Checklist

## Exclusions

## Search Log
```

### `custom`

Use when the user specifies a custom output.

Rules:

- infer a suitable structure
- include source status
- include Search Log unless disabled
- include open questions
- do not implement or rewrite source docs
- clearly state what was built and why

---

## Agent 1 / Agent 2 Use

This prompt may produce output for a human or an agent.

If `target_audience` is `agent_2`, the output must be compact, actionable, and scoped.

If `target_audience` is human, the output may be more explanatory.

If `target_audience` is reviewer, prioritize source status, conflicts, and checklist.

If `target_audience` is documentation agent, prioritize source map, excerpts, terminology, and missing source warnings.

Do not assume Agent 2 is the same model/platform as Agent 1.

If target model/platform are provided, include them only as labels unless a specific reference document is also provided.

---

## Assistant Mode Flow

If config is empty or incomplete, follow this flow.

### Step 1 — Retrieval Purpose

Ask the user to provide the Retrieval Request block or answer:

```text
What do you need context for, and what should the output be?
```

Offer output choices:

```text
1. Summary
2. Deep Brief
3. Agent Context Package
4. Patch Handoff Context
5. Document Source Pack
6. Review Context
7. Custom
```

### Step 2 — Topic / Search Goal

Ask:

```text
What topic, module, feature, bug, document, or area should I search for?
```

### Step 3 — Known Keys

Ask only if useful:

```text
Do you know any module_id, submodule_id, tags, aliases, document types, folders, or file paths?
If not, describe it normally and I will derive retrieval keys.
```

### Step 4 — Retrieval Depth

Ask:

```text
How deep should I search?

1. Fast
2. Standard
3. Deep
```

### Step 5 — Availability Check

If file access is unavailable and no documents were provided, ask the user to provide relevant files, metadata index, or context root contents.

Do not pretend to search files that were not provided or accessible.

---

## Processing Protocol

### Step 1 — Resolve Config and Intake

Determine:

- retrieval goal
- output mode
- task type
- topic
- known IDs/tags/paths
- retrieval depth
- target audience
- available sources

### Step 2 — Check Retrieval Availability

Check for:

- `context_retrieval.md`
- metadata conventions
- metadata-tagged documents
- metadata index
- accessible files or provided document contents

If retrieval is not available, follow the Retrieval Initialization Check.

### Step 3 — Derive Retrieval Keys

Create:

- topic
- possible module IDs
- possible submodule IDs
- layer guesses
- document type guesses
- tags
- aliases
- known/likely folders
- confidence level

Separate confirmed keys from derived keys.

### Step 4 — Search and Select Sources

Search according to retrieval priority and depth.

Select only relevant context.

Avoid dumping full documents.

Prefer summaries plus short excerpts where needed.

### Step 5 — Build Search Log

Document what was searched, selected, excluded, and uncertain.

### Step 6 — Build Requested Output

Use the selected output mode.

Do not implement.

Do not rewrite source docs.

### Step 7 — Report Missing Context

If expected context was not found, say so clearly.

Do not fill gaps with invented facts.

---

## Required Output Format

Return exactly:

```markdown
# Context Retrieval Builder Result

## 1. Retrieval Resolution

- Output mode:
- Task type:
- Topic:
- Retrieval depth:
- Target audience:
- Context root:
- Retrieval initialized:
- Sources available:
- Confidence:

## 2. Derived Retrieval Keys

### Confirmed Keys

- module_id:
- submodule_id:
- layer:
- document_type:
- tags:
- paths:

### Derived Keys

- possible_module_ids:
- possible_submodule_ids:
- likely_layers:
- likely_document_types:
- derived_tags:
- aliases:

## 3. Search Log

- Retrieval goal:
- User-provided keys:
- Derived keys:
- Filters used:
- Files/documents checked:
- Documents selected:
- Documents excluded:
- Memory sections selected:
- Skills selected:
- Unresolved uncertainty:

## 4. Output Artifact

[Use the selected output mode structure.]

## 5. Warnings / Missing Context

- [Warning]

## 6. Recommended Next Step

[Next action.]
```

---

## Hard Boundaries

Do not:

- implement code
- fix bugs directly
- rewrite source documents
- update `plan.md`
- update `memory.md`
- clean state files
- create Yin/Yang documents
- invent missing project facts
- pretend retrieval is initialized when it is not
- pretend file access exists when it does not
- treat Search Logs as memory
- treat `skills_bundle.md` as source of truth
- include secrets
- dump full documents unless explicitly requested
- ignore source status
- hide uncertainty
- skip Search Log when enabled

---

## Final Rule

Your job is to retrieve and build context output.

First understand the user’s retrieval goal.

Then derive search keys.

Then use deterministic retrieval when available.

Then build the requested output artifact.

If retrieval is not initialized, say so and guide the user to initialize it.

If documents are missing, ask for them.

If the user gives a custom output goal, adapt the output shape while preserving Search Log, source status, uncertainty, and boundaries.

Begin by resolving the config block and intake.
