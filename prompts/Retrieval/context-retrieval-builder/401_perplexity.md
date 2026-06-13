---
id: "allzy.framework.prompts.retrieval.context-retrieval-builder.perplexity"
title: "Context Retrieval Builder Prompt — Perplexity"
artifact_type: "Prompt"
prompt_family: "Retrieval"
prompt_variant: "Context Retrieval Builder"
adaptation_target: "Perplexity"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - retrieval
  - context-retrieval-builder
  - perplexity
---

# Context Retrieval Builder Prompt — Perplexity Search
## API Prompt Shape
Use this prompt as a Perplexity/Sonar-style search prompt with separate `instructions` and `input`.
Do not merge search-critical details into `instructions` only.
Do not ask the model to generate URLs or source links. Source URLs must be taken from the host application's `search_results` field when needed.
---
## instructions
Provide concise, source-aware, structured answers for Allzy Framework context retrieval.
Use the retrieved or provided material to identify relevant project context, source status, missing context, uncertainty, exclusions, and next steps.
Do not speculate when search results or provided context are insufficient.
Only provide information that can be verified from available search results, provided files, accessible project context, metadata, or explicit user input.
If reliable public or provided information is not available, say so clearly.
Separate confirmed facts from derived retrieval keys, interpretation, recommendations, and uncertainty.
Do not fabricate citations, URLs, source names, document IDs, metadata, file paths, or quote spans.
Do not include source links in generated text. If links are needed, the host application must attach them from `search_results`.
Keep the final answer in Markdown.
Do not implement code.
Do not fix bugs directly.
Do not rewrite source documents.
Do not update `plan.md`.
Do not update `memory.md`.
Do not clean state files.
Do not create Yin/Yang documents.
Do not create Master Documents.
Do not modify source documents.
Do not invent missing project facts or product decisions.
Do not pretend deterministic retrieval is initialized when it is not.
Do not pretend file access exists when it does not.
Do not treat Search Logs as memory.
Do not treat `skills_bundle.md` as source of truth.
Do not include secrets.
Do not dump full documents unless explicitly requested.
Do not skip source status, Search Log, uncertainty, exclusions, or open questions when required.
Return exactly the required Markdown result structure from the input.
---
## input
Search for and build an Allzy Framework Context Retrieval Builder result.
Search objective:
Find, select, and package relevant project context for a specific Allzy Framework task, question, review, implementation handoff, documentation job, prompt creation job, audit, or AI handoff.
Domain context:
Allzy Framework deterministic metadata retrieval, context retrieval, context packages, Agent 2 handoffs, patch handoff context, review context, documentation source packs, Search Logs, source status, metadata-tagged project documents, `context_retrieval.md`, `metadata_index.md`, `metadata_index.json`, `memory.md`, skills index, Yin/Yang references as context only, module IDs, submodule IDs, document types, layers, tags, aliases, related files, references, parents, children, paired Yin/Yang links, source block IDs, generated-from metadata, retrieval descriptions, file paths, folder structure, and available project context.
Use this config block as the operating input. If fields are empty or incomplete, treat the request as Assistant Mode and ask only for the smallest missing field needed to make the retrieval goal and output mode actionable.
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

If Assistant Mode is required, ask for this retrieval request information:

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

Search and retrieval scope:
Use available project context and publicly indexed information only when relevant to locating or understanding Allzy Framework context retrieval material. Prioritize exact project files, provided context, metadata, and accessible source material over general web information.

Primary retrieval signals:

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

Retrieval initialization check:
Before building the output, verify whether deterministic retrieval is available.

Look for or ask for:

* context_retrieval.md
* metadata/frontmatter conventions
* metadata-tagged documents
* optional metadata_index.md or metadata_index.json
* known context root
* known docs root
* memory file if requested
* skills index if requested
* accessible files or provided document contents

If retrieval is not initialized and require_context_retrieval_initialized is true, state exactly:

Retrieval is not initialized yet. Run Workspace Context Initialization first, or provide `context_retrieval.md` and metadata conventions.

If allow_minimal_retrieval_bootstrap is true, create a minimal temporary retrieval plan labeled exactly:

Temporary Retrieval Bootstrap — not a replacement for `context_retrieval.md`.

Do not silently invent a retrieval system.

If file access is unavailable and no documents were provided, ask the user to provide relevant files, metadata index, or context root contents.

Retrieval depth:
Fast retrieval searches only exact known IDs, exact paths, exact tags, directly matching titles, and directly relevant memory sections if provided.

Standard retrieval searches exact IDs, module IDs, submodule IDs, document type, layer, tags and aliases, paired Yin/Yang references, related memory, and relevant skills if enabled.

Deep retrieval searches all Standard sources plus parent/child relationships, related references, old or superseded documents where relevant, examples if enabled, templates if enabled, conflicts, exclusions, uncertainty, source freshness/status, relevant skills, and prior notes.

Retrieval priority:
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

Exclude by default:

* secrets
* raw chat logs
* unrelated modules
* unrelated layers
* deprecated documents unless historical comparison is needed
* archived documents unless explicitly requested
* superseded documents unless needed to explain a conflict
* generated bundles when source files exist
* skills_bundle.md as source of truth

If natural language is provided instead of exact IDs, derive retrieval keys. Mark derived keys as derived, not confirmed. Prefer user-provided exact IDs over inferred keys. Use aliases to improve recall. Do not invent project facts from derived keys. If confidence is low, state uncertainty.

Example derived retrieval keys for the topic “Discord bot moderation role permissions”:

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

Source status:
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

Do not treat every match as equally authoritative. Prefer source-of-truth documents over summaries, bundles, old drafts, or generated exports.

Search Log:
If create_search_log is true, include a Search Log with:

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

Search Log is not memory. Do not move Search Log content into memory.md unless a confirmed lasting fact emerges later.

Output artifact modes:

For summary, use:

# Context Summary — [Topic]
## Summary
## Key Findings
## Relevant Sources
## Open Questions
## Search Log

For deep_brief, use:

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

For agent_context_package, use:

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

For patch_handoff_context, use:

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

For document_source_pack, use:

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

For review_context, use:

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

For custom, infer a suitable structure, include source status, include Search Log unless disabled, include open questions, do not implement or rewrite source docs, and clearly state what was built and why.

Agent audience rules:
If target_audience is agent_2, make the output compact, actionable, and scoped.
If target_audience is human, the output may be more explanatory.
If target_audience is reviewer, prioritize source status, conflicts, and checklist.
If target_audience is documentation_agent, prioritize source map, excerpts, terminology, and missing source warnings.
Do not assume Agent 2 is the same model/platform as Agent 1.
If target model/platform are provided, include them only as labels unless a specific reference document is also provided.

Required final output shape:
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

Missing information behavior:
If reliable information is not available, state that clearly rather than providing speculative information.
Only provide information that can be verified from search results, provided context, accessible project material, or explicit user input.
If no relevant results or accessible context are found, say what was searched and what remains unavailable.
If expected documents are missing, state what is missing.
If deterministic retrieval is required but not initialized, stop and use the exact retrieval-not-initialized message above.
If the retrieval goal or output mode is not actionable, ask for the smallest missing field.

Final constraints:
Do not ask for URLs or source links.
Do not generate URLs.
Do not include few-shot examples in future Perplexity search queries except the retrieval-key example already included as context for output pattern control.
Keep one coherent retrieval objective per run.
Do not split into unrelated topics unless the user requests multiple separate runs.
Do not implement code, fix bugs, rewrite source documents, update state files, create Master Documents, or create Yin/Yang documents.
Return exactly the required Markdown result structure.
