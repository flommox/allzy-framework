---
id: "allzy.framework.prompts.workspace.plan-md.universal"
title: "Plan MD Prompt — Universal"
artifact_type: "Prompt"
prompt_family: "Workspace"
prompt_variant: "Plan MD"
adaptation_target: "Universal"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - workspace
  - plan-md
  - universal
---

# `plan_md_prompt.md`

## Purpose

Use this prompt to create, update, inspect, or clean `plan.md` for an active AI-assisted project workspace.

`plan.md` is the current working focus for a project, implementation area, module, submodule, task, or agent session.

It answers:

```text
What is being worked on right now?
```

This prompt keeps `plan.md` short, current, actionable, and checkable.

It does not initialize the full workspace context layer.

It does not create `memory.md`.

It does not create `context_retrieval.md`.

It does not create metadata indexes.

It does not create skills.

It only works on `plan.md`.

---

## When to Use This Prompt

Use this prompt when:

- creating a new `plan.md` for a project, module, submodule, task, or implementation session
- updating `plan.md` from the current task context
- converting rough notes into a clean current plan
- cleaning an existing `plan.md`
- removing stale completed items from `plan.md`
- preserving active and blocked work
- creating a clear task focus before using a coding agent
- preparing a small handoff plan for another AI agent
- checking whether an existing `plan.md` is still usable

---

## When Not to Use This Prompt

Do not use this prompt to:

- create or update `memory.md`
- store confirmed long-term project truth
- create `context_retrieval.md`
- generate a context package
- generate or update a metadata index
- maintain skills
- write application code
- implement features
- fix bugs
- perform Triage
- generate a Master Document
- create Yin/Yang documents
- rewrite architecture
- manage a full backlog or roadmap
- store raw chat history
- store secrets

If the user asks for one of these tasks, explain that this prompt only creates, updates, inspects, or cleans `plan.md`.

---

## Config Block

This config block is always present.

If the config is filled, use it as **Preconfigured Mode**.

If the config is empty or incomplete, use **Assistant Mode** and ask only the next necessary question.

If the user manually edits the config before running the prompt, treat it exactly like website-generated config.

```yaml
---
plan_md_prompt_config:
  mode: "" # assistant | preconfigured

  operation: "" # generate_or_update | clean_existing | inspect_only
  target_artifact: "plan.md"
  target_path: "" # e.g. context/plan.md, .ai/context/plan.md, plan.md

  allow_file_creation: null # true | false
  allow_file_updates: null # true | false
  allow_overwrite: false
  allow_placeholder_repair: null # true | false

  target_exists: null # true | false | unknown
  existing_plan_provided: null # true | false
  current_task_input_provided: null # true | false

  plan_scope:
    project_name: ""
    module: ""
    submodule: ""
    task_id: ""
    task_title: ""
    current_focus: ""

  cleanup_policy:
    preserve_active_tasks: true
    preserve_blocked_tasks: true
    preserve_scope_boundaries: true
    preserve_acceptance_criteria: true
    remove_stale_completed_items: true
    remove_raw_chat_fragments: true
    remove_long_term_memory: true
    remove_broad_backlog: true

  output_style: "copy_ready" # copy_ready | report_only | patch_ready
  target_environment: "" # cursor | claude-code | codex-cli | chatgpt | gemini | other | unknown
---
```

---

## Operating Logic

This prompt supports three operations:

```text
generate_or_update
clean_existing
inspect_only
```

### `generate_or_update`

Use this operation when:

- no `plan.md` exists
- a new current working plan is needed
- rough task context should be converted into `plan.md`
- an existing plan should be updated with the current focus

If `plan.md` does not exist and file creation is allowed, create it.

If `plan.md` exists and updates are allowed, update it without erasing active or blocked work.

If `plan.md` exists but file updates are not allowed, return a copy-ready replacement or patch-style output.

---

### `clean_existing`

Use this operation when:

- an existing `plan.md` is too long
- completed items are stale
- old notes make the current work unclear
- raw chat fragments are present
- backlog items are mixed into the current plan
- memory-like content is stored in `plan.md`

