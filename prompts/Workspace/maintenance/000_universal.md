---
id: "allzy.framework.prompts.workspace.workspace-state-maintenance.universal"
title: "Workspace State Maintenance Prompt — Universal"
artifact_type: "Prompt"
prompt_family: "Workspace"
prompt_variant: "Workspace State Maintenance"
adaptation_target: "Universal"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - workspace
  - workspace-state-maintenance
  - universal
---

# Workspace State Maintenance Prompt

## Purpose

Use this prompt to clean, compress, update, or review the active workspace state files created or managed by the Allzy Framework workspace context system.

This prompt is for maintaining living workspace state.

It does not initialize a workspace.

It does not write application code.

It does not fix bugs.

It does not perform Triage.

It does not rewrite framework templates.

It only maintains active workspace context files such as:

- `plan.md`
- `memory.md`
- `skills/`
- `skills_index.md`
- `skills_bundle.md`

---

## Core Principle

Only living state should be cleaned regularly.

Living state changes over time and can become stale, duplicated, too long, or misleading.

Stable method files and templates should not be cleaned as part of normal maintenance.

---

## What This Prompt Maintains

Primary maintenance targets:

```text
plan.md
memory.md
skills/
skills_index.md
skills_bundle.md
```

Optional health-check targets:

```text
context_retrieval.md
metadata_index.md
metadata_index.json
context packages
search logs
```

Optional targets are checked only when provided or explicitly requested.

They are not rewritten by default.

---

## What This Prompt Must Not Maintain by Default

Do not clean or rewrite these unless explicitly requested:

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

`AGENTS.md` and `agenten.md` are outside this prompt’s scope unless the user explicitly adds them.

---

## Config Block

This config block is always present.

If filled, use it as Preconfigured Mode.

If empty or incomplete, use Assistant Mode and ask only for the next required file or decision.

```yaml
---
workspace_state_maintenance_config:
  mode: "" # assistant | preconfigured
  maintenance_profile: "" # plan_only | memory_only | skills_only | full_state | inspect_only | custom

  target_file_type: "" # plan | memory | skills_index | skills_bundle | skill | unknown
  target_path: ""
  allow_rewrite: null # true | false
  allow_compression: null # true | false
  allow_archiving: null # true | false
  allow_skill_changes: null # true | false

  process_one_file_at_a_time: true
  max_files_per_run: 1

  plan_policy:
    remove_completed_old_items: true
    keep_current_active_items: true
    keep_blocked_items: true
    keep_recent_context: true
    age_based_cleanup: true

  memory_policy:
    compress_confirmed_history: true
    remove_duplicates: true
    remove_stale_or_superseded_entries: true
    preserve_current_truth: true
    preserve_useful_troubleshooting_notes: true
    preserve_contract_relevant_notes: true

  skills_policy:
    review_candidates: true
    deduplicate_skills: true
    preserve_approved_skills: true
    archive_stale_skills: true
    regenerate_skills_index: true
    regenerate_skills_bundle: true
    agentskills_io_compatible: true

  cleanup_metadata:
    update_last_maintenance: true
    update_last_compressed: true
    update_entries_since_maintenance: true
    update_rounds_since_compression: true
    update_cleanup_status: true
    update_compression_status: true

  output_delivery:
    output_mode: "copy_ready_markdown" # copy_ready_markdown | downloadable_file | patch_file | report_only
    requested_filename: ""
---
```

---

## Assistant Mode

If no file content is provided, ask for one file at a time.

Do not ask for all files at once.

Start with the most likely target.

Ask:

```text
Which workspace state file should I maintain first?

1. plan.md
2. memory.md
3. skills_index.md / skills_bundle.md
4. one SKILL.md file
5. inspect only
```

Then ask the user to paste or attach that file.

If the user provides multiple files at once, process only the first selected primary file unless the config explicitly allows multi-file maintenance.

If the provided file is not a living state file, explain that it does not need regular cleanup.

---

## Preconfigured Mode

If config and file content are provided:

1. Identify the file type.
2. Verify it is in scope.
3. Perform the requested maintenance.
4. Return the cleaned file or report.
5. List what was changed and why.

Do not ask redundant questions.

---

## File Access Rule

If running in an environment with file access, inspect the target files directly.

If running in a normal chat without file access, ask the user to provide the file content.

If the user has not provided the required file, ask for it.

Do not pretend to have read files that were not provided.

---

## Security and Privacy Check

Before maintaining any file, inspect it for secrets.

Secrets include:

- API keys
- passwords
- tokens
- private credentials
- database URLs
- session secrets
- private user/customer data
- unredacted logs
- private infrastructure values

If secrets are present:

1. Stop.
2. Do not repeat the secret.
3. Tell the user to sanitize the file.
4. Replace examples only with placeholders if needed.

Use placeholders such as:

```text
process.env.API_KEY
process.env.DATABASE_URL
$ENV_SESSION_SECRET
```

Never preserve real secrets in maintained output.

---

## Maintenance Profiles

