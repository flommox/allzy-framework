---
id: "allzy.framework.prompts.workspace.context-package-generation.universal"
title: "Context Package Generation Prompt — Universal"
artifact_type: "Prompt"
prompt_family: "Workspace"
prompt_variant: "Context Package Generation"
adaptation_target: "Universal"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - workspace
  - context-package-generation
  - universal
---

# `context_package_generation_prompt.md`

## Purpose

Use this prompt to generate a task-specific context package for an AI-assisted project workspace.

A context package is a temporary selected context bundle for one task, review, patch, handoff, implementation step, Triage follow-up, or research step.

It answers:

```text
What exact context should the next agent use for this specific task?
```

This prompt selects, summarizes, structures, and packages relevant context.

It does not create `plan.md`.

It does not create `memory.md`.

It does not create or rewrite `context_retrieval.md`.

It does not generate a metadata index.

It does not create or maintain skills.

It does not clean old context packages as living state.

It only generates a context package output.

---

## When to Use This Prompt

Use this prompt when:

- preparing a task-specific handoff for another AI agent
- giving a coding agent only the context it needs
- reducing token waste before implementation
- creating a context package from `plan.md`, `memory.md`, docs, Search Logs, and retrieval results
- preparing a review context
- preparing a patch handoff context
- preparing a Triage-to-implementation handoff context
- summarizing relevant excerpts for one task
- documenting what was searched and why
- separating selected task context from permanent project memory

---

## When Not to Use This Prompt

Do not use this prompt to:

- create or update `plan.md`
- create or update `memory.md`
- create or update `context_retrieval.md`
- define retrieval rules
- generate or update metadata indexes
- create or maintain skills
- write application code
- implement features
- fix bugs
- perform Triage itself
- generate a Master Document
- create Yin/Yang documents
- rewrite architecture
- clean persistent workspace state
- store permanent project truth
- treat old context packages as memory
- store secrets

If the user asks for one of these tasks, explain that this prompt only generates a task-specific context package.

---

## Config Block

This config block is always present.

If the config is filled, use it as **Preconfigured Mode**.

If the config is empty or incomplete, use **Assistant Mode** and ask only the next necessary question.

If the user manually edits the config before running the prompt, treat it exactly like website-generated config.

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
```

---

## Operating Logic

This prompt supports one primary operation:

```text
generate_package
```

### `generate_package`

Use this operation when a specific task needs a compact, selected context bundle.

The context package should contain enough context for the next agent to work safely.

It should not contain every available document.

It should not contain all memory.

It should not contain unrelated source material.

It should not become permanent memory.

It should not be reused as project truth after the task is done.

---

## Assistant Mode

If the config is empty or incomplete, ask only the next necessary question.

Do not ask all setup questions at once.

### Question 1 — Task

If the task is missing, ask:

```text
What task should this context package support?
Please provide the task goal, target agent/environment if known, and any relevant scope boundaries.
```

### Question 2 — Available Inputs

Ask only after the task is known:

```text
Which context sources are available for this package?

1. plan.md
2. memory.md
3. context_retrieval.md
4. metadata_index.md / metadata_index.json
5. Search Log
6. source documents
7. existing notes or handoff
```

### Question 3 — Missing Critical Source

If the task requires context that was not provided, ask for the most important missing source only.

Example:

```text
Please provide memory.md or the relevant memory sections. I only need the parts related to this task.
```

### Question 4 — Output Preference

Ask only if needed:

```text
Should I return the context package as copy-ready Markdown or as a file-ready document?
```

---

## File Access Rule

If running in an environment with file access, inspect the configured files and source paths directly.

If running in a normal chat without file access, ask the user to paste or attach only the necessary content.

Do not pretend to have read files that were not provided or accessible.

If the source documents are too large, ask for or produce a narrower retrieval request.

Do not request all project files unless the task truly requires broad context.

---

## Security and Privacy Check

Before generating a context package, check all provided content for secrets or sensitive operational data.

Secrets include:

- API keys
- passwords
- tokens
- private credentials
- database URLs
- session secrets
- private customer or user data
- unredacted logs
- private infrastructure values
- internal URLs that should not be included in handoffs

If secrets are present:

1. Stop.
2. Do not repeat the secret.
3. Ask the user to sanitize the input.
4. Use placeholders only if an example is needed.

Use placeholders such as:

```text
process.env.API_KEY
process.env.DATABASE_URL
$ENV_SESSION_SECRET
```

Never store real secrets in a context package.

---

## Context Package Role

A context package is temporary selected context for one task.

It is not:

```text
plan.md
memory.md
context_retrieval.md
metadata_index
skills/
raw chat history
full documentation dump
```

It may reference those sources.

It may quote or summarize relevant excerpts.

It may include a Search Log.

It may identify memory candidates.

It must not become the source of truth for lasting project facts.

---

## Context Package Must Contain

A useful context package should contain:

- task title
- task goal
- target agent or environment if known
- task type
- scope boundaries
- search goal
- sources used
- filters used
- documents matched
- relevant excerpts or summaries
- relevant memory sections
- relevant plan items
- exclusions
- unresolved retrieval uncertainty
- open questions
- handoff context
- memory candidates if lasting facts were found

---

## Context Package Must Not Contain

Do not include:

- all memory by default
- unrelated project history
- unrelated source documents
- raw chat logs
- old context packages unless explicitly needed
- all Search Logs
- full skills bundle
- generated metadata index dumps unless directly relevant
- secrets
- speculative content as fact
- stale or superseded facts as current truth
- broad backlog
- unrelated implementation details

---

## Selection Principles

Use these principles:

```text
Select, do not dump.
Prefer exact task relevance.
Prefer current truth over history.
Prefer explicit metadata and Search Logs over guessing.
Prefer summaries unless exact excerpts are needed.
Include only memory sections relevant to the task.
Include only document excerpts relevant to the task.
Include exclusions so future agents know what was intentionally ignored.
Mark uncertainty instead of inventing context.
```

---

## Source Priority

Use this source priority unless the provided `context_retrieval.md` defines a stronger project-specific priority:

```text
1. Current task prompt or user request
2. plan.md current focus and active task
3. context_retrieval.md retrieval rules
4. metadata index entries relevant to the task
5. relevant source documents
6. memory.md sections relevant to the task
7. Search Logs, if available
8. prior handoffs or packages, only as temporary references
9. semantic or title-based matching as helper
```

If `context_retrieval.md` is available, follow it.

If it is not available, use the fallback priority above and state that retrieval was performed with fallback rules.

---

## Retrieval and Filtering Rules

When building the package:

1. Identify the task goal.
2. Identify the narrowest known scope.
3. Use IDs, module IDs, submodule IDs, document types, layers, tags, and explicit filenames when available.
4. Select only matching documents or sections.
5. Extract only relevant excerpts or summaries.
6. Add relevant current memory.
7. Add relevant plan items.
8. Log exclusions.
9. Mark unresolved uncertainty.
10. Do not include unrelated context to be “safe.”

If source context is incomplete, generate the best possible package and mark missing context.

If missing context blocks safe use, stop and request the single most important missing source.

---

## Memory Candidate Rules

If lasting confirmed facts are discovered while generating the package, do not store them as permanent truth inside the package.

Instead, add:

```markdown
## Memory Candidates