This operation should preserve active and blocked work.

It should remove or compress stale, duplicated, completed, or misplaced content.

---

### `inspect_only`

Use this operation when:

- the user only wants a report
- file creation is not allowed
- file updates are not allowed
- the existing plan may be unsafe to modify
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
What should I do with plan.md?

1. Generate or update plan.md from the current task context
2. Clean an existing plan.md
3. Inspect only
```

### Question 2 — Input

Ask only for the needed input.

If generating:

```text
Please provide the current task context, goal, scope, and acceptance criteria. Rough notes are fine.
```

If cleaning:

```text
Please paste or attach the existing plan.md.
```

If inspecting:

```text
Please paste or attach the existing plan.md, or provide the target path if I have file access.
```

### Question 3 — File Permission

Ask only if file access exists and permission is unclear:

```text
May I create or update plan.md directly, or should I return copy-ready Markdown only?
```

---

## File Access Rule

If running in an environment with file access, inspect the target file directly.

If running in a normal chat without file access, ask the user to paste or attach the needed content.

Do not pretend to have read files that were not provided or accessible.

If `target_path` is missing and file access is needed, ask for the path.

Default target path if no path is provided:

```text
context/plan.md
```

---

## Security and Privacy Check

Before creating, updating, cleaning, or inspecting `plan.md`, check all provided content for secrets or sensitive operational data.

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
- internal URLs that should not be stored in planning state

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

Never store real secrets in `plan.md`.

---

## `plan.md` Role

`plan.md` is living current task state.

It should be short enough to be read before work begins.

It should not become a full project database.

It should not contain permanent project memory.

It should not contain broad backlog or roadmap planning.

It should not contain raw chat history.

It should not contain implementation diary content.

Long-term confirmed facts belong in `memory.md`.

Search and retrieval behavior belongs in `context_retrieval.md`.

Reusable agent lessons belong in `skills/`.

Temporary handoff context belongs in a context package.

---

## `plan.md` Must Contain

A useful `plan.md` should contain:

- current focus
- active task
- task goal
- current status checklist
- blocked or needs-input items
- scope boundaries
- acceptance criteria
- immediate next steps
- short maintenance notes if relevant

---

## `plan.md` Must Not Contain

Do not include:

- full backlog
- long-term roadmap
- raw chat logs
- permanent architecture memory
- old failed attempts unless still blocking current work
- unrelated notes
- speculative ideas
- detailed implementation history
- secrets
- duplicated context retrieval rules
- skills
- completed old work that no longer affects the current task

---

## Generation Rules

When generating `plan.md` from task context:

1. Extract the current focus.
2. Identify the active task.
3. Define what “done” means.
4. Convert requirements into checkable tasks.
5. Preserve explicit scope boundaries.
6. Preserve blocked items and missing decisions.
7. Add acceptance criteria.
8. Keep the plan concise.
9. Do not invent project decisions.
10. Mark uncertainty clearly.

If the user provides rough or messy input, normalize it into a clean plan.

If key information is missing but the plan can still be useful, proceed and include a `Needs Input` section.

If the missing information blocks the plan entirely, ask one targeted question.

---

## Update Rules

When updating an existing `plan.md`:

1. Preserve active tasks unless clearly superseded.
2. Preserve blocked tasks unless clearly resolved.
3. Preserve scope boundaries.
4. Preserve acceptance criteria that still apply.
5. Add new current task information.
6. Remove duplicated items.
7. Move stale or unclear items to `Needs Review`.
8. Do not reset the plan unless explicitly requested.
9. Do not convert the plan into memory.
10. Do not add broad backlog items.

If the existing plan conflicts with new task context, prefer the newer explicit instruction and mark the old item as superseded or needing review.

---

## Cleaning Rules

When cleaning an existing `plan.md`, classify content as:

```text
Current / active
→ keep

Blocked / needs input
→ keep, but compress if verbose

Recently completed and still useful
→ keep briefly in Recently Completed

Old completed
→ remove

Duplicated
→ merge

Backlog / roadmap
→ remove or mark out of scope

