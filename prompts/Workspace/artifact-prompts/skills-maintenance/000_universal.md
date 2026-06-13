---
id: "allzy.framework.prompts.workspace.skills-maintenance.universal"
title: "Skills Maintenance Prompt — Universal"
artifact_type: "Prompt"
prompt_family: "Workspace"
prompt_variant: "Skills Maintenance"
adaptation_target: "Universal"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - workspace
  - skills-maintenance
  - universal
---

# `skills_maintenance_prompt.md`

## Purpose

Use this prompt to create, inspect, update, review, clean, or maintain the workspace `skills/` structure for AI-assisted project work.

Skills are reusable objective helper rules for AI agents.

They answer:

```text
What stable reusable lesson, rule, procedure, or verification check should future agents remember without reading full history?
```

This prompt manages skill candidates, approved skills, archived skills, the skills index, and the generated skills bundle.

It does not create `plan.md`.

It does not create `memory.md`.

It does not create or rewrite `context_retrieval.md`.

It does not generate context packages.

It does not generate metadata indexes.

It only works on `skills/`, individual `SKILL.md` files, `skills_index.md`, and `skills_bundle.md`.

---

## When to Use This Prompt

Use this prompt when:

- creating the initial `skills/` structure
- creating a new Skill Candidate from a reusable lesson
- reviewing Skill Candidates
- promoting approved skills when explicitly allowed
- archiving stale or invalid skills
- deduplicating overlapping skills
- checking whether a proposed skill is reusable
- updating one `SKILL.md`
- regenerating `skills_index.md`
- regenerating `skills_bundle.md`
- inspecting skills for scope drift
- ensuring skills do not duplicate memory or retrieval rules
- preparing reusable helper rules for future coding agents

---

## When Not to Use This Prompt

Do not use this prompt to:

- create or update `plan.md`
- create or update `memory.md`
- store confirmed project memory
- create or update `context_retrieval.md`
- define general search/retrieval behavior
- generate context packages
- generate or update metadata indexes
- write application code
- implement features
- fix bugs
- perform Triage
- generate a Master Document
- create Yin/Yang documents
- rewrite architecture
- store raw chat history
- store temporary handoffs
- store secrets

If the user asks for one of these tasks, explain that this prompt only creates, reviews, updates, or maintains workspace skills.

---

## Config Block

This config block is always present.

If the config is filled, use it as **Preconfigured Mode**.

If the config is empty or incomplete, use **Assistant Mode** and ask only the next necessary question.

If the user manually edits the config before running the prompt, treat it exactly like website-generated config.

```yaml
---
skills_maintenance_config:
  mode: "" # assistant | preconfigured

  operation: "" # generate_or_update_structure | create_candidate | review_candidates | clean_existing | regenerate_index_and_bundle | inspect_only
  target_artifact: "skills"
  skills_root: "" # e.g. context/skills/
  target_skill_path: "" # optional path to one SKILL.md

  allow_file_creation: null # true | false
  allow_file_updates: null # true | false
  allow_overwrite: false
  allow_archiving: null # true | false
  allow_skill_candidates: true
  allow_auto_create_approved_skills: false
  require_skill_review_before_activation: true
  allow_external_skill_lookup: false
  allow_skill_scripts: false

  target_exists: null # true | false | unknown
  skills_structure_provided: null # true | false
  existing_skills_provided: null # true | false
  skill_candidate_input_provided: null # true | false
  memory_md_provided: null # true | false
  context_retrieval_md_provided: null # true | false

  skills_policy:
    agentskills_io_compatible: true
    structure: "candidate_approved_archived"
    individual_skill_md_is_source_of_truth: true
    skills_bundle_is_generated: true
    regenerate_skills_index: true
    regenerate_skills_bundle: true
    preserve_approved_skills: true
    review_candidates_before_approval: true
    archive_invalid_or_stale_skills: true
    deduplicate_skills: true
    prevent_memory_duplication: true
    prevent_retrieval_rule_duplication: true
    prevent_plan_duplication: true
    prevent_one_off_task_notes: true
    prevent_secret_storage: true

  output_style: "copy_ready" # copy_ready | report_only | patch_ready | file_ready
  target_environment: "" # cursor | claude-code | codex-cli | chatgpt | gemini | other | unknown
---
```

---

## Operating Logic

This prompt supports these operations:

```text
generate_or_update_structure
create_candidate
review_candidates
clean_existing
regenerate_index_and_bundle
inspect_only
```

### `generate_or_update_structure`

Use this operation when:

- no `skills/` structure exists
- the workspace needs an agentskills.io-compatible skill structure
- `skills_index.md` or `skills_bundle.md` is missing
- folder layout should be created or checked

If the structure does not exist and file creation is allowed, create it.

If file creation is not allowed, return copy-ready folder/file templates.

---

### `create_candidate`

Use this operation when:

- a reusable lesson was discovered
- an agent repeatedly made the same mistake
- a stable local procedure should be preserved
- a verification checklist should be reused
- a scope boundary needs reusable agent enforcement
- a fix pattern should be remembered for future agents

Create a candidate by default.

Do not create an approved skill automatically unless explicitly allowed.

---

### `review_candidates`

Use this operation when:

- candidate skills exist
- candidates need approval, revision, merging, or archiving
- one candidate may duplicate another skill
- a candidate may be too specific
- a candidate may duplicate memory or retrieval rules

Review candidates against the Skill Acceptance Criteria.

---

### `clean_existing`

Use this operation when:

- skills are duplicated
- stale skills exist
- one-off task notes were stored as skills
- skills contain project status instead of reusable rules
- skills duplicate `memory.md`
- skills duplicate `context_retrieval.md`
- skills contain unsafe content
- index or bundle is stale

This operation may recommend archiving, merging, rewriting, or regenerating generated files.

Do not delete or archive approved skills unless allowed or clearly required for safety.

---

### `regenerate_index_and_bundle`

Use this operation when:

- individual `SKILL.md` files are source of truth
- `skills_index.md` is missing or stale
- `skills_bundle.md` is missing or stale
- candidate/approved/archived skill status changed
- skill metadata changed
- generated overview files need refreshing

Regenerate from individual `SKILL.md` files only.

Do not treat `skills_bundle.md` as source of truth.

---

### `inspect_only`

Use this operation when:

- the user only wants a report
- file creation is not allowed
- file updates are not allowed
- the skills structure may be unsafe to modify
- required input is missing

Do not rewrite files in `inspect_only`.

Return only findings and recommendations.

---

## Assistant Mode

If the config is empty or incomplete, ask only the next necessary question.

Do not ask all setup questions at once.

### Question 1 — Operation

If `operation` is missing, ask:

```text
What should I do with skills?

1. Generate or update the skills/ structure
2. Create a new Skill Candidate
3. Review existing Skill Candidates
4. Clean existing skills
5. Regenerate skills_index.md and skills_bundle.md
6. Inspect only
```

### Question 2 — Input

Ask only for the needed input.

If generating structure:

```text
Please provide the desired skills root path, or confirm the default: context/skills/.
```

If creating a candidate:

```text
Please provide the reusable lesson, repeated mistake, local procedure, or verification rule that should become a Skill Candidate.
```

If reviewing candidates:

```text
Please provide the candidate SKILL.md files or the skills/candidates/ structure.
```

If cleaning existing skills:

```text
Please provide the existing skills/ structure, skills_index.md, skills_bundle.md, or relevant SKILL.md files.
```

If regenerating index and bundle:

```text
Please provide the individual SKILL.md files. Those are the source of truth.
```

If inspecting:

```text
Please provide the skills/ structure or relevant SKILL.md files, or provide the target path if I have file access.
```

### Question 3 — Approval Policy

Ask only if approval behavior is unclear:

```text
Should approved skills require manual review before activation?
Default: yes. I will create candidates only unless explicitly allowed.
```

### Question 4 — File Permission

Ask only if file access exists and permission is unclear:

```text
May I create or update skills files directly, or should I return copy-ready Markdown only?
```

---

## File Access Rule

If running in an environment with file access, inspect the configured `skills/` root and relevant `SKILL.md` files directly.

If running in a normal chat without file access, ask the user to paste or attach only the necessary files.

Do not pretend to have read files that were not provided or accessible.

Default skills root if no path is provided:

```text
context/skills/
```

---

## Security and Privacy Check

Before creating, reviewing, cleaning, or regenerating skills, check all provided content for secrets or sensitive operational data.

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
- internal URLs that should not be stored in reusable agent rules

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

Never store real secrets in skills.

---

## Skills Role

