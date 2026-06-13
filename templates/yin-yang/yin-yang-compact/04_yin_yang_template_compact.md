---
id: "allzy.framework.templates.yin-yang.yin-yang-compact"
title: "04 — Yin/Yang Compact Template"
artifact_type: "Template"
template_family: "yin-yang.yin-yang-compact"
status: "Draft"
version: "0.2.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - template
  - yin-yang
  - yin-yang-compact
  - compact
---

# 04 — Yin/Yang Compact Template

## What Is Yin/Yang Compact?

**Yin/Yang Compact** is a compact single-file specification for small executable tasks that need more structure than a Direct Scoped Prompt but do not require a full Yang Core Module.

It contains:

- a compact **Yin** section for human intent
- a compact **Yang** section for execution rules

Yin/Yang Compact is not standalone Yang Compact.

There is no standalone **Yang Compact** artifact.

---

## When to Use This Template

Use this compact template only when the task is:

- small
- self-contained
- low-risk
- clearly scoped
- executable
- unlikely to affect architecture
- not dependent on complex shared state
- not a public/shared API contract
- not a permission or compliance boundary
- not a long-lived deterministic Core Module contract

Use this template for:

- small helper behavior
- isolated utility logic
- local transformation tasks
- small component behavior with limited state
- narrow internal tooling behavior
- low-risk task handoff where concise execution rules are enough

Do **not** use this compact template if the task involves:

- database writes or migrations
- shared state
- API contracts used by other modules
- permission or access-control systems
- queue, job, or event systems
- complex data flows
- multi-step coordinated workflows
- formal idempotency, audit, telemetry, or traceability requirements
- architecture-relevant Core Module logic
- unresolved business logic
- privacy/security-sensitive behavior

If any of those apply, use:

- `03_yang_template.md` for a standalone full Yang Core Module
- `04_yin_yang_template.md` for a full combined Yin/Yang Document

For trivial CSS, copy, label, spacing, or static visual fixes, use a Direct Scoped Prompt instead.

---

## Language Rules

- The Yin section follows the configured `Yin output language`.
- The Yang section should be English by default for AI execution.
- Technical identifiers remain English in both sections.

---

## Security Rules

Never include secrets in this file.

Do not include:

- API keys
- passwords
- access tokens
- refresh tokens
- bearer tokens
- private keys
- session secrets
- private infrastructure values
- private user data unless explicitly allowed

Use environment variable placeholders instead.

---

## Template Body

Copy everything below this line.

---

