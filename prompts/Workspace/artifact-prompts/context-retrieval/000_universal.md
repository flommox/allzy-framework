---
id: "allzy.framework.prompts.workspace.context-retrieval.universal"
title: "Context Retrieval Prompt — Universal"
artifact_type: "Prompt"
prompt_family: "Workspace"
prompt_variant: "Context Retrieval"
adaptation_target: "Universal"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - workspace
  - context-retrieval
  - universal
---

# `context_retrieval_prompt.md`

## Purpose

Use this prompt to create, inspect, or repair `context_retrieval.md` for an AI-assisted project workspace.

`context_retrieval.md` is the reusable deterministic retrieval method for the workspace.

It answers:

```text
How should agents find the right context?
```

This prompt defines how AI agents should search, filter, select, exclude, and log relevant context before implementation, Triage, review, or handoff generation.

It does not create `plan.md`.

It does not create `memory.md`.

It does not generate a context package.

It does not generate a metadata index.

It does not create or maintain skills.

It only works on the retrieval method file.

---

## When to Use This Prompt

Use this prompt when:

- creating `context_retrieval.md`
- defining deterministic context search rules
- defining metadata-first retrieval behavior
- defining document type, layer, tag, and ID lookup rules
- defining parent/child traversal rules
- defining paired Yin/Yang traversal rules
- defining memory section lookup rules
- defining exclusion rules
- defining Search Log format
- checking whether an existing `context_retrieval.md` is usable
- repairing placeholder retrieval rules
- adapting retrieval rules to an existing project documentation structure

---

## When Not to Use This Prompt

Do not use this prompt to:

- create or update `plan.md`
- create or update `memory.md`
- store confirmed project truth
- generate context packages
- generate or update metadata indexes
- create or maintain skills
- write application code
- implement features
- fix bugs
- perform Triage
- generate a Master Document
- create Yin/Yang documents
- rewrite architecture
- clean living workspace state
- compress memory
- maintain full project history
- store raw chat history
- store secrets

If the user asks for one of these tasks, explain that this prompt only creates, inspects, or repairs `context_retrieval.md`.

---

## Config Block

This config block is always present.

If the config is filled, use it as **Preconfigured Mode**.

If the config is empty or incomplete, use **Assistant Mode** and ask only the next necessary question.

If the user manually edits the config before running the prompt, treat it exactly like website-generated config.

```yaml
---
context_retrieval_prompt_config:
  mode: "" # assistant | preconfigured

  operation: "" # generate | inspect | repair_placeholders
  target_artifact: "context_retrieval.md"
  target_path: "" # e.g. context/context_retrieval.md, .ai/context/context_retrieval.md

  allow_file_creation: null # true | false
  allow_file_updates: null # true | false
  allow_overwrite: false
  allow_placeholder_repair: null # true | false

  target_exists: null # true | false | unknown
  existing_retrieval_file_provided: null # true | false
  project_structure_input_provided: null # true | false
  metadata_conventions_provided: null # true | false

  retrieval_scope:
    project_name: ""
    documentation_root: "" # e.g. docs/, context/, blocks/, modules/
    memory_path: "" # e.g. context/memory.md
    plan_path: "" # e.g. context/plan.md
    metadata_index_path: "" # optional
    search_log_template_path: "" # optional

  retrieval_features:
    use_frontmatter_metadata: true
    use_document_ids: true
    use_module_ids: true
    use_submodule_ids: true
    use_layers: true
    use_document_types: true
    use_tags: true
    use_parent_child_links: true
    use_paired_yin_yang_links: true
    use_memory_section_lookup: true
    use_search_logs: true
    allow_semantic_search_as_helper: true

  output_style: "copy_ready" # copy_ready | report_only | patch_ready
  target_environment: "" # cursor | claude-code | codex-cli | chatgpt | gemini | other | unknown
---
```

---

## Operating Logic

This prompt supports three operations:

```text
generate
inspect
repair_placeholders
```

### `generate`

Use this operation when:

- no `context_retrieval.md` exists
- a deterministic retrieval method is needed
- the project has structured Markdown, YAML frontmatter, IDs, tags, layers, modules, or Yin/Yang documents
- future agents need repeatable search behavior
- broad repository guessing should be reduced

If `context_retrieval.md` does not exist and file creation is allowed, create it.

If file creation is not allowed, return copy-ready Markdown.

---

### `inspect`

Use this operation when:

- `context_retrieval.md` already exists
- the user wants to know whether retrieval is ready
- file updates are not allowed
- the existing file may be outdated
- metadata conventions may not match current project structure

Inspection should report issues.

Inspection should not rewrite the file.

---

### `repair_placeholders`

Use this operation when:

- `context_retrieval.md` exists but contains placeholders
- known project structure is available
- metadata rules are known
- placeholder sections can be safely replaced
- file updates or copy-ready replacement are allowed