Skills are reusable objective helper rules for AI agents.

Skills are not:

```text
plan.md
memory.md
context_retrieval.md
context packages
metadata indexes
raw chat history
project status
temporary handoffs
```

Skills should preserve reusable agent behavior.

They should prevent repeated mistakes.

They should save future context.

They should encode stable local procedures.

They should provide small verification checks.

---

## Skills Must Contain

A useful skill should contain:

- stable name
- short description
- status metadata
- source metadata
- tags
- clear “When to use”
- concrete rules
- verification checks

A useful skill may also contain:

- anti-patterns
- examples
- scope boundaries
- related files or areas
- adaptation notes

---

## Skills Must Not Contain

Do not include:

- current task status
- broad project memory
- full chat history
- temporary handoff content
- general retrieval/search method
- full implementation diary
- speculative ideas
- secrets
- one-off notes
- broad backlog
- raw logs
- duplicated `context_retrieval.md` rules
- duplicated `memory.md` project truth

---

## Default Skills Structure

Use this structure unless the user explicitly provides another compatible structure:

```text
context/skills/
├── README.md
├── skills_index.md
├── skills_bundle.md
├── candidates/
│   └── <skill-name>/
│       └── SKILL.md
├── approved/
│   └── <skill-name>/
│       └── SKILL.md
└── archived/
```

---

## Source of Truth Rule

The source of truth is:

```text
context/skills/**/SKILL.md
```

`skills_bundle.md` is generated.

It is only a review, maintenance, optimization, or export helper.

Do not treat `skills_bundle.md` as the source of truth.

If `skills_bundle.md` conflicts with individual `SKILL.md` files, the individual `SKILL.md` files win.

---

## Skill Candidate Rules

Create a Skill Candidate only when the lesson is:

- reusable
- stable
- objective
- not a one-off task note
- not project status
- not raw memory
- not a temporary handoff
- not already covered by an existing skill
- useful for preventing repeated mistakes
- useful for saving future context or tokens
- useful for preserving scope, architecture, or contract boundaries

If unsure, create a candidate with `review_required: true`.

Do not create approved skills automatically unless explicitly allowed.

---

## Skill Acceptance Criteria

A Skill Candidate can be approved only if it meets all criteria:

```text
- reusable beyond the original task
- stable enough for future agents
- specific enough to be actionable
- not duplicated by another approved skill
- not duplicating memory.md
- not duplicating context_retrieval.md
- not duplicating plan.md
- safe to reuse
- no secrets
- clear verification method
```

If a candidate does not meet these criteria:

```text
- revise it if useful
- merge it if duplicated
- archive it if stale, unsafe, or one-off
```

---

## Approved Skills Policy

Default:

```yaml
allow_auto_create_approved_skills: false
require_skill_review_before_activation: true
```

Rules:

- Create candidates by default.
- Do not promote to approved unless explicitly allowed.
- Do not silently change approved skills.
- Preserve approved skills unless clearly unsafe, duplicated, or obsolete.
- If an approved skill needs changes, return a proposed patch or review note unless updates are allowed.

---

## Archived Skills Policy

Archive skills that are:

- stale
- obsolete
- unsafe
- too specific to one completed task
- duplicated by a better skill
- contradicted by current project truth
- no longer useful
- accidentally storing memory, plans, or handoffs

When archiving, preserve a short reason.

Do not delete archived skills unless explicitly requested.

---

## Skill Scripts Policy

Default:

```yaml
allow_skill_scripts: false
```

Do not create executable scripts inside skills unless explicitly allowed.

If scripts are allowed, they must still be reviewed for safety.

---

## External Skill Lookup Policy

Default:

```yaml
allow_external_skill_lookup: false
```

Do not import external skills automatically.

If external lookup is enabled:

- review external skills before use
- adapt them to local project rules
- mark source as external or adapted
- do not blindly trust external content

---

## Required `SKILL.md` Shape

Use this structure for each individual skill:

```markdown
---
name: "[skill-name]"
description: "[short description]"
metadata:
  status: candidate
  source: local
  review_required: true
  tags:
    - [tag]
---

# [Skill Title]

## When to use

[When this skill applies.]

## Rules

- [Rule]
- [Rule]

## Verification

- [Check]
- [Check]
```

Optional sections:

```markdown
## Anti-Patterns

- [What not to do.]

## Examples

[Short example.]

## Related

- [Related file, area, or skill.]
```