```markdown
---
id: "[document-id]"
title: "[TASK_OR_FEATURE_NAME] — Yin/Yang Compact"
document_type: "Yin/Yang Compact"
document_role: "Compact Intent and Execution Specification"
layer: "[Infrastructure / Backend | System | Core | Ecosystem | Utilities | Framework | Workspace Context | Other]"
status: "[Draft | Review | Approved | Deprecated]"
version: "0.1.0"
metadata_version: "1.0.0"
created: "[YYYY-MM-DD]"
updated: "[YYYY-MM-DD]"
language: "[Yin output language for Yin section; Yang section is English by default]"
technical_identifiers_language: "English"
tags:
  - yin-yang
  - yin-yang-compact
  - compact
  - allzy-framework
aliases: []
summary: "[One to three sentences summarizing the compact task or feature.]"
retrieval_description: "[When should this compact Yin/Yang document be retrieved?]"
source:
  source_documents: []
  source_blocks: []
  generated_from_template: "04_yin_yang_template_compact.md"
  generated_by_prompt: ""
  source_context_package: ""
scope:
  project: ""
  product: ""
  system: ""
  domain: ""
  module_id: ""
  submodule_id: ""
  component_id: ""
  feature_id: "[task-or-feature-id]"
yin_yang:
  is_yin_yang_document: true
  yin_document: "[this-file#yin-intent]"
  yang_document: "[this-file#yang-execution-rules]"
  paired_yin: "[this-file#yin-intent]"
  paired_yang: "[this-file#yang-execution-rules]"
retrieval:
  retrieval_ready: true
  retrieval_confidence: "[High | Medium | Low | Unknown]"
  retrieval_priority: "[primary | normal | supporting | low | exclude]"
  preferred_retrieval_keys:
    - "[task-or-feature-id]"
  excluded_from_retrieval: false
  exclusion_reason: ""
compact_scope:
  requires_full_yang: false
  requires_full_yin_yang: false
  direct_prompt_too_small: false
  escalation_reason: ""
validation:
  metadata_inferred: false
  uncertain_fields: []
  missing_context: []
  needs_human_review: false
  validation_notes: []
---

# [TASK_OR_FEATURE_NAME] — Yin/Yang Compact

**Yin output language:** `[English | German | other]`  
**Task / Feature ID:** `[task-or-feature-id]`  
**Layer:** `[Infrastructure / Backend | System | Core | Ecosystem | Utilities | Framework | Workspace Context | Other]`  
**Status:** `[Draft | Review | Approved | Deprecated]`  
**Owner:** `[Team or person responsible]`  
**Last updated:** `[YYYY-MM-DD]`

---

## Scope Fit Check

Use this template only if all statements are true:

- [ ] The task is small and self-contained.
- [ ] The task does not require a full Yang Core Module.
- [ ] The task does not require a full Yin/Yang Document.
- [ ] The task is not merely trivial Direct work.
- [ ] The task does not affect shared APIs, persistence, permissions, queues, complex state, privacy/security boundaries, or architecture.
- [ ] Open questions can be safely marked without blocking the compact specification.

If any required statement is false, stop and use the correct Full or Direct artifact instead.

---

# Part 1 — YIN: Intent

## 1. Purpose

[One to three sentences.

Describe what this task, helper, small feature, utility, or isolated component is and why it exists.

Do not describe implementation details here.]

---

## 2. Target Audience / Actor

[Who uses this, triggers this, or benefits from it?]

| Actor | Need or expectation |
|---|---|
| [Actor] | [What this actor needs] |
| [Actor] | [What this actor needs] |

---

## 3. Expected Behavior

[Describe the expected behavior from start to finish in plain human language.]

1. [Trigger or starting situation]
2. [User, admin, system, or process action]
3. [Expected processing in human terms]
4. [Expected output, result, or visible change]
5. [Feedback, follow-up, or completion behavior]

---

## 4. Domain Rules

[Small list of human-level rules the implementation must respect.]

- [Rule 1]
- [Rule 2]
- [Rule 3]

---

## 5. Out of Scope

[What this task explicitly does not do.]

- This does not [excluded behavior].
- This does not [excluded feature].
- This does not [responsibility belonging elsewhere].
- This must not assume [unconfirmed rule or behavior].

---

# Part 2 — YANG: Execution Rules

## 6. Hard Rules

[Non-negotiable implementation constraints.]

- Must not modify files outside `[defined scope]`.
- Must not make network requests unless explicitly allowed.
- Must not write to a database, shared store, or external system.
- Must not log secrets or sensitive values.
- Must not introduce new dependencies unless explicitly allowed.
- Must not create new architecture.
- Must not add unrelated features.
- Must not change public APIs or shared contracts.
- Must not expand this compact task into a broader implementation.

---

## 7. Inputs

| Name | Type | Required | Description |
|---|---|---:|---|
| `[input_name]` | `[type]` | ✅ | [What it is] |
| `[input_name]` | `[type]` | ❌ | [What it is and default behavior if absent] |

---

## 8. Outputs

| Name | Type | Description |
|---|---|---|
| `[output_name]` | `[type]` | [What the output represents] |
| `[output_name]` | `[type]` | [What the output represents] |

---

## 9. Constraints

| Constraint | Value |
|---|---|
| Runtime | `[Node 22+ | Python 3.11+ | Browser | Other]` |
| Dependencies | `[none / allowed dependencies]` |
| File scope | `[allowed files or directories]` |
| Network access | `[forbidden / allowed only for X]` |
| Persistence | `[forbidden / local temp output only / other]` |
| Max execution time | `[expected limit]` |

---

## 10. Forbidden Actions

- Do not read or write files outside `[defined path]`.
- Do not make HTTP requests unless explicitly allowed.
- Do not log sensitive values.
- Do not add unrelated features.
- Do not refactor unrelated code.
- Do not change public APIs or shared contracts.
- Do not expand this compact task into a broader implementation.

---

## 11. Error Behavior

| Case | Expected behavior |
|---|---|
| Missing required input | [Behavior] |
| Invalid input | [Behavior] |
| File not found, if relevant | [Behavior] |
| Unsupported value | [Behavior] |
| Unexpected failure | [Behavior] |

---

## 12. Source Traceability

[Record where the intent, execution rules, constraints, and examples came from.

Do not invent sources.]

| Source | Type | Relevant sections / blocks | Used for |
|---|---|---|---|
| [Source document/path] | [Master Document / notes / screenshot / existing doc / issue / other] | [Section or block ID] | [Intent / rule / input / output / constraint] |

---

## 13. Acceptance Criteria

- [ ] [The task does X when given Y]
- [ ] [The output matches the expected format]
- [ ] [Invalid input is handled predictably]
- [ ] [No forbidden files are modified]
- [ ] [No secrets are logged or exposed]
- [ ] [No unrelated behavior is changed]

---

## 14. Open Questions

[Mark unresolved decisions. Do not invent answers.]

- [Question or missing decision]
- [Question or missing decision]

---

## 15. Quality Checklist

Before using this compact Yin/Yang document as AI context, verify:

- [ ] The task truly fits Compact scope.
- [ ] Full Yang is not required.
- [ ] Full Yin/Yang is not required.
- [ ] Direct is not sufficient.
- [ ] The Yin section explains intent clearly.
- [ ] The Yang section defines execution rules clearly.
- [ ] Inputs and outputs are explicit.
- [ ] Constraints are explicit.
- [ ] Forbidden actions prevent likely AI overreach.
- [ ] Acceptance criteria are testable.
- [ ] Source traceability is recorded where known.
- [ ] Open questions are marked instead of invented.
- [ ] No secrets appear anywhere in the document.
```
