---
id: "allzy.framework.templates.yin.yin-page"
title: "02 — Yin Page Template"
artifact_type: "Template"
template_family: "yin.yin-page"
status: "Draft"
version: "0.2.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - template
  - yin
  - yin-page
---

# 02 — Yin Page Template

## What Is a Yin Page?

A **Yin Page** is the human-facing intent layer of an Allzy Framework module.

It captures what a module is, why it exists, who it serves, how it is used, which domain rules matter, which workflows must be understood, which UI or interaction meanings are relevant, and which boundaries must not be crossed.

A Yin Page is the source of truth for:

- human intent
- product meaning
- domain context
- onboarding context
- user/admin/system workflows
- UI and interaction meaning
- business rules in human language
- role, permission, privacy, and safety expectations at intent level
- scope boundaries
- open questions for architect review
- handoff notes for a later Yang Core Module

A Yin Page is **not** a technical execution contract.

It must not define implementation contracts, database schemas, API routes, TypeScript interfaces, library choices, Functional Core signatures, Action objects, implementation invariants, or machine-readable execution schemas as primary content.

Those belong in the matching **Yang Core Module**.

---

## When to Use This Template

Use this full Yin template for:

- real modules
- larger product areas
- long-lived documentation
- multi-step workflows
- product behavior with meaningful user, admin, or system meaning
- features with domain rules, permissions, UI states, privacy expectations, or business logic
- anything likely to receive a matching Yang Core Module later
- documentation that future AI sessions must understand without guessing

Do **not** use this template for:

- trivial CSS fixes
- static copy edits
- isolated label changes
- tiny one-off visual fixes
- implementation-only patches
- tasks that need only a Direct Scoped Prompt
- technical execution contracts that require Yang

Use **Compact Yin Page** when the scope is smaller but still needs human intent.

Use **Yin/Yang Compact** when a small executable task needs both concise intent and concise execution rules.

Use **Yang Core Module** when formal deterministic technical execution logic is required.

There is no standalone **Yang Compact** artifact.

---

## Language Rule

The generated Yin prose must be written in the configured **Yin output language**.

Technical identifiers must always remain in English, regardless of the selected Yin output language.

Technical identifiers include:

- module IDs
- submodule IDs
- file names and file paths
- field names
- enum values
- role keys
- dependency names
- environment variable names
- schema references
- event names
- action names
- API names
- metric names
- audit identifiers

Examples:

```text
Yin output language: German
Prose: German
Technical identifier: userRole, projectId, ADMIN, $ENV_AUTH_SECRET
```

```text
Yin output language: Spanish
Prose: Spanish
Technical identifier: userRole, projectId, ADMIN, $ENV_AUTH_SECRET
```

Yang documents are always written in English. The Yin output language does not change the Yang language rule.

---

## Security Rules

- Never include API keys, passwords, tokens, private keys, bearer tokens, refresh tokens, session secrets, or real credentials.
- Use environment variable placeholders for any credential reference.
- Yin Pages should be secret-free and safe to share with AI systems, collaborators, reviewers, or documentation workflows.
- Do not include sensitive operational details, private infrastructure values, private user data, or confidential business information unless explicitly allowed by the project owner.
- Logs, examples, scenarios, and audit notes must use fictional or redacted values.

Allowed examples:

```text
$ENV_SERVICE_API_KEY
${AUTH_SECRET}
$ENV_DATABASE_URL
```

Forbidden examples:

```text
sk-abc123...
Bearer eyJhbGci...
real passwords
real tokens
real private infrastructure values
```

---

## Template Body

Copy everything below this line.

---