Memory-like project truth
→ remove from plan.md and suggest moving to memory.md

Retrieval rules
→ remove from plan.md and suggest moving to context_retrieval.md

Reusable agent lesson
→ remove from plan.md and suggest moving to skills/

Raw chat or implementation diary
→ remove unless it contains unresolved blocking context
```

Do not delete active or blocked work unless clearly obsolete.

---

## Required `plan.md` Output Shape

Use this structure unless the existing file has a stronger compatible structure.

```markdown
# Plan

_Last updated: YYYY-MM-DD_
_Status: Active_
_Cleanup status: OK | REVIEW_NEEDED | STALE_

## Current Focus

[Current active focus.]

## Active Task

### Goal

[What done means.]

### Status

- [ ] [Step]
- [ ] [Step]
- [ ] [Step]

## Blocked / Needs Input

- [ ] [Blocked item or missing decision.]

## Recently Completed

- [x] [Short completed item only if still useful.]

## Scope Boundaries

In scope:

- [Item]

Out of scope:

- [Item]

## Acceptance Criteria

- [ ] [Criterion]
- [ ] [Criterion]

## Immediate Next Steps

- [ ] [Next step]

## Maintenance Notes

- [Short note about generation, update, or cleanup.]
```

If no blocked items exist, write:

```markdown
## Blocked / Needs Input

- None currently known.
```

If no recently completed items are relevant, write:

```markdown
## Recently Completed

- None currently relevant.
```

---

## Date Rule

Use the current date for `_Last updated`.

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
- whether current task input is provided
- whether existing plan content is provided
- file creation permission
- file update permission
- output style

If config is incomplete, enter Assistant Mode.

---

### Step 2 — Determine Input Availability

For `generate_or_update`, require at least one of:

- current task context
- rough task notes
- implementation handoff
- module/submodule description
- existing `plan.md`

For `clean_existing`, require:

- existing `plan.md`

For `inspect_only`, require:

- existing `plan.md` or file access to target path

If required input is missing, ask only for that input.

---

### Step 3 — Check Scope

Verify that the request is about `plan.md`.

If the request is about another artifact, redirect:

```text
This prompt only handles plan.md. Use the appropriate artifact prompt for memory.md, context_retrieval.md, context packages, metadata indexes, or skills.
```

---

### Step 4 — Security Check

Inspect input for secrets.

Stop if unsafe.

Do not repeat secrets.

---

### Step 5 — Analyze Existing Plan or Task Context

Identify:

- current focus
- active task
- goal
- status items
- scope boundaries
- acceptance criteria
- blockers
- completed items
- stale content
- duplicated content
- misplaced memory
- misplaced backlog
- raw chat fragments
- unclear or conflicting items

---

### Step 6 — Produce Output

Depending on operation:

```text
generate_or_update
→ return full plan.md content

clean_existing
→ return full cleaned plan.md content

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
- what needs review
- what was not changed

---

## Required Output Format

Return exactly:

```markdown
# plan.md Result

## 1. Operation Used

[generate_or_update / clean_existing / inspect_only]

## 2. Target Artifact

[plan.md path or provided content]

## 3. Input Used

[Current task context / existing plan.md / both / missing input]

## 4. Output

```markdown
[full generated or updated plan.md content]
```

## 5. Change Summary

- Created:
- Updated:
- Preserved:
- Removed:
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
- create or update `memory.md`
- create or update `context_retrieval.md`
- create context packages
- create metadata indexes
- create or maintain skills
- store secrets
- claim file access when no file access exists
- invent project decisions
- convert broad backlog into current plan
- store long-term project truth in `plan.md`
- store raw chat history in `plan.md`
- delete active or blocked work unless clearly obsolete
- overwrite an existing file unless explicitly allowed

---

## Final Rule

Your job is to create, update, inspect, or clean `plan.md`.

Keep it current.

Keep it actionable.

Keep it short.

Keep active and blocked work.

Remove stale noise.

Do not turn `plan.md` into memory, backlog, retrieval rules, skills, or chat history.

If required input is missing, ask only for the next necessary input.
