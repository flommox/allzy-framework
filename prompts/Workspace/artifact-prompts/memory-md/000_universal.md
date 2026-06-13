---
id: "allzy.framework.prompts.workspace.memory-md.universal"
title: "Memory MD Prompt — Universal"
artifact_type: "Prompt"
prompt_family: "Workspace"
prompt_variant: "Memory MD"
adaptation_target: "Universal"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - workspace
  - memory-md
  - universal
---

# `memory_md_prompt.md`

## Purpose

Use this prompt to create, update, inspect, compress, or clean `memory.md` for an active AI-assisted project workspace.

`memory.md` is confirmed project memory.

It answers:

```text
What is currently true about this project or area?
```

This prompt preserves current project truth, confirmed architecture decisions, useful implementation facts, contract-relevant changes, and compact troubleshooting notes that prevent repeated mistakes.

It does not create `plan.md`.

It does not create `context_retrieval.md`.

It does not generate context packages.

It does not generate metadata indexes.

It does not create or maintain skills.

It only works on `memory.md`.

---

## When to Use This Prompt

Use this prompt when:

- creating a new `memory.md`
- updating `memory.md` with confirmed project facts
- adding confirmed architecture decisions
- preserving important changed behavior
- compressing long project history into current truth
- deduplicating repeated memory entries
- removing stale or superseded decisions
- preserving useful troubleshooting notes
- cleaning raw chat fragments out of memory
- preparing persistent memory for future AI agents
- checking whether an existing `memory.md` is still usable

---

## When Not to Use This Prompt

Do not use this prompt to:

- create or update `plan.md`
- define the current active task
- create `context_retrieval.md`
- define search or retrieval rules
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
- store raw chat history
- store temporary handoff context
- store secrets

If the user asks for one of these tasks, explain that this prompt only creates, updates, inspects, compresses, or cleans `memory.md`.

---

## Config Block

This config block is always present.

If the config is filled, use it as **Preconfigured Mode**.

If the config is empty or incomplete, use **Assistant Mode** and ask only the next necessary question.

If the user manually edits the config before running the prompt, treat it exactly like website-generated config.

```yaml
---
memory_md_prompt_config:
  mode: "" # assistant | preconfigured

  operation: "" # generate_or_update | compress_or_clean_existing | inspect_only
  target_artifact: "memory.md"
  target_path: "" # e.g. context/memory.md, .ai/context/memory.md, memory.md

  allow_file_creation: null # true | false
  allow_file_updates: null # true | false
  allow_overwrite: false
  allow_placeholder_repair: null # true | false

  target_exists: null # true | false | unknown
  existing_memory_provided: null # true | false
  confirmed_context_input_provided: null # true | false

  memory_scope:
    project_name: ""
    module: ""
    submodule: ""
    area: ""
    source_context: "" # notes | docs | implementation_result | review | handoff | mixed | unknown

  compression_policy:
    preserve_current_truth: true
    preserve_architecture_decisions: true
    preserve_contract_relevant_notes: true
    preserve_useful_troubleshooting_notes: true
    preserve_latest_superseding_decision: true
    remove_duplicates: true
    remove_raw_chat_fragments: true
    remove_speculation: true
    remove_stale_or_superseded_entries: true
    remove_temporary_handoffs: true

  maintenance_metadata:
    use_frontmatter: true
    update_last_maintenance: true
    update_last_compressed: true
    reset_rounds_since_compression_when_compressed: true
    reset_entries_since_maintenance_when_cleaned: true

  output_style: "copy_ready" # copy_ready | report_only | patch_ready
  target_environment: "" # cursor | claude-code | codex-cli | chatgpt | gemini | other | unknown
---
```

---

## Operating Logic

This prompt supports three operations:

```text
generate_or_update
compress_or_clean_existing
inspect_only
```

### `generate_or_update`

Use this operation when:

- no `memory.md` exists
- a new persistent project memory file is needed
- confirmed project facts should be added
- confirmed architecture decisions should be preserved
- implementation results should be converted into stable memory
- useful troubleshooting notes should be stored compactly

