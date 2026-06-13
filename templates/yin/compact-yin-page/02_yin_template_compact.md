---
id: "allzy.framework.templates.yin.compact-yin-page"
title: "02 — Compact Yin Page Template"
artifact_type: "Template"
template_family: "yin.compact-yin-page"
status: "Draft"
version: "0.2.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - template
  - yin
  - compact-yin-page
---

# 02 — Compact Yin Page Template

## What Is a Compact Yin Page?

A **Compact Yin Page** is a shorter Yin-only intent document for small or medium features that still need clear human context but do not justify the full Yin template.

It preserves the most important Yin responsibilities:

- define human intent
- explain purpose and value
- identify target audience or actors
- describe expected behavior
- capture domain rules
- define scope boundaries
- mark open questions
- prevent AI invention before later implementation work

A Compact Yin Page is **not** a technical execution contract.

It does not replace a Yang Core Module when deterministic core logic, APIs, persistence, permissions, shared state, audit, idempotency, or formal schemas are required.

---

## When to Use Compact Yin

Use Compact Yin for:

- small product features
- simple UI or UX areas
- a single product workflow
- a small admin surface
- a small internal tool that still needs product/domain context
- early module notes before deciding whether full Yin/Yang is needed
- low-overhead AI context where no technical execution contract should be written yet

Use the full Yin template instead when:

- the module has multiple workflows
- the module has multiple roles
- the module has meaningful state
- the module has complex domain logic
- the documentation must remain long-lived
- the module is likely to receive a full Yang Core Module later

Use Yin/Yang Compact when:

- the AI is expected to implement a small executable task
- concise execution rules are needed
- inputs, outputs, constraints, forbidden actions, and acceptance criteria must be explicit

Use Direct Scoped Prompt when:

- the task is trivial and isolated
- no contract, state, API, privacy, architecture, or business logic impact exists

There is no standalone **Yang Compact** artifact.

---

## Language Rule

The generated Compact Yin prose must be written in the configured **Yin output language**.

Technical identifiers must always remain in English, regardless of the selected Yin output language.

Yang documents are always written in English. The Yin output language does not change the Yang language rule.

---

## Security Rules

- Never include API keys, passwords, tokens, private keys, bearer tokens, refresh tokens, session secrets, or real credentials.
- Use environment variable placeholders for any credential reference.
- Compact Yin Pages should be secret-free and safe to share with AI systems, collaborators, and reviewers.
- Do not include sensitive operational details, private infrastructure values, private user data, or confidential business information unless explicitly allowed by the project owner.
- Use fictional or redacted examples.

---

## Template Body

Copy everything below this line.

---