This operation repairs incomplete method sections.

It is not normal cleaning.

It should not compress or simplify valid retrieval rules merely because they are long.

---

## Assistant Mode

If the config is empty or incomplete, ask only the next necessary question.

Do not ask all setup questions at once.

### Question 1 — Operation

If `operation` is missing, ask:

```text
What should I do with context_retrieval.md?

1. Generate a new retrieval method
2. Inspect an existing retrieval method
3. Repair placeholders in an existing retrieval method
```

### Question 2 — Input

Ask only for the needed input.

If generating:

```text
Please provide the project documentation structure, known metadata/frontmatter conventions, and where plan.md/memory.md are located. Rough structure is enough.
```

If inspecting:

```text
Please paste or attach the existing context_retrieval.md.
```

If repairing placeholders:

```text
Please paste or attach the existing context_retrieval.md and provide the project structure or metadata rules needed to replace placeholders.
```

### Question 3 — File Permission

Ask only if file access exists and permission is unclear:

```text
May I create or update context_retrieval.md directly, or should I return copy-ready Markdown only?
```

---

## File Access Rule

If running in an environment with file access, inspect the target file and relevant documentation structure directly.

If running in a normal chat without file access, ask the user to paste or attach the needed content.

Do not pretend to have read files that were not provided or accessible.

If `target_path` is missing and file access is needed, ask for the path.

Default target path if no path is provided:

```text
context/context_retrieval.md
```

---

## Security and Privacy Check

Before creating, inspecting, or repairing `context_retrieval.md`, check all provided content for secrets or sensitive operational data.

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
- internal URLs that should not be stored in retrieval rules

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

Never store real secrets in `context_retrieval.md`.

---

## `context_retrieval.md` Role

`context_retrieval.md` is the source of truth for search and retrieval behavior.

It defines how agents locate relevant project context.

It must stay separate from:

```text
plan.md
memory.md
context packages
metadata indexes
skills/
raw chat history
```

It should describe the method.

It should not store the project’s permanent memory.

It should not store task checklists.

It should not store generated Search Logs as permanent content.

It should not duplicate skill rules.

It should not become a context dump.

---

## `context_retrieval.md` Must Contain

A useful `context_retrieval.md` should define:

- purpose of retrieval
- search priority
- metadata fields
- document ID rules
- module and submodule lookup rules
- layer rules
- document type rules
- tag rules
- parent/child traversal
- paired Yin/Yang traversal
- memory section lookup
- exclusion rules
- Search Log format
- context package selection rules
- uncertainty handling
- fallback behavior
- safety boundaries

---

## `context_retrieval.md` Must Not Contain

Do not include:

- current active task checklist
- confirmed long-term memory
- full context package contents
- generated metadata index contents
- full skills
- raw chat logs
- implementation diary
- broad project backlog
- speculative ideas
- secrets
- unrelated architecture rewrite
- application runtime state rules

---

## Retrieval Principles

The retrieval method should follow these principles:

```text
Prefer explicit metadata over guessing.
Prefer stable IDs over fuzzy titles.
Prefer document_type and layer filters before semantic search.
Follow parent/child links when scope expansion is needed.
Follow paired Yin/Yang links when implementation and human context both matter.
Use memory.md only for confirmed current truth.
Use plan.md only for current focus.
Use semantic search only as helper, not source of truth.
Record search choices in a Search Log.
Exclude deprecated, archived, superseded, unrelated, and secret-bearing sources.
```

---

## Recommended Search Priority

Use this priority unless the project has stronger existing conventions:

```text
1. Exact `id`
2. Exact `module_id`
3. Exact `submodule_id`
4. Exact `document_type`
5. Exact `layer`
6. High-signal tags
7. Parent/child links
8. Paired Yin/Yang links
9. Related memory sections
10. Prior context packages or handoffs, only as temporary references
11. Semantic search as helper
```

Semantic search may help find candidates.

Semantic search should not override explicit metadata.

---

## Recommended Metadata Fields

Use these fields when the project supports YAML/frontmatter:

```yaml
---
id:
title:
document_type:
layer:
status:
version:
created:
updated:
tags:
related:
---
```

Optional implementation/framework fields:

```yaml
module_id:
submodule_id:
parent:
children:
paired_yin:
paired_yang:
schemas:
trace_map:
source_block_id:
generated_from:
depends_on:
used_by:
supersedes:
superseded_by:
```

Do not require all optional fields for small projects.

---

## Recommended Document Type Rules

Define document types clearly.

Example:

```text
Master Specification
Genesis Document
Yin Page
Yang Core Module
Triage Handoff
Implementation Handoff
Review Report
State File
Context Retrieval
Context Package
Metadata Index
Search Log
Skill
Prompt
Template
Reference
```