If `memory.md` does not exist and file creation is allowed, create it.

If `memory.md` exists and updates are allowed, update it without erasing current confirmed truth.

If `memory.md` exists but file updates are not allowed, return a copy-ready replacement or patch-style output.

---

### `compress_or_clean_existing`

Use this operation when:

- existing `memory.md` is too long
- repeated entries exist
- stale decisions remain as current truth
- superseded decisions are not clearly marked
- old implementation history is too verbose
- raw chat fragments are present
- temporary handoffs are mixed into memory
- context retrieval rules are mixed into memory
- skills are mixed into memory

This operation should preserve current confirmed truth.

It should compress history into usable present-state memory.

---

### `inspect_only`

Use this operation when:

- the user only wants a report
- file creation is not allowed
- file updates are not allowed
- the existing memory may be unsafe to modify
- required context is missing

Do not rewrite the file in `inspect_only`.

Return only findings and recommendations.

---

## Assistant Mode

If the config is empty or incomplete, ask only the next necessary question.

Do not ask all setup questions at once.

### Question 1 — Operation

If `operation` is missing, ask:

```text
What should I do with memory.md?

1. Generate or update memory.md from confirmed project context
2. Compress or clean an existing memory.md
3. Inspect only
```

### Question 2 — Input

Ask only for the needed input.

If generating or updating:

```text
Please provide the confirmed project facts, decisions, changes, or troubleshooting notes that should become memory.
```

If compressing or cleaning:

```text
Please paste or attach the existing memory.md.
```

If inspecting:

```text
Please paste or attach the existing memory.md, or provide the target path if I have file access.
```

### Question 3 — File Permission

Ask only if file access exists and permission is unclear:

```text
May I create or update memory.md directly, or should I return copy-ready Markdown only?
```

---

## File Access Rule

If running in an environment with file access, inspect the target file directly.

If running in a normal chat without file access, ask the user to paste or attach the needed content.

Do not pretend to have read files that were not provided or accessible.

If `target_path` is missing and file access is needed, ask for the path.

Default target path if no path is provided:

```text
context/memory.md
```

---

## Security and Privacy Check

Before creating, updating, compressing, cleaning, or inspecting `memory.md`, check all provided content for secrets or sensitive operational data.

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
- internal URLs that should not be stored in persistent state

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

Never store real secrets in `memory.md`.

---

## `memory.md` Role

`memory.md` is living confirmed project truth.

It is not the current task plan.

It is not a backlog.

It is not the retrieval method.

It is not a context package.

It is not a skill library.

It is not raw chat history.

It should preserve only information that helps future agents understand what is currently true, what decisions are binding, what changed, and what mistakes should not be repeated.

---

## `memory.md` Must Contain

A useful `memory.md` may contain:

- current project facts
- current architecture decisions
- current file or contract relationships
- confirmed implementation outcomes
- relevant behavior changes
- important constraints
- useful troubleshooting notes
- “already tried / ineffective” notes while an issue remains unresolved
- compact summaries of previous decisions that still matter
- latest superseding decisions

---

## `memory.md` Must Not Contain

Do not include:

- full chat history
- raw reasoning logs
- speculative ideas
- temporary handoffs
- current active task checklist
- full backlog
- search and retrieval method
- context package content
- skill definitions
- duplicated plan content
- stale decisions as current truth
- secrets
- verbose implementation diary
- old failed attempts that no longer help

---

## Required Maintenance Metadata

`memory.md` should include or update this frontmatter unless the existing file has a stronger compatible metadata structure:

```yaml
---
id: "state.memory"
title: "Project Memory"
document_type: "State File"
status: "Active"
updated: "YYYY-MM-DD"
last_maintenance: "YYYY-MM-DD"
last_compressed: "YYYY-MM-DD"
entries_since_maintenance: 0
rounds_since_compression: 0
cleanup_status: "OK"
compression_status: "OK"
tags:
  - state
  - memory
---
```