```markdown
---
id: "[document-id]"
title: "[MODULE_NAME] — Yin Page"
document_type: "Yin Page"
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
  - yin-page
  - allzy-framework
aliases: []
summary: "[One to three sentences summarizing what this Yin Page explains.]"
retrieval_description: "[When should this Yin Page be retrieved for AI-assisted work?]"
source:
  source_documents: []
  source_blocks: []
  generated_from_template: "02_yin_template.md"
  generated_by_prompt: ""
  source_context_package: ""
scope:
  project: ""
  product: ""
  system: ""
  domain: ""
  module_id: "[module-id]"
  submodule_id: ""
  component_id: ""
  feature_id: ""
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
    - "[module-id]"
  excluded_from_retrieval: false
  exclusion_reason: ""
validation:
  metadata_inferred: false
  uncertain_fields: []
  missing_context: []
  needs_human_review: false
  validation_notes: []
---

# [MODULE_NAME] — Yin Page

**Yin output language:** `[English | German | other]`  
**Module ID:** `[module-id]`  
**Submodule ID:** `[submodule-id or Not applicable]`  
**Layer:** `[Vision | Infrastructure / Backend | System | Core | Ecosystem | Utilities | Framework | Workspace Context | Other]`  
**Version:** `[0.1.0]`  
**Status:** `[Draft | Review | Stable | Deprecated]`  
**Owner:** `[Team or person responsible]`  
**Last updated:** `[YYYY-MM-DD]`  
**Paired Yang document:** `[yang-document-id-or-path | Not yet created | Not applicable]`

---

## 1. Short Description

[One to three sentences.

Explain what this module, product area, workflow, or feature does in plain human language.

Write this as if explaining the module to a new team member on their first day.

Avoid implementation details. Do not mention libraries, frameworks, database tables, API routes, code structure, or Functional Core details.]

---

## 2. Purpose and Product Meaning

[Explain why this module exists.

What product or domain problem does it solve?
What role does it play in the product?
What should the reader understand before implementation is discussed?]

---

## 3. Target Audience

[Describe who uses this module or is affected by it.

Include relevant user types, admin roles, internal operators, external users, background systems, or AI agents when applicable.

Do not define technical permission enforcement here. That belongs in Yang.]

| Audience / Actor | Need or expectation | Context |
|---|---|---|
| [Actor] | [What this actor needs from the module] | [When or why this matters] |
| [Actor] | [What this actor needs from the module] | [When or why this matters] |

---

## 4. Core Value

[Describe the value this module provides.

Focus on outcome, usefulness, and why the module matters to users, admins, operators, the product, or the system as a whole.]

---

## 5. Main Capabilities

[Describe the module's capabilities in terms a product manager, designer, domain expert, or architect would understand.

Each row is one meaningful capability, not a technical function.]

| Capability | Description | Practical example | Status |
|---|---|---|---|
| [Capability name] | [What it does from the user/product perspective] | [How it is used in practice] | `[Planned | Active | Deprecated]` |
| [Capability name] | [What it does from the user/product perspective] | [How it is used in practice] | `[Planned | Active | Deprecated]` |

---

## 6. Domain Logic / Business Rules

[Describe the real-world rules, product rules, business logic, policy logic, or domain-specific assumptions that this module must respect.

This section prevents AI invention.

Do not write implementation code, database schemas, API contracts, Functional Core rules, or Action objects here. Describe the rules in human language.]

| Rule | Meaning | Example | Priority |
|---|---|---|---|
| [Rule name] | [What the rule means in human terms] | [Concrete example] | `[Required | Recommended | Optional]` |
| [Rule name] | [What the rule means in human terms] | [Concrete example] | `[Required | Recommended | Optional]` |

---

## 7. Workflows

[Describe the key end-to-end flows this module participates in.

Use numbered steps for sequential flows. Use a table for an overview of multiple workflows.]

### 7.1 Workflow Overview

| Workflow | Trigger | Actor | Outcome |
|---|---|---|---|
| [Workflow name] | [What starts it] | [User role or system] | [What the actor gets or what changes] |
| [Workflow name] | [What starts it] | [User role or system] | [What the actor gets or what changes] |

### 7.2 [Primary Workflow Name]

1. [Trigger — what starts the workflow]
2. [Input or action — what the user, admin, or system does]
3. [Conceptual processing — what the product does in human terms]
4. [Result — what changes or becomes visible]
5. [Follow-up — feedback, notification, next action, logging, or handoff]

**Expected result:** [Describe the successful end state.]

**Important alternatives / edge cases:** [Describe what happens when something goes wrong, an optional path diverges, or the user/system cannot continue.]

### 7.3 [Secondary Workflow Name, if applicable]

1. [Trigger]
2. [Input or action]
3. [Conceptual processing]
4. [Result]
5. [Follow-up]

**Expected result:** [Describe the successful end state.]

**Important alternatives / edge cases:** [Describe relevant non-happy paths.]

---

## 8. UI / Interaction Meaning

[Describe screens, views, interaction surfaces, states, controls, visibility rules, or feedback behavior.

Do not write CSS, component code, implementation markup, framework-specific instructions, or design-system implementation details.

Reference design files or screenshots if they exist.]

### 8.1 Screens / Views

| View name | Purpose | Primary actor | Notes |
|---|---|---|---|
| [View name] | [What the user does here] | [Role] | [Design link, screenshot reference, or constraint] |
| [View name] | [What the user does here] | [Role] | [Design link, screenshot reference, or constraint] |

### 8.2 Key UI Concepts

- **[UI element or pattern]:** [What it means and why it matters]
- **[UI element or pattern]:** [What it means and why it matters]
- **[UI element or pattern]:** [What it means and why it matters]

### 8.3 States and Feedback

| State | Meaning | User-facing feedback | Notes |
|---|---|---|---|
| [State] | [What it means] | [What the user sees] | [Constraint or note] |
| [State] | [What it means] | [What the user sees] | [Constraint or note] |

---

## 9. Data Concepts and Field Definitions

[Describe the data this module works with in human terms.

This is not a JSON schema. It is a field dictionary for product, design, domain, and documentation understanding.

Use canonical English field names as identifiers, even when writing prose in another language.]

### 9.1 [Primary Entity Name]

[Briefly describe what this entity represents.]

| Field | Type | Required | Meaning | Validation / constraint | Example |
|---|---|---:|---|---|---|
| `[field_name]` | [string / number / boolean / date / enum / reference] | [Yes / No] | [What this field means] | [Human-readable validation or constraint] | [Example value] |
| `[field_name]` | [string / number / boolean / date / enum / reference] | [Yes / No] | [What this field means] | [Human-readable validation or constraint] | [Example value] |

**Enum values for `[field_name]`:**

| Value | Meaning |
|---|---|
| `[VALUE_A]` | [Plain-language description] |
| `[VALUE_B]` | [Plain-language description] |

### 9.2 [Secondary Entity Name, if applicable]

[Briefly describe what this entity represents.]

| Field | Type | Required | Meaning | Validation / constraint | Example |
|---|---|---:|---|---|---|
| `[field_name]` | [type] | [Yes / No] | [Meaning] | [Validation or constraint] | [Example] |

---

## 10. Roles, Permissions, Privacy, and Safety

[Describe who can do what and why.

Keep this at the intent level: actions, restrictions, sensitive categories, audit expectations, privacy expectations, and safety rules.

Do not encode technical enforcement logic here. That belongs in the Yang Core Module.]

| Role | Expected access / capability | Restriction | Notes |
|---|---|---|---|
| `[ROLE_KEY]` | [What this role should be able to do] | [What this role must not do] | [Any context] |
| `[ROLE_KEY]` | [What this role should be able to do] | [What this role must not do] | [Any context] |

### 10.1 Security and Privacy Considerations

- [Sensitive data category, if any, and how it should be treated]
- [Audit, logging, redaction, or traceability expectation]
- [Privacy, GDPR/DSGVO, compliance, or retention expectation]
- [Human-level safety or abuse-prevention concern]

Environment variables required by this module, if relevant:

- `$ENV_[VARIABLE_NAME]` — [What it is used for, no real value]
- `$ENV_[VARIABLE_NAME]` — [What it is used for, no real value]

---

## 11. Integrations and Dependencies

[List what this module depends on or integrates with.

Keep descriptions at product, domain, or intent level. Technical contracts belong in Yang.]

| Dependency | Type | Purpose | Required |
|---|---|---|---|
| `[dependency-name]` | [Internal module / External service / Library / Human process] | [Why this module needs it] | [Yes / No] |
| `[dependency-name]` | [Internal module / External service / Library / Human process] | [Why this module needs it] | [Yes / No] |

### 11.1 Upstream Dependencies

- `[module-id]` — [What data, capability, or decision it provides]

### 11.2 Downstream Dependents

- `[module-id]` — [How it uses this module]

---

## 12. Out of Scope

[List what this module explicitly does not do.

This section prevents feature creep and AI invention. Be concrete.]

- This module does not [excluded behavior].
- This module does not [excluded feature].
- This module does not [responsibility belonging to another module].
- This module must not assume [unconfirmed rule or behavior].

---

## 13. Example Application

[Show one concrete, realistic scenario where this module is used.

This is not a code example. It is a narrative or walkthrough.

Use realistic but fictional data. Help the reader understand the module in action.]

**Scenario:** [Describe who the actor is, what they want to accomplish, and why this module matters.]

1. [Step 1 — what the user, admin, system, or process does]
2. [Step 2 — what the product conceptually does in response]
3. [Step 3 — what changes or becomes visible]
4. [Step 4 — the outcome for the user/system]

**Result:** [Summarize the value delivered by the end of this scenario.]

---

## 14. Connection to the Yang Core Module

[This section bridges the Yin Page to its Yang counterpart.

List the concepts defined here that must be formally specified in the Yang Core Module.

Do not define the technical contracts here.]

The following concepts described in this Yin Page may require corresponding formal specification in `[module-id]_yang.md`:

- [ ] Data schema for `[EntityName]`
- [ ] Validation rules for `[field_name]`
- [ ] Functional signature for `[WorkflowName]`
- [ ] Permission enforcement contract for `[ROLE_KEY]`
- [ ] Integration contract with `[dependency-name]`
- [ ] Error taxonomy for `[WorkflowName]`
- [ ] Idempotency or duplicate-handling expectations, if relevant
- [ ] Audit, telemetry, or traceability expectations, if relevant
- [ ] Other Yin concept that must have a Yang counterpart: [describe]

---

## 15. Source Traceability

[Record where the intent, rules, workflows, and constraints came from.

Do not invent source links. Leave unknown fields empty and mark uncertainty.]

| Source | Type | Relevant sections / blocks | Used for |
|---|---|---|---|
| [Source document/path] | [Master Document / notes / screenshot / transcript / existing doc / other] | [Section or block ID] | [Intent / rule / workflow / UI meaning / constraint] |

---

## 16. Open Questions

[List missing decisions, unresolved assumptions, or points that require architect review.

Do not invent answers. Mark unknowns clearly.]

- [Question or missing decision]
- [Question or missing decision]
- [Question or missing decision]

---

## 17. Quality Checklist

Before using this Yin Page as AI context or handing it to a Yang author, verify:

- [ ] The configured Yin output language was followed.
- [ ] Technical identifiers remained in English.
- [ ] Document frontmatter is complete enough for retrieval.
- [ ] The module is understandable from a human/product/domain perspective.
- [ ] Target audience and actor expectations are clear.
- [ ] Core value is clear.
- [ ] User, admin, or system workflows are concrete.
- [ ] Domain logic and business rules are explicit.
- [ ] UI or interaction meaning is understandable without reading code.
- [ ] Relevant data concepts and fields are listed in human terms.
- [ ] Roles, permissions, privacy, and safety expectations are visible.
- [ ] Integrations and dependencies are listed.
- [ ] Out-of-scope boundaries are explicit.
- [ ] Source traceability is recorded where known.
- [ ] Open questions are marked instead of invented.
- [ ] The matching Yang Core Module can be logically derived from this Yin Page if needed.
- [ ] No secrets, tokens, passwords, or private credentials appear anywhere in the document.

---

*This Yin Page may serve as source material for product documentation, onboarding guides, AI context preparation, and later Yang contract creation. Keep it accurate, readable, retrieval-ready, and free of implementation-level execution detail.*
```