### `plan_only`

Maintain only `plan.md`.

Use this for current task cleanup.

### `memory_only`

Maintain only `memory.md`.

Use this for compression, deduplication, and stale-truth cleanup.

### `skills_only`

Maintain only `skills/`, `skills_index.md`, `skills_bundle.md`, or one `SKILL.md`.

Use this for Skill Candidate review, deduplication, indexing, or bundle regeneration.

### `full_state`

Maintain the active state set, but still one file at a time unless file access is available and the user explicitly allows multi-file processing.

### `inspect_only`

Only report problems.

Do not rewrite.

### `custom`

Use explicit config choices.

---

## `plan.md` Maintenance Rules

`plan.md` is the current working focus.

It should be short, current, actionable, and checkable.

### Keep

Keep:

- active tasks
- blocked tasks
- immediate next steps
- current scope boundaries
- current acceptance criteria
- recent context still needed for execution
- unresolved items still relevant to the current work

### Remove or Archive

Remove or archive:

- completed old items
- stale tasks
- outdated “next steps”
- old context that no longer affects current work
- duplicated task entries
- broad backlog items
- old discussion notes
- raw chat fragments
- implementation diary content

### Age-Based Cleanup

Apply age-based cleanup when dates or status markers exist:

```text
Current / active
→ keep

Recently completed
→ summarize briefly or move to completed summary

Old completed
→ remove from plan.md

Stale / unclear
→ move to "Needs Review" or ask before deleting

Blocked
→ keep if still relevant, but compress
```

Do not delete active or blocked work unless clearly obsolete.

### Required `plan.md` Output Shape

Use this structure unless the existing file has a stronger compatible structure:

```markdown
# Plan

_Last maintained: YYYY-MM-DD_
_Cleanup status: OK | REVIEW_NEEDED | STALE_

## Current Focus

[Current active focus.]

## Active Tasks

- [ ] [Task]
- [ ] [Task]

## Blocked / Needs Input

- [ ] [Blocked item and needed decision]

## Recently Completed

- [x] [Short completed item, only if still useful]

## Scope Boundaries

In scope:

- [Item]

Out of scope:

- [Item]

## Acceptance Criteria

- [ ] [Criterion]

## Maintenance Notes

- Removed stale completed items older than current relevance window.
- Preserved active and blocked items.
```

---

## `memory.md` Maintenance Rules

`memory.md` is confirmed project truth.

It should preserve what is currently true and useful.

### Keep

Keep:

- current project facts
- current architecture decisions
- confirmed behavior
- current file/contract relationships
- useful troubleshooting notes that prevent repeated mistakes
- important “already tried / ineffective” notes while an issue remains unresolved
- contract-relevant history
- latest superseding decision

### Compress

Compress:

- long histories into short current-state summaries
- repeated notes
- multiple entries describing the same decision
- old troubleshooting into one useful note
- verbose implementation history into confirmed outcome + why it matters

### Remove or Mark Superseded

Remove or mark:

- stale decisions
- duplicated entries
- old truth replaced by newer truth
- raw chat history
- speculative reasoning
- resolved issue details no longer useful
- outdated implementation attempts
- unrelated notes

### Required Maintenance Metadata

`memory.md` should include or update:

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
cleanup_status: "OK | REVIEW_NEEDED | STALE | OVERGROWN"
compression_status: "OK | NEEDED | DONE | REVIEW_NEEDED"
tags:
  - state
  - memory
---
```

### Compression Thresholds

Use these thresholds unless the file defines stricter ones:

```text
0–9 new entries/rounds since compression
→ OK

10–19 new entries/rounds since compression
→ compression recommended

20+ new entries/rounds since compression
→ compression required
```

When compression is performed:

```text
last_compressed = today
rounds_since_compression = 0
compression_status = DONE
```

When only minor cleanup is performed:

```text
last_maintenance = today
entries_since_maintenance = 0
cleanup_status = OK
```

---

## `skills/` Maintenance Rules

Skills are reusable objective helper rules for AI agents.

Skills are not memory.

Skills are not plan.

Skills are not context retrieval.

Skills are not temporary handoffs.

### Maintain

Maintain:

- `skills/candidates/**/SKILL.md`
- `skills/approved/**/SKILL.md`
- `skills/archived/**/SKILL.md`
- `skills_index.md`
- `skills_bundle.md`

### Skill Source of Truth

Each individual `SKILL.md` is source of truth.

`skills_bundle.md` is generated.

Do not treat `skills_bundle.md` as source of truth.

### Candidate Review

A Skill Candidate may be promoted only if it is:

- reusable
- stable
- not a one-off task note
- not project status
- not duplicated by another skill
- not duplicating `context_retrieval.md`
- useful for preventing repeated mistakes or saving future context

### Archive

Archive skills that are:

- stale
- too specific to one completed task
- duplicated by a better approved skill
- unsafe
- obsolete
- not reusable

### `SKILL.md` Requirements

Each `SKILL.md` should contain:

```yaml
---
name:
description:
metadata:
  status: candidate | approved | archived
  source: local | external | adapted
  review_required: true | false
  tags:
    - tag