If compression was performed:

```text
last_compressed = current date
rounds_since_compression = 0
compression_status = DONE
```

If only minor cleanup was performed:

```text
last_maintenance = current date
entries_since_maintenance = 0
cleanup_status = OK
```

If the file is too large or unclear and cannot be safely compressed:

```text
cleanup_status = REVIEW_NEEDED
compression_status = REVIEW_NEEDED
```

---

## Compression Thresholds

Use these thresholds unless the existing file defines stricter ones:

```text
0–9 new entries or rounds since compression
→ OK

10–19 new entries or rounds since compression
→ compression recommended

20+ new entries or rounds since compression
→ compression required
```

When compression is required and allowed, compress.

When compression is required but not allowed, report the issue and recommend compression.

---

## Generation Rules

When generating `memory.md` from confirmed context:

1. Extract only confirmed facts.
2. Separate current state from decision history.
3. Preserve architecture decisions as current truth.
4. Preserve contract-relevant notes.
5. Preserve useful troubleshooting notes.
6. Exclude speculation.
7. Exclude unresolved guesses unless marked as open questions.
8. Exclude raw chat fragments.
9. Exclude current plan tasks unless they represent stable confirmed context.
10. Mark uncertainty clearly.

If the user provides rough or messy input, normalize it into stable memory.

If input contains both confirmed and speculative content, include only confirmed content and list speculative content under `Needs Review` or omit it.

Do not invent project decisions.

---

## Update Rules

When updating an existing `memory.md`:

1. Preserve current confirmed truth.
2. Add new confirmed facts.
3. Merge duplicates.
4. Prefer latest explicit decision when older entries conflict.
5. Mark or remove superseded entries.
6. Compress verbose history into current-state summaries.
7. Keep useful troubleshooting notes if they prevent repeated mistakes.
8. Remove temporary handoffs.
9. Remove plan-only tasks.
10. Remove retrieval rules.
11. Remove skill definitions.
12. Preserve unresolved “already tried” notes while the issue remains unresolved.

If new input conflicts with existing memory, do not silently overwrite.

Instead:

```text
- If new input is explicit and clearly newer, preserve the new truth and mark the old entry as superseded.
- If conflict cannot be resolved, place it under Needs Review.
```

---

## Cleaning and Compression Rules

When cleaning or compressing `memory.md`, classify content as:

```text
Current confirmed truth
→ keep

Current architecture decision
→ keep

Latest superseding decision
→ keep and remove/mark older versions

Contract-relevant note
→ keep

Useful unresolved troubleshooting note
→ keep, but compress

Resolved troubleshooting detail
→ compress or remove unless still useful

Duplicate memory
→ merge

Temporary handoff
→ remove

Plan/task checklist
→ remove or suggest moving to plan.md

Retrieval/search method
→ remove or suggest moving to context_retrieval.md

Reusable agent lesson
→ remove or suggest moving to skills/

Raw chat or transcript
→ remove unless it contains a confirmed decision not stored elsewhere

Speculation
→ remove or mark Needs Review

Secret
→ stop and request sanitized input
```

Do not remove current confirmed memory unless clearly obsolete or superseded.

---

## Required `memory.md` Output Shape

Use this structure unless the existing file has a stronger compatible structure.

```markdown
---
id: "state.memory"
title: "Project Memory"
document_type: "State File"
status: "Active"
updated: "YYYY-MM-DD"
last_maintenance: "YYYY-MM-DD"
last_compressed: "YYYY-MM-DD"
entries_since_maintenance: 0
rounds_since_compression: 0
cleanup_status: "OK"
compression_status: "OK"
tags:
  - state
  - memory
---

# Memory

## Current Project State

[Confirmed current truth about the project.]

## Architecture Decisions

[Confirmed architecture decisions.]

## Confirmed Changes

### YYYY-MM-DD — [Short title]

**Status:** Confirmed  
**Reason:** [Why this changed or matters.]  
**Changed:** [What changed.]  
**Files affected:** [Files or areas.]  
**Contracts affected:** [Contracts or docs.]  
**Verification:** [How it was checked.]

## Useful Troubleshooting Notes

[Only compact notes that still help.]

## Superseded / Historical Notes

[Only if still useful. Keep short.]

## Needs Review

[Unresolved conflicts or uncertain entries.]
```