- [Confirmed fact that should be considered for memory.md]
```

Only add memory candidates when they are:

- confirmed
- stable
- relevant beyond the current task
- useful for future agents
- not already clearly present in memory.md

Do not add speculative ideas as memory candidates.

---

## Exclusion Rules

Exclude by default:

```text
- unrelated modules
- unrelated submodules
- unrelated layers
- superseded documents
- archived documents
- deprecated documents
- old context packages
- raw chat logs
- unreviewed speculation
- full memory dumps
- full metadata indexes
- full skills bundles
- secrets
```

If excluded content may look relevant, record the exclusion and reason.

---

## Required Context Package Output Shape

Use this structure unless the user explicitly requests a different handoff format.

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

- [Source/path/document]

## 6. Filters Used

- [id/module_id/submodule_id/document_type/layer/tag/filter]

## 7. Relevant Plan Context

[Relevant items from plan.md or None provided.]

## 8. Relevant Memory Context

[Relevant confirmed memory or None provided.]

## 9. Relevant Source Context

### [Document or section]

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
```

---

## Date Rule

If a date is needed, use the current date.

If the current date is unavailable, use:

```text
YYYY-MM-DD
```

Do not invent historical dates.

---

## Processing Protocol

### Step 1 — Resolve Config

Read the config block.

Determine:

- mode
- task
- task type
- target agent/environment
- available inputs
- source paths
- selection policy
- output style

If config is incomplete, enter Assistant Mode.

---

### Step 2 — Validate Task Specificity

A context package must support a specific task.

If the task is too vague, ask for the task goal.

Do not generate a generic project overview unless explicitly requested.

---

### Step 3 — Determine Input Availability

Require at least one of:

- task prompt
- plan.md
- memory.md
- source documents
- Search Log
- metadata index
- retrieval result
- existing handoff notes

If no useful input is provided and no file access exists, ask for the most relevant source.

---

### Step 4 — Check Scope

Verify that the request is about generating a context package.

If the request is about another artifact, redirect:

```text
This prompt only generates context packages. Use the appropriate artifact prompt for plan.md, memory.md, context_retrieval.md, metadata indexes, or skills.
```

---

### Step 5 — Security Check

Inspect input for secrets.

Stop if unsafe.

Do not repeat secrets.

---

### Step 6 — Select Context

Use available retrieval rules and sources.

Identify:

- relevant plan items
- relevant memory sections
- relevant source documents
- relevant excerpts
- relevant metadata filters
- relevant previous search results
- relevant exclusions
- unresolved uncertainty
- possible memory candidates

---

### Step 7 — Build Context Package

Create a compact package using the required output shape.

Do not include unrelated context.

Do not include full documents unless explicitly required and safe.

Do not treat package content as permanent truth.

---

### Step 8 — Explain Package Quality

Briefly list:

- what sources were used
- what was excluded
- what is missing
- what should be reviewed
- whether the package is ready for the target agent

---

## Required Output Format

Return exactly:

```markdown
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
```

## 5. Package Summary

- Sources used:
- Included:
- Excluded:
- Memory candidates:
- Needs review:

## 6. Warnings / Blockers

- [Warning, blocker, or None]

## 7. Recommended Next Step

[Next action]
```

---

## Hard Boundaries

Do not:

- write application code
- implement features
- fix bugs
- perform Triage itself
- generate a Master Document
- create Yin/Yang documents
- create or update `plan.md`
- create or update `memory.md`
- create or update `context_retrieval.md`
- generate or update metadata indexes
- create or maintain skills
- store secrets
- claim file access when no file access exists
- invent source documents
- invent project decisions
- treat context packages as permanent memory
- include all memory by default
- include full source dumps by default
- include unrelated context to appear safer
- treat old context packages as source of truth
- overwrite an existing file unless explicitly allowed

---

## Final Rule

Your job is to generate a task-specific context package.

Select only relevant context.

Do not dump everything.

Keep permanent truth in `memory.md`.

Keep retrieval rules in `context_retrieval.md`.

Keep reusable lessons in `skills/`.

If required input is missing, ask only for the next necessary input.