Agents should filter by document type before reading large documents.

---

## Recommended Layer Rules

Define project layers clearly.

Example:

```text
Vision
Infrastructure
System
Core
Ecosystem
Utilities
State
Reference
```

Agents should use layers to avoid mixing unrelated areas.

---

## Recommended Tag Rules

Tags should be:

- lowercase when practical
- stable
- specific
- reusable
- not overly personal
- not one-off prose
- useful for filtering

Example:

```text
state
memory
retrieval
metadata
yin
yang
triage
implementation
review
frontend
backend
auth
billing
discord
docs
```

Avoid vague tags such as:

```text
important
misc
todo
stuff
random
```

---

## Parent / Child Traversal Rules

Use parent/child links to move between larger and smaller scopes.

Example:

```text
Parent document:
- module overview
- master specification
- feature area

Child document:
- submodule
- implementation contract
- Yang module
- detailed handoff
```

Traversal rule:

```text
Start from the narrowest known scope.
Move upward only when needed for missing context.
Move downward only when implementation detail is required.
Do not read the entire parent hierarchy unless necessary.
```

---

## Paired Yin/Yang Traversal Rules

If the project uses Yin/Yang documents:

```text
Yin = human/context/documentation side
Yang = AI execution contract / implementation side
```

Traversal rule:

```text
If implementing:
→ read Yang first, then paired Yin only for human intent or missing context.

If reviewing requirements or user intent:
→ read Yin first, then paired Yang for implementation constraints.

If both are available:
→ cite or log both in the Search Log.

If pair links are missing:
→ search by shared module_id, submodule_id, source_block_id, or title.
```

---

## Memory Section Lookup Rules

Use `memory.md` only for confirmed current truth.

Do not dump all memory into every task.

Recommended lookup flow:

```text
1. Identify task/module/submodule.
2. Search memory headings and tags if available.
3. Extract only sections relevant to the current task.
4. Prefer current truth over older historical notes.
5. Exclude superseded memory unless needed to avoid repeated mistakes.
6. Include unresolved troubleshooting notes only if relevant.
```

---

## Exclusion Rules

Exclude by default:

```text
- deprecated documents
- archived documents
- superseded documents
- unrelated modules
- unrelated submodules
- unrelated layers
- raw chat logs
- old context packages unless explicitly needed
- generated bundles treated as source of truth
- secrets
- unredacted private logs
- speculative notes
```

If excluded content may still matter, record it in the Search Log under `Excluded`.

---

## Search Log Format

Every retrieval run should produce or append a Search Log entry when context is selected.

Use this format:

```markdown
# Search Log Entry

## Query / Task

[What context was searched for.]

## Filters Used

- id:
- module_id:
- submodule_id:
- document_type:
- layer:
- tags:

## Documents Matched

- [path or document id]

## Memory Sections Matched

- [memory heading or id]

## Links Followed

- [parent / child / paired_yin / paired_yang / related]

## Excluded

- [file/document and reason]

## Unresolved Retrieval Uncertainty

- [uncertainty or None]
```

---

## Context Package Selection Rules

When a context package is requested, retrieval should produce selected context, not a full dump.

Include:

- task
- search goal
- filters used
- documents matched
- relevant excerpts or summaries
- memory sections matched
- exclusions
- unresolved uncertainty
- recommended handoff context

Do not include:

- unrelated full documents
- all memory
- all Search Logs
- all skills
- raw chat history
- secrets

Lasting confirmed facts discovered during package generation should be proposed as memory candidates, not stored inside retrieval rules.

---

## Placeholder Repair Rules

When repairing placeholders:

1. Replace placeholders only when source information is provided or file access confirms it.
2. Preserve valid existing retrieval rules.
3. Do not simplify working rules just because they are long.
4. Do not invent metadata conventions.
5. If a placeholder cannot be filled safely, leave it marked as `TODO` or `Needs Input`.
6. Report every unresolved placeholder.
7. Do not convert placeholder repair into a full rewrite unless explicitly allowed.

---

## Required `context_retrieval.md` Output Shape

Use this structure unless the existing file has a stronger compatible structure.