If no reviewed conflicts exist, write:

```markdown
## Needs Review

- None currently known.
```

If no historical notes are useful, omit `Superseded / Historical Notes`.

---

## Date Rule

Use the current date for:

```text
updated
last_maintenance
last_compressed when compression was performed
```

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
- whether confirmed context input is provided
- whether existing memory content is provided
- file creation permission
- file update permission
- compression policy
- output style

If config is incomplete, enter Assistant Mode.

---

### Step 2 — Determine Input Availability

For `generate_or_update`, require at least one of:

- confirmed project facts
- confirmed decisions
- confirmed implementation result
- review result
- troubleshooting notes
- existing `memory.md`

For `compress_or_clean_existing`, require:

- existing `memory.md`

For `inspect_only`, require:

- existing `memory.md` or file access to target path

If required input is missing, ask only for that input.

---

### Step 3 — Check Scope

Verify that the request is about `memory.md`.

If the request is about another artifact, redirect:

```text
This prompt only handles memory.md. Use the appropriate artifact prompt for plan.md, context_retrieval.md, context packages, metadata indexes, or skills.
```

---

### Step 4 — Security Check

Inspect input for secrets.

Stop if unsafe.

Do not repeat secrets.

---

### Step 5 — Analyze Existing Memory or Confirmed Context

Identify:

- confirmed current truth
- architecture decisions
- confirmed changes
- file or contract relationships
- useful troubleshooting notes
- stale content
- duplicated content
- superseded content
- speculative content
- raw chat fragments
- misplaced plan content
- misplaced retrieval rules
- misplaced skills
- secrets
- unclear or conflicting entries

---

### Step 6 — Produce Output

Depending on operation:

```text
generate_or_update
→ return full memory.md content

compress_or_clean_existing
→ return full cleaned/compressed memory.md content

inspect_only
→ return inspection report only
```

Do not return only partial edits unless `output_style` is `patch_ready`.

---

### Step 7 — Explain Changes

Briefly list:

- what was created
- what was updated
- what was preserved
- what was removed
- what was compressed
- what needs review
- what was not changed

---

## Required Output Format

Return exactly:

```markdown
# memory.md Result

## 1. Operation Used

[generate_or_update / compress_or_clean_existing / inspect_only]

## 2. Target Artifact

[memory.md path or provided content]

## 3. Input Used

[confirmed context / existing memory.md / both / missing input]

## 4. Output

```markdown
[full generated or updated memory.md content]
```

## 5. Change Summary

- Created:
- Updated:
- Preserved:
- Removed:
- Compressed:
- Needs review:

## 6. Warnings / Blockers

- [Warning, blocker, or None]

## 7. Recommended Next Step

[Next action]
```

If `inspect_only` is used, replace `## 4. Output` with:

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
- create or update `context_retrieval.md`
- create context packages
- create metadata indexes
- create or maintain skills
- store secrets
- claim file access when no file access exists
- invent project decisions
- store current task checklist in `memory.md`
- store broad backlog in `memory.md`
- store raw chat history in `memory.md`
- store retrieval rules in `memory.md`
- store skill definitions in `memory.md`
- preserve stale memory as current truth
- remove current confirmed truth unless clearly obsolete or superseded
- overwrite an existing file unless explicitly allowed

---

## Final Rule

Your job is to create, update, inspect, compress, or clean `memory.md`.

Preserve current truth.

Compress old history.

Remove stale noise.

Keep useful troubleshooting notes.

Do not turn `memory.md` into a plan, backlog, retrieval method, context package, skills folder, or chat transcript.

If required input is missing, ask only for the next necessary input.