```markdown
---
id: "[document-id]"
title: "[MODULE_OR_FEATURE_NAME] — Compact Yin Page"
document_type: "Compact Yin Page"
document_role: "Human Intent Specification"
layer: "[Vision | Infrastructure / Backend | System | Core | Ecosystem | Utilities | Framework | Workspace Context | Other]"
status: "[Draft | Review | Stable | Deprecated]"
version: "0.1.0"
metadata_version: "1.0.0"
created: "[YYYY-MM-DD]"
updated: "[YYYY-MM-DD]"
language: "[Yin output language]"
technical_identifiers_language: "English"
tags:
  - yin
  - compact-yin-page
  - allzy-framework
aliases: []
summary: "[One to three sentences summarizing what this Compact Yin Page explains.]"
retrieval_description: "[When should this Compact Yin Page be retrieved for AI-assisted work?]"
source:
  source_documents: []
  source_blocks: []
  generated_from_template: "02_yin_template_compact.md"
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
  feature_id: "[feature-id]"
yin_yang:
  is_yin_yang_document: false  # Set to true once this document is paired with a Yang document
  yin_document: "[this-file]"
  yang_document: ""
  paired_yin: ""
  paired_yang: ""
retrieval:
  retrieval_ready: true
  retrieval_confidence: "[High | Medium | Low | Unknown]"
  retrieval_priority: "[primary | normal | supporting | low | exclude]"
  preferred_retrieval_keys:
    - "[feature-id-or-module-id]"
  excluded_from_retrieval: false
  exclusion_reason: ""
validation:
  metadata_inferred: false
  uncertain_fields: []
  missing_context: []
  needs_human_review: false
  validation_notes: []
---

# [MODULE_OR_FEATURE_NAME] — Compact Yin Page

**Yin output language:** `[English | German | other]`  
**Module / Feature ID:** `[module-or-feature-id]`  
**Layer:** `[Vision | Infrastructure / Backend | System | Core | Ecosystem | Utilities | Framework | Workspace Context | Other]`  
**Status:** `[Draft | Review | Stable | Deprecated]`  
**Owner:** `[Team or person responsible]`  
**Last updated:** `[YYYY-MM-DD]`  
**Paired Yang document:** `[yang-document-id-or-path | Not yet created | Not applicable]`

---

## 1. Purpose

[One to three sentences.

What is this module, feature, workflow, or product area?
Why does it exist?
Which problem does it solve?

Avoid implementation details, code, APIs, database schemas, framework names, or library choices.]

---

## 2. Target Audience / Actors

[Who uses this or is affected by it?

Mention users, admins, internal operators, background systems, or AI agents where relevant.]

| Audience / Actor | Need or expectation |
|---|---|
| [Actor] | [What this actor needs from the feature/module] |
| [Actor] | [What this actor needs from the feature/module] |

---

## 3. Core Value

[One to four sentences.

What value does this provide?
What becomes easier, safer, clearer, faster, or more reliable because this exists?]

---

## 4. Expected Behavior

[Describe what should happen from the user, admin, or system perspective.

Use plain language. Focus on externally visible or domain-relevant behavior, not implementation.]

1. [Trigger or starting situation]
2. [User, admin, or system action]
3. [Product/system response in human terms]
4. [Expected result]
5. [Feedback, follow-up, or next step]

---

## 5. Domain Logic / Business Rules

[Describe the real-world rules, product rules, or policy rules that must be respected.

This section prevents AI invention.]

- [Rule 1]
- [Rule 2]
- [Rule 3]

---

## 6. UI / Interaction Notes

[Describe relevant screens, states, controls, visibility rules, feedback, or interaction meaning.

Do not write CSS, component code, framework-specific instructions, or implementation markup.]

- **[UI concept / state / element]:** [Meaning and expected behavior]
- **[UI concept / state / element]:** [Meaning and expected behavior]
- **[UI concept / state / element]:** [Meaning and expected behavior]

---

## 7. Data Concepts

[List important data concepts in human terms.

This is not a JSON schema. Use English technical identifiers for field names if needed.]

| Concept / Field | Meaning | Notes |
|---|---|---|
| `[field_or_concept]` | [What it means] | [Constraint, example, or clarification] |
| `[field_or_concept]` | [What it means] | [Constraint, example, or clarification] |

---

## 8. Roles, Permissions, Privacy, and Safety Notes

[Describe role expectations, restrictions, privacy considerations, security expectations, or safety concerns at the intent level.

Do not define technical enforcement logic here.]

- [Role, permission, or restriction note]
- [Privacy, audit, or compliance note]
- [Security or safety note]

Environment variable names, if relevant:

- `$ENV_[VARIABLE_NAME]` — [What it is used for, no real value]

---

## 9. Dependencies / Related Areas

[List modules, pages, workflows, human processes, or external systems this depends on or affects.

Keep this at the product/domain level.]

- `[related-module-or-area]` — [How it relates]
- `[related-module-or-area]` — [How it relates]

---

## 10. Out of Scope

[List what this feature or module explicitly does not do.

This prevents feature creep and AI invention.]

- This does not [excluded behavior].
- This does not [excluded feature].
- This does not [responsibility belonging elsewhere].
- This must not assume [unconfirmed rule or behavior].

---

## 11. Yang Handoff Notes

[If this later needs a Yang Core Module, list what must be formally specified there.

Do not define the Yang contract here.]

Potential Yang topics:

- [ ] Data schema for `[EntityName]`
- [ ] Validation rules for `[field_name]`
- [ ] Permission enforcement for `[ROLE_KEY]`
- [ ] Error or edge-case handling for `[WorkflowName]`
- [ ] Integration contract with `[dependency-name]`
- [ ] Audit, telemetry, or traceability expectations, if relevant

---

## 12. Source Traceability

[Record where the intent, rules, workflows, and constraints came from.

Do not invent source links. Leave unknown fields empty and mark uncertainty.]

| Source | Type | Relevant sections / blocks | Used for |
|---|---|---|---|
| [Source document/path] | [Master Document / notes / screenshot / transcript / existing doc / other] | [Section or block ID] | [Intent / rule / workflow / UI meaning / constraint] |

---

## 13. Open Questions

[List unresolved decisions. Do not invent answers.]

- [Question or missing decision]
- [Question or missing decision]
- [Question or missing decision]

---

## 14. Quality Checklist

Before using this Compact Yin Page as AI context, verify:

- [ ] The configured Yin output language was followed.
- [ ] Technical identifiers remained in English.
- [ ] Document frontmatter is complete enough for retrieval.
- [ ] The feature/module intent is clear.
- [ ] Target audience or actors are clear.
- [ ] Expected behavior is understandable.
- [ ] Domain rules are explicit.
- [ ] Scope boundaries are explicit.
- [ ] Privacy, safety, or permission expectations are visible where relevant.
- [ ] Source traceability is recorded where known.
- [ ] Open questions are marked instead of invented.
- [ ] Full Yin is not required.
- [ ] Full Yang is not required.
- [ ] No secrets, tokens, passwords, or private credentials appear anywhere in the document.
```