```markdown
---
id: "state.context-retrieval"
title: "Context Retrieval Method"
document_type: "Context Retrieval"
status: "Active"
updated: "YYYY-MM-DD"
tags:
  - state
  - retrieval
  - metadata
---

# Context Retrieval Method

## Purpose

This file defines how agents retrieve project context before implementation, Triage, review, or handoff creation.

## Retrieval Principles

- Prefer explicit metadata over guessing.
- Prefer stable IDs over fuzzy titles.
- Use semantic search only as helper.
- Record search choices in a Search Log.

## Search Priority

1. Exact `id`
2. Exact `module_id`
3. Exact `submodule_id`
4. Exact `document_type`
5. Exact `layer`
6. High-signal tags
7. Parent/child links
8. Paired Yin/Yang links
9. Related memory sections
10. Semantic search as helper

## Metadata Fields

### Required Base Fields

- `id`
- `title`
- `document_type`
- `layer`
- `status`
- `updated`
- `tags`

### Optional Fields

- `module_id`
- `submodule_id`
- `parent`
- `children`
- `paired_yin`
- `paired_yang`
- `source_block_id`
- `generated_from`
- `depends_on`
- `used_by`
- `supersedes`
- `superseded_by`

## Document Type Rules

[Define document types used in this workspace.]

## Layer Rules

[Define layers used in this workspace.]

## Tag Rules

[Define tag conventions.]

## Parent / Child Traversal

[Define traversal behavior.]

## Paired Yin/Yang Traversal

[Define paired document traversal.]

## Memory Section Lookup

[Define how memory.md is searched.]

## Exclusion Rules

[Define what to exclude by default.]

## Search Log Format

[Define Search Log format.]

## Context Package Rules

[Define how selected context becomes a package.]

## Fallback Behavior

[Define what to do when metadata is incomplete.]

## Unresolved Setup Questions

- [Question or None]
```

---

## Date Rule

Use the current date for `updated`.

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
- operation
- target path
- whether the target exists
- whether existing retrieval file content is provided
- whether project structure is provided
- whether metadata conventions are provided
- file creation permission
- file update permission
- placeholder repair permission
- output style

If config is incomplete, enter Assistant Mode.

---

### Step 2 — Determine Input Availability

For `generate`, require at least one of:

- project documentation structure
- metadata/frontmatter conventions
- known document types
- known layers
- known module/submodule structure
- existing project context description

For `inspect`, require:

- existing `context_retrieval.md`

For `repair_placeholders`, require:

- existing `context_retrieval.md`
- project structure or metadata conventions needed to fill placeholders

If required input is missing, ask only for that input.

---

### Step 3 — Check Scope

Verify that the request is about `context_retrieval.md`.

If the request is about another artifact, redirect:

```text
This prompt only handles context_retrieval.md. Use the appropriate artifact prompt for plan.md, memory.md, context packages, metadata indexes, or skills.
```

---

### Step 4 — Security Check

Inspect input for secrets.

Stop if unsafe.

Do not repeat secrets.

---

### Step 5 — Analyze Retrieval Readiness

Identify:

- metadata availability
- ID conventions
- module/submodule conventions
- document types
- layers
- tags
- parent/child links
- paired Yin/Yang links
- memory lookup rules
- exclusion rules
- Search Log format
- placeholder sections
- outdated or contradictory retrieval rules
- missing fallback behavior
- unresolved setup questions

---

### Step 6 — Produce Output

Depending on operation:

```text
generate
→ return full context_retrieval.md content

inspect
→ return inspection report only

repair_placeholders
→ return full repaired context_retrieval.md content or patch-ready sections
```

Do not return only partial edits unless `output_style` is `patch_ready`.

---

### Step 7 — Explain Changes

Briefly list:

- what was created
- what was inspected
- what was repaired
- what was preserved
- what needs review
- what was not changed

---

## Required Output Format

Return exactly:

```markdown
# context_retrieval.md Result

## 1. Operation Used

[generate / inspect / repair_placeholders]

## 2. Target Artifact

[context_retrieval.md path or provided content]

## 3. Input Used

[project structure / existing retrieval file / metadata conventions / missing input]

## 4. Output

```markdown
[full generated or repaired context_retrieval.md content]
```

## 5. Change Summary

- Created:
- Repaired:
- Preserved:
- Needs review:
- Not changed:

## 6. Warnings / Blockers

- [Warning, blocker, or None]

## 7. Recommended Next Step

[Next action]
```

If `inspect` is used, replace `## 4. Output` with:

```markdown
## 4. Inspection Report

[inspection findings]
```

---

## Hard Boundaries

Do not:

- write application code
- implement features
- fix bugs
- perform Triage
- generate a Master Document
- create Yin/Yang documents
- create or update `plan.md`
- create or update `memory.md`
- generate context packages
- generate metadata indexes
- create or maintain skills
- store secrets
- claim file access when no file access exists
- invent project structure
- invent metadata conventions
- store project memory in `context_retrieval.md`
- store current task plans in `context_retrieval.md`
- duplicate skills inside `context_retrieval.md`
- duplicate full metadata index contents inside `context_retrieval.md`
- treat semantic search as source of truth
- overwrite an existing file unless explicitly allowed

---

## Final Rule

Your job is to create, inspect, or repair `context_retrieval.md`.

Define how agents find context.

Prefer metadata, IDs, layers, document types, tags, and links over guessing.

Keep retrieval separate from memory, plans, context packages, metadata indexes, and skills.

If required input is missing, ask only for the next necessary input.
