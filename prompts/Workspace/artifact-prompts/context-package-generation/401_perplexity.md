---
id: "allzy.framework.prompts.workspace.context-package-generation.perplexity"
title: "Context Package Generation Prompt — Perplexity"
artifact_type: "Prompt"
prompt_family: "Workspace"
prompt_variant: "Context Package Generation"
adaptation_target: "Perplexity"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - workspace
  - context-package-generation
  - perplexity
---

# Context Package Generation Prompt — Perplexity Search
## Purpose
Use this prompt with Perplexity / Sonar-style search models when a source-grounded search workflow is needed to generate a task-specific Allzy Framework Context Package.
This prompt is structured for Perplexity-style usage:
- `instructions` controls answer behavior, tone, grounding, and formatting.
- `input` contains the actual search-relevant query details.
Search-critical details must be included in `input`, not only in `instructions`.
Do not ask the model to generate URLs. Source URLs should be taken from the host application's `search_results` metadata, not from generated answer text.
---
## instructions
Provide a concise, source-grounded, task-specific context package for an Allzy Framework project.
Use a direct, practical, documentation-ready style.
Only provide information that can be verified from the available search results, provided context, attached files, configured workspace files, or explicitly referenced project sources.
If reliable information is not found, state that clearly rather than providing speculative information.
Do not fabricate source titles, URLs, file paths, project decisions, dates, owners, tasks, implementation details, or citations.
Do not include source URLs in the generated answer. If sources are available through the host application, refer to them by title, filename, path, document name, or source label only.
If certain information is missing, unavailable, inaccessible, private, not publicly indexed, or not present in provided context, mark it as unavailable or uncertain.
Separate sourced facts from interpretation.
The output must be Markdown and must follow the required result structure exactly.
Do not add explanations after the result.
---
## input
Generate a task-specific Allzy Framework Context Package.
Search objective:
Find and synthesize the exact context needed by the next AI agent for one specific Allzy Framework task, review, patch, handoff, implementation step, Triage follow-up, documentation step, or research step.
Project/domain context:
This is for the Allzy Framework workspace context layer. A Context Package is a temporary selected context bundle for one task. It answers: “What exact context should the next agent use for this specific task?”
Use case:
The result will support another AI agent, coding agent, reviewer, researcher, documentation agent, or implementation follow-up agent. The package should reduce guessing, token waste, context contamination, and unnecessary project exploration.
Operation:
generate_package
Config:
```yaml
---
context_package_generation_config:
  mode: "" # assistant | preconfigured
  operation: "generate_package" # generate_package
  target_artifact: "context_package"
  output_filename: "" # e.g. context_package_<task-id>.md
  task:
    task_id: ""
    task_title: ""
    task_type: "" # implementation | review | patch | triage_handoff | research | documentation | mixed | unknown
    goal: ""
    target_agent: "" # agent-2 | coding-agent | reviewer | researcher | other | unknown
    target_environment: "" # cursor | claude-code | codex-cli | chatgpt | gemini | other | unknown
  inputs:
    task_prompt_provided: null # true | false
    plan_md_provided: null # true | false
    memory_md_provided: null # true | false
    context_retrieval_md_provided: null # true | false
    search_log_provided: null # true | false
    metadata_index_provided: null # true | false
    source_documents_provided: null # true | false
    existing_context_package_provided: null # true | false
  source_paths:
    plan_md: "" # e.g. context/plan.md
    memory_md: "" # e.g. context/memory.md
    context_retrieval_md: "" # e.g. context/context_retrieval.md
    metadata_index: "" # e.g. context/metadata_index.md
    search_log: ""
    source_documents_root: ""
  selection_policy:
    include_task_summary: true
    include_retrieval_summary: true
    include_relevant_plan_items: true
    include_relevant_memory_only: true
    include_relevant_document_excerpts: true
    include_search_log: true
    include_exclusions: true
    include_open_questions: true
    include_handoff_context: true
    mark_memory_candidates: true
    exclude_unrelated_memory: true
    exclude_raw_chat: true
    exclude_secrets: true
    avoid_full_context_dump: true
  output_style: "copy_ready" # copy_ready | report_only | file_ready
---

Source scope:
Use only available, provided, attached, configured, explicitly referenced, or publicly indexed project/context sources relevant to the task.

Prioritize sources in this order unless a provided context_retrieval.md defines a stronger project-specific priority:

1. Current task prompt or user request
2. plan.md current focus and active task
3. context_retrieval.md retrieval rules
4. metadata index entries relevant to the task
5. relevant source documents
6. memory.md sections relevant to the task
7. Search Logs, if available
8. prior handoffs or context packages, only as temporary references
9. semantic or title-based matching as helper

Required search and synthesis dimensions:

* task ID
* task title
* task type
* task goal
* target agent or target environment
* scope boundaries
* search goal
* source paths or document labels
* metadata filters
* document matches
* relevant plan items
* relevant memory sections
* relevant source excerpts or summaries
* Search Log entries
* exclusions and reasons
* unresolved retrieval uncertainty
* open questions
* memory candidates
* compact final handoff context

If available, use search-friendly identifiers and terms:

* Allzy Framework
* Workspace Context
* Context Package
* plan.md
* memory.md
* context_retrieval.md
* metadata_index.md
* metadata_index.json
* Search Log
* task ID
* module ID
* submodule ID
* document type
* layer
* tag
* source document
* handoff context
* Agent 2
* coding agent
* reviewer
* researcher
* Triage handoff

Context selection rules:
Select only task-relevant context. Do not dump all available context.

Prefer exact task relevance.

Prefer current truth over history.

Prefer explicit metadata and Search Logs over guessing.

Prefer summaries unless exact excerpts are needed.

Include only memory sections relevant to the task.

Include only document excerpts relevant to the task.

Include exclusions so future agents know what was intentionally ignored.

Mark uncertainty instead of inventing context.

Missing information behavior:
If the task is missing or too vague, ask only for the task goal, target agent/environment if known, and relevant scope boundaries.

If context sources are missing, ask only for the most important missing source.

If reliable information cannot be found in available sources or search results, state that clearly.

If a data point is unavailable, use “Not available” or mark it as uncertain.

If safe generation is blocked by missing context, stop and ask one targeted question.

Security and privacy:
Before generating the package, check all available content for secrets or sensitive operational data.

Secrets include API keys, passwords, tokens, private credentials, database URLs, session secrets, private customer or user data, unredacted logs, private infrastructure values, and internal URLs that should not be included in handoffs.

If secrets are present:

1. Stop.
2. Do not repeat the secret.
3. Ask the user to sanitize the input.
4. Use placeholders only if needed, such as process.env.API_KEY, process.env.DATABASE_URL, or $ENV_SESSION_SECRET.

Hard exclusions:
Do not create or update plan.md.

Do not create or update memory.md.

Do not create or update context_retrieval.md.

Do not define retrieval rules.

Do not generate or update metadata indexes.

Do not create or maintain skills.

Do not clean persistent workspace state.

Do not write application code.

Do not implement features.

Do not fix bugs.

Do not perform Triage itself.

Do not generate a Master Document.

Do not create Yin/Yang documents.

Do not rewrite architecture.

Do not create API contracts.

Do not create database schemas.

Do not create implementation plans.

Do not create execution prompts.

Do not store secrets.

Do not claim file access when no file access exists.

Do not invent source documents.

Do not invent project decisions.

Do not treat context packages as permanent memory.

Do not include all memory by default.

Do not include full source dumps by default.

Do not include unrelated context to appear safer.

Do not treat old context packages as source of truth.

Do not overwrite an existing file unless explicitly allowed by a different task.

Do not ask the model to generate URLs or source links.

Output shape:
Return exactly this Markdown structure:

# Context Package Generation Result
## 1. Operation Used
generate_package
## 2. Target Output
[context package filename or copy-ready output]
## 3. Input Used
[task / plan.md / memory.md / source documents / metadata index / Search Log / missing input]
## 4. Context Package
```markdown
[full generated context package]