---
```

And body sections:

```markdown
# [Skill Title]

## When to use

[When this skill applies.]

## Rules

- [Rule]

## Verification

- [Check]
```

### `skills_index.md`

Regenerate from individual `SKILL.md` files.

It should contain:

```markdown
# Skills Index

_Last generated: YYYY-MM-DD_

| Skill | Status | Tags | When to use |
|---|---|---|---|
| [skill-name] | candidate/approved/archived | [tags] | [short use case] |
```

### `skills_bundle.md`

Regenerate only as maintenance/export helper.

It must clearly state:

```markdown
# Skills Bundle

Generated file. Do not edit as source of truth.

Source of truth:

context/skills/**/SKILL.md
```

---

## Optional Health Checks

These are not regular cleanup targets.

Check them only if provided or explicitly requested.

### `context_retrieval.md`

Check only:

- exists
- clearly defines retrieval method
- does not contain project memory
- does not contain secrets
- does not duplicate skills
- still matches metadata conventions

Do not rewrite it unless explicitly requested.

### Metadata Index

Check only:

- appears generated from actual documents
- has no obvious stale entries
- has no secrets
- format is still useful

Regenerate only if explicitly requested and source documents are available.

### Context Packages

Check only:

- old packages are not being treated as memory
- confirmed lasting facts were transferred to `memory.md` if needed
- obsolete packages can be archived if requested

### Search Logs

Check only:

- logs are not being treated as memory
- logs contain no secrets
- old logs may be archived if requested

---

## Processing Rule: One File at a Time

Default:

```text
process_one_file_at_a_time: true
```

Reason:

- avoids context overload
- avoids accidental cross-file rewriting
- works better in normal chat assistants
- allows user to paste files one by one
- reduces risk of deleting useful state

If multiple files are provided, choose this order:

```text
1. plan.md
2. memory.md
3. skills_index.md
4. skills_bundle.md
5. individual SKILL.md files
```

Then ask before continuing to the next file.

Exception: In a file-access IDE/CLI agent, multi-file maintenance is allowed only if explicitly configured.

---

## Maintenance Protocol

### Step 1 — Resolve Config

Read the config.

Determine:

- maintenance profile
- target file type
- file access status
- rewrite permission
- compression permission
- archive permission
- skill-change permission

If missing, ask only the next required question.

### Step 2 — Request Required File

If file content is not provided and no file access exists, ask for the file.

Example:

```text
Please paste or attach `plan.md`. I will clean only that file first.
```

### Step 3 — Identify File Type

Identify whether the provided file is:

```text
plan.md
memory.md
skills_index.md
skills_bundle.md
SKILL.md
other
```

If it is not a regular maintenance target, explain that it does not need cleanup by default.

### Step 4 — Security Check

Check for secrets.

Stop if unsafe.

### Step 5 — Analyze Current State

Identify:

- stale content
- duplicates
- completed items
- active items
- blocked items
- outdated truths
- superseded entries
- missing maintenance metadata
- overgrown sections
- unclear items needing review

### Step 6 — Produce Cleaned Output

Return the cleaned file in full.

Do not provide only partial edits unless requested.

### Step 7 — Explain Changes

Briefly list:

- what was kept
- what was removed
- what was compressed
- what needs user review
- what metadata was updated

### Step 8 — Ask Whether to Continue

If more files are likely needed, ask for the next one.

Example:

```text
Next recommended file: memory.md. Paste it when ready.
```

---

## Required Output Format

Return exactly:

```markdown
# Workspace State Maintenance Result

## 1. File Processed

[filename / file type]

## 2. Action Taken

[cleaned / compressed / inspected only / rejected / not in scope]

## 3. Cleaned File

```markdown
[full cleaned file content]
```

## 4. Change Summary

- Kept:
- Removed:
- Compressed:
- Updated metadata:
- Needs review:

## 5. Warnings / Blockers

- [warning or blocker]

## 6. Next Recommended File

[filename or None]
```

If only inspection was allowed, replace `Cleaned File` with `Inspection Report`.

---

## Hard Boundaries

Do not:

- write application code
- fix bugs
- perform Triage
- rewrite framework templates
- rewrite `context_retrieval.md` by default
- treat `context_retrieval.md` as memory
- treat `skills_bundle.md` as source of truth
- delete active or blocked plan items
- delete current confirmed memory
- preserve stale memory as current truth
- store secrets
- process many files at once unless explicitly allowed
- modify files that were not provided or accessible
- claim file access when no file access exists

---

## Final Rule

Maintain only living workspace state.

Clean one file at a time by default.

Keep active work.

Compress old truth.

Remove stale noise.

Preserve useful lessons.

Keep skills reusable.

Do not touch stable method/template files unless explicitly requested.

If the needed file is missing, ask for it.

Begin by resolving the config and requesting the first required file.
