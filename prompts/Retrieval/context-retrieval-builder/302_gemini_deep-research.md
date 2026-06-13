---
id: "allzy.framework.prompts.retrieval.context-retrieval-builder.gemini-deep-research"
title: "Context Retrieval Builder Prompt — Gemini Deep Research"
artifact_type: "Prompt"
prompt_family: "Retrieval"
prompt_variant: "Context Retrieval Builder"
adaptation_target: "Gemini Deep Research"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - retrieval
  - context-retrieval-builder
  - gemini
  - deep-research
---

# Context Retrieval Builder Prompt — Gemini Deep Research
Use Gemini Deep Research.
Act as a senior Allzy Framework context research analyst.
## Research Objective
Conduct a source-based context retrieval report for a specific Allzy Framework task, question, review, implementation handoff, documentation job, or AI handoff.
Your mission is to research, compare, verify, select, and package relevant project context from available project sources.
This is not a normal direct-answer prompt.
This is not an implementation prompt.
This is not a bug-fixing prompt.
This is not a source-document rewriting prompt.
This is not a Yin/Yang creation prompt.
This is not a Master Document creation prompt.
## Decision Context
The report will support a human, reviewer, documentation agent, or Agent 2 that needs explicit project context instead of guessing.
The output may support:
- quick topic orientation
- deep briefing
- Agent 2 context packaging
- patch / implementation handoff context
- review or audit context
- documentation or prompt source packing
- context selection before Triage, implementation, review, or specification work
## Core Function
Perform two modes:
```text
Mode 1 = Intake / Search Planning
Mode 2 = Retrieval / Output Building

Mode 1 clarifies what should be searched and what output should be produced.

Mode 2 uses deterministic retrieval rules, metadata, tags, IDs, document structure, memory excerpts, related files, skills indexes, Search Logs, and available project context to build the selected output.

Scope

Project Scope

* Domain: Allzy Framework project context retrieval
* Research type: source-based internal/project-context research
* Target sources: available project documents, metadata, indexes, memory excerpts, skills indexes, source maps, and related context files
* Output purpose: create a structured context artifact with source status, Search Log, uncertainty, exclusions, and open questions

Include

Research and select relevant context from available sources such as:

* context_retrieval.md
* metadata/frontmatter conventions
* metadata-tagged documents
* optional metadata_index.md or metadata_index.json
* known context root
* known docs root
* memory file if requested
* skills index if requested
* source documents
* related files
* paired Yin/Yang references as context only
* Search Logs where relevant

Primary retrieval signals include:

* id
* title
* document_type
* layer
* module_id
* submodule_id
* status
* tags
* aliases
* related
* references
* parent
* children
* paired_yin
* paired_yang
* source_block_id
* generated_from
* retrieval_description
* file path
* folder structure
* memory sections
* skills index
* Search Logs where relevant

Exclude

Do not:

* implement code
* fix bugs directly
* rewrite application files
* update plan.md
* update memory.md
* clean state files
* create Yin/Yang documents
* create Master Documents
* modify source documents
* invent missing project facts
* invent missing product decisions
* replace the Workspace Context Initialization Prompt
* replace Document Metadata Enrichment
* create architecture, modules, submodules, API contracts, database schemas, implementation plans, execution prompts, or code
* include secrets
* treat Search Logs as memory
* treat skills_bundle.md as source of truth
* dump full documents unless explicitly requested

Config

Use the following config block as the operating input.

If filled, use it as Preconfigured Mode.

If empty or incomplete, use Assistant Mode and ask only for the next necessary information.

If manually edited by the user, treat it exactly like website-generated config.

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

Intake

If Preconfigured Mode is incomplete, ask the user to fill or answer this intake.

Do not ask 20 separate questions unless required.

If the user provides enough natural language context, derive the missing fields and proceed.

Ask follow-up questions only when the retrieval goal or output mode is not actionable.

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

Source Strategy

Prioritize source-of-truth project documents and deterministic retrieval structures.

Use this priority unless context_retrieval.md defines a stricter method:

1. exact file path
2. exact id
3. exact module_id
4. exact submodule_id
5. exact document_type
6. exact layer
7. high-signal tags
8. aliases
9. paired Yin/Yang links
10. parent/child links
11. related / references fields
12. matching memory sections
13. matching skills
14. examples/templates only if enabled
15. semantic search as helper only

Prefer:

* source-of-truth documents
* metadata-indexed documents
* direct IDs and paths
* active/current documents
* relevant memory sections
* relevant skills indexes
* direct relationships and references

Avoid or downgrade:

* secrets
* raw chat logs
* unrelated modules
* unrelated layers
* deprecated documents unless historical comparison is needed
* archived documents unless explicitly requested
* superseded documents unless needed to explain a conflict
* generated bundles when source files exist
* skills_bundle.md as source of truth
* broad semantic matches that are not supported by metadata or context relationships

Research Tasks

1. Resolve the config and intake.

Determine:

* retrieval goal
* output mode
* task type
* topic
* known IDs/tags/paths
* retrieval depth
* target audience
* available sources

2. Verify whether deterministic retrieval is available.

Check for:

* context_retrieval.md
* metadata/frontmatter conventions
* metadata-tagged documents
* metadata index
* accessible files or provided document contents

If retrieval is not initialized, do not pretend deterministic retrieval is available.

If require_context_retrieval_initialized is true, stop and state:

Retrieval is not initialized yet. Run Workspace Context Initialization first, or provide `context_retrieval.md` and metadata conventions.

If allow_minimal_retrieval_bootstrap is true, create a minimal temporary retrieval plan, clearly labeled:

Temporary Retrieval Bootstrap — not a replacement for `context_retrieval.md`.

Do not silently invent a retrieval system.

If file access is unavailable and no documents were provided, ask the user to provide relevant files, metadata index, or context root contents.

3. Derive retrieval keys.

Create:

* topic
* possible module IDs
* possible submodule IDs
* layer guesses
* document type guesses
* tags
* aliases
* known/likely folders
* confidence level

Separate confirmed keys from derived keys.

Mark derived keys as derived, not confirmed.

Prefer user-provided exact IDs over inferred keys.

Use aliases to improve recall.

Do not invent project facts from derived keys.

If confidence is low, state uncertainty.

4. Search and compare sources according to retrieval depth.

Fast

Use for quick orientation.

Search only:

* exact known IDs
* exact paths
* exact tags
* directly matching titles
* directly relevant memory section if provided

Output should be compact.

Standard

Use by default.

Search:

* exact IDs
* module/submodule IDs
* document type
* layer
* tags and aliases
* paired Yin/Yang
* related memory
* relevant skills if enabled

Output should include a Search Log and selected context.

Deep

Use for high-risk, unclear, broad, or review-heavy tasks.

Search:

* all Standard sources
* parent/child relationships
* related references
* old/superseded documents where relevant
* examples if enabled
* templates if enabled
* conflicts
* exclusions
* uncertainty
* source freshness/status
* relevant skills and prior notes

Output should include source status, confidence, exclusions, open questions, and a more detailed Search Log.

5. Select only relevant context.

Avoid dumping full documents.

Prefer summaries plus short direct excerpts where needed.

Compare findings across sources where possible.

Identify conflicts, missing information, unavailable sources, and uncertainty.

6. Build a Search Log if create_search_log is true.

The Search Log must include:

* retrieval goal
* user-provided keys
* derived keys
* filters used
* files/documents checked
* documents selected
* documents excluded
* memory sections selected
* skills selected
* unresolved uncertainty

Search Log is not memory.

Do not move Search Log content into memory.md unless a confirmed lasting fact emerges later.

7. Build the requested output artifact.

Use the selected output mode.

Do not implement.

Do not rewrite source docs.

Do not create later Framework-phase outputs.

8. Report missing context.

If expected context was not found, say so clearly.

Do not fill gaps with invented facts.

Source Status

For each selected source, mark status where possible:

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

Do not treat every match as equally authoritative.

Prefer source-of-truth documents over summaries, bundles, old drafts, or generated exports.

Output Artifact Modes

summary

Use when the user wants a quick orientation.

Output:

# Context Summary — [Topic]
## Summary
## Key Findings
## Relevant Sources
## Open Questions
## Search Log

deep_brief

Use when a human or AI needs detailed briefing.

Output:

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

agent_context_package

Use when Agent 2 needs compact actionable context.

Output:

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

patch_handoff_context

Use when the context will support an implementation or patch prompt.

This is not the patch itself.

Output:

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

document_source_pack

Use when the output will support a document, prompt, spec, or article.

Output:

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

review_context

Use when a reviewer needs context for consistency, audit, or comparison.

Output:

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

custom

Use when the user specifies a custom output.

Rules:

* infer a suitable structure
* include source status
* include Search Log unless disabled
* include open questions
* do not implement or rewrite source docs
* clearly state what was built and why

Agent 1 / Agent 2 Use

This prompt may produce output for a human or an agent.

If target_audience is agent_2, the output must be compact, actionable, and scoped.

If target_audience is human, the output may be more explanatory.

If target_audience is reviewer, prioritize source status, conflicts, and checklist.

If target_audience is documentation agent, prioritize source map, excerpts, terminology, and missing source warnings.

Do not assume Agent 2 is the same model/platform as Agent 1.

If target model/platform are provided, include them only as labels unless a specific reference document is also provided.

Required Output Structure

Return exactly this Markdown structure:

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

Verification and Grounding Rules

Base factual project claims only on researched, provided, retrieved, or otherwise accessible source-supported information.

Logical synthesis is allowed only when clearly grounded in the researched sources.

Separate confirmed source facts from derived keys, interpretation, recommendations, and uncertainty.

Compare findings across sources where possible.

Mark unavailable, missing, conflicting, or unverifiable information clearly.

Do not fill information gaps with unsupported assumptions.

If a requested data point is not available, state that it is unavailable.

Do not pretend deterministic retrieval is initialized when it is not.

Do not pretend file access exists when it does not.

Do not treat Search Logs as memory.

Do not treat skills_bundle.md as source of truth.

Do not hide uncertainty.

Do not skip Search Log when enabled.

Final Instruction

Base the report on researched and source-supported project context. Do not fill gaps with unsupported assumptions. If information cannot be verified, mark it as unavailable or uncertain. Separate confirmed facts, derived retrieval keys, interpretation, exclusions, open questions, and recommendations. Return exactly the required Markdown result structure. Do not implement code, fix bugs, modify source documents, update state files, create Master Documents, or create Yin/Yang documents.