5. Package Summary

* Sources used:
* Included:
* Excluded:
* Memory candidates:
* Needs review:

6. Warnings / Blockers

* [Warning, blocker, or None]

7. Recommended Next Step

[Next action]

Inside `## 4. Context Package`, use this structure unless the user explicitly requests a different handoff format:
```markdown
# Context Package
## 1. Task
**Task ID:** [task id or None]  
**Task title:** [task title]  
**Task type:** [implementation / review / patch / triage_handoff / research / documentation / mixed / unknown]  
**Target agent/environment:** [agent or environment]  
## 2. Goal
[What the next agent must accomplish.]
## 3. Scope Boundaries
In scope:
- [Item]
Out of scope:
- [Item]
## 4. Search Goal
[What context was searched for and why.]
## 5. Sources Used
- [Source/path/document/title/source label]
## 6. Filters Used
- [id/module_id/submodule_id/document_type/layer/tag/filter]
## 7. Relevant Plan Context
[Relevant items from plan.md or None provided.]
## 8. Relevant Memory Context
[Relevant confirmed memory or None provided.]
## 9. Relevant Source Context
### [Document, title, path, source label, or section]
[Short excerpt or summary.]
## 10. Exclusions
- [Excluded source and reason.]
## 11. Search Log
- Query / task:
- Filters:
- Documents matched:
- Memory matched:
- Links followed:
- Excluded:
- Unresolved uncertainty:
## 12. Open Questions
- [Question or None.]
## 13. Memory Candidates
- [Candidate or None.]
## 14. Handoff Context
[Compact final handoff context the next agent should use.]

Final grounding instruction:
Base the context package only on available search results, provided context, attached files, configured workspace files, or explicitly referenced project sources. Do not fill gaps with unsupported assumptions. If information cannot be verified, mark it as unavailable or uncertain. Do not generate URLs. Generate only the task-specific Context Package Generation Result.