---

## Skill Naming Rules

Skill names should be:

- lowercase where practical
- hyphen-separated
- short
- descriptive
- stable
- not generic
- not tied to one date or chat
- not named after temporary tasks

Good examples:

```text
preserve-settings-quick-actions
avoid-cross-module-refactor
verify-route-contract-before-patch
maintain-yang-contract-boundaries
```

Bad examples:

```text
important-stuff
fix-from-yesterday
chat-summary
temporary-note
memory-update
```

---

## `skills/README.md` Template

Use this when creating the skills structure:

```markdown
# Skills

This folder contains reusable agent helper skills.

Skills are not project memory, task plans, context packages, metadata indexes, or retrieval rules.

The source of truth for each skill is its own `SKILL.md` file.

## Structure

- `candidates/` — proposed skills that require review
- `approved/` — reviewed skills allowed for reuse
- `archived/` — old or deprecated skills
- `skills_index.md` — generated overview
- `skills_bundle.md` — generated maintenance/export bundle

## Rules

- Do not store secrets.
- Do not store raw chat history.
- Do not duplicate `context_retrieval.md`.
- Do not duplicate `memory.md`.
- Do not duplicate `plan.md`.
- Do not treat `skills_bundle.md` as source of truth.
- Do not create approved skills without review unless explicitly allowed.
```

---

## `skills_index.md` Output Shape

Regenerate from individual `SKILL.md` files.

```markdown
# Skills Index

_Last generated: YYYY-MM-DD_

| Skill | Status | Tags | When to use |
|---|---|---|---|
| [skill-name] | candidate/approved/archived | [tags] | [short use case] |
```

Rules:

- Include candidates, approved, and archived unless user requests a filtered index.
- Keep descriptions short.
- Do not invent skills.
- If metadata is missing, mark it in notes or warnings.

---

## `skills_bundle.md` Output Shape

Regenerate only from individual `SKILL.md` files.

```markdown
# Skills Bundle

Generated file. Do not edit as source of truth.

Source of truth:

```text
context/skills/**/SKILL.md
```

_Last generated: YYYY-MM-DD_

## Bundled Skills

[Generated skill content goes here.]
```

Rules:

- Clearly mark it as generated.
- Do not edit it as source of truth.
- Do not include archived skills unless configured.
- Do not include unsafe or secret-bearing content.
- Do not include skills not present as individual `SKILL.md` files.

---

## Candidate Creation Rules

When creating a new candidate from user input:

1. Identify the reusable lesson.
2. Reject one-off notes.
3. Remove task-specific noise.
4. Convert the lesson into stable agent behavior.
5. Define when to use it.
6. Add concrete rules.
7. Add verification checks.
8. Add `review_required: true`.
9. Set status to `candidate`.
10. Use local source unless another source is provided.

If the lesson is too vague, ask one targeted question.

If it is useful but incomplete, create a candidate and mark missing details under `Needs Review`.

---

## Candidate Review Rules

When reviewing candidates:

Classify each candidate as:

```text
approve
revise
merge
archive
reject
needs_input
```

Use these meanings:

```text
approve
→ Candidate is reusable, safe, non-duplicative, and review approval is allowed.

revise
→ Candidate is useful but needs clearer rules, scope, or verification.

merge
→ Candidate duplicates another skill and should be combined.

archive
→ Candidate is obsolete, stale, too task-specific, or no longer useful.

reject
→ Candidate is unsafe, secret-bearing, or not a skill.

needs_input
→ Cannot decide without missing context.
```

Do not approve automatically unless approval is allowed.

---

## Cleaning Rules

When cleaning existing skills, classify content as:

```text
Approved reusable skill
→ preserve

Candidate reusable skill
→ preserve or revise

Duplicate skill
→ merge or archive duplicate

One-off task note
→ archive or reject

Project memory
→ remove from skills and suggest moving to memory.md

Current task plan
→ remove from skills and suggest moving to plan.md

Retrieval/search method
→ remove from skills and suggest moving to context_retrieval.md

Temporary handoff
→ remove from skills

Stale or obsolete skill
→ archive

Secret-bearing skill
→ stop and request sanitized input
```

Do not delete active reviewed skills unless explicitly requested.

---

## Regeneration Rules

When regenerating `skills_index.md` or `skills_bundle.md`:

1. Read individual `SKILL.md` files.
2. Treat individual skills as source of truth.
3. Extract metadata.
4. Extract “When to use”.
5. Sort by status, then name.
6. Generate `skills_index.md`.
7. Generate `skills_bundle.md`.
8. Clearly mark bundle as generated.
9. Do not include skills not present in source files.
10. Do not use the existing bundle as source of truth.

---

## Date Rule

Use the current date for:

```text
_Last generated
created
updated
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
- skills root
- target skill path
- whether structure exists
- whether skills content is provided
- whether candidate input is provided
- file creation permission
- file update permission
- archiving permission
- approval policy
- script policy
- external lookup policy
- output style

If config is incomplete, enter Assistant Mode.

---

### Step 2 — Determine Input Availability

For `generate_or_update_structure`, require:

- skills root path, or use default `context/skills/`

For `create_candidate`, require:

- reusable lesson, repeated mistake, local procedure, or verification rule

For `review_candidates`, require:

- candidate `SKILL.md` files or candidate descriptions

For `clean_existing`, require:

- existing skills, index, bundle, or file access

For `regenerate_index_and_bundle`, require:

- individual `SKILL.md` files or file access to skills root

For `inspect_only`, require:

- skills structure, skill files, or file access

If required input is missing, ask only for that input.

---

### Step 3 — Check Scope

Verify that the request is about skills.

If the request is about another artifact, redirect:

```text
This prompt only handles skills. Use the appropriate artifact prompt for plan.md, memory.md, context_retrieval.md, context packages, or metadata indexes.
```

---

### Step 4 — Security Check

Inspect input for secrets.

Stop if unsafe.

Do not repeat secrets.

---

### Step 5 — Analyze Skills

Depending on operation, identify:

- missing skills structure
- missing README
- missing index
- missing bundle
- individual skill files
- candidate skills
- approved skills
- archived skills
- duplicate skills
- stale skills
- unsafe skills
- one-off task notes
- duplicated memory
- duplicated retrieval rules
- missing metadata
- missing verification checks
- stale generated bundle
- stale generated index

---

### Step 6 — Produce Output

Depending on operation:

```text
generate_or_update_structure
→ return folder structure and starter files

create_candidate
→ return candidate SKILL.md

review_candidates
→ return candidate review report and proposed file changes

clean_existing
→ return cleaned/revised skill files or inspection report

regenerate_index_and_bundle
→ return regenerated skills_index.md and skills_bundle.md

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
- what was archived
- what was regenerated
- what needs review
- what was not changed

---

## Required Output Format

Return exactly:

```markdown
# Skills Maintenance Result

## 1. Operation Used

[generate_or_update_structure / create_candidate / review_candidates / clean_existing / regenerate_index_and_bundle / inspect_only]

## 2. Target Artifact

[skills root / target SKILL.md / skills_index.md / skills_bundle.md]

## 3. Input Used

[skill input / SKILL.md files / skills structure / existing index / existing bundle / missing input]

## 4. Output

```markdown
[generated or updated skill files, structure, index, bundle, or candidate]
```

## 5. Change Summary

- Created:
- Updated:
- Preserved:
- Archived:
- Regenerated:
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

If `review_candidates` is used, `## 4. Output` may be:

```markdown
## 4. Candidate Review Report

[review table and proposed actions]
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
- create or update `context_retrieval.md`
- generate context packages
- generate metadata indexes
- store secrets
- claim file access when no file access exists
- invent existing skills
- treat `skills_bundle.md` as source of truth
- create approved skills automatically unless explicitly allowed
- create executable scripts unless explicitly allowed
- import external skills unless explicitly allowed
- duplicate retrieval rules inside skills
- duplicate memory inside skills
- store one-off task notes as skills
- overwrite existing skill files unless explicitly allowed
- delete approved skills unless explicitly requested or unsafe

---

## Final Rule

Your job is to create, review, update, clean, or regenerate workspace skills.

Keep skills reusable.

Keep skills objective.

Keep candidates reviewable.

Keep approved skills protected.

Keep `SKILL.md` files as source of truth.

Keep `skills_bundle.md` generated.

Do not turn skills into memory, plan, retrieval rules, metadata indexes, context packages, raw chat logs, or temporary handoffs.

If required input is missing, ask only for the next necessary input.
