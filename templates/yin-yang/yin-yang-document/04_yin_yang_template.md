---
id: "allzy.framework.templates.yin-yang.yin-yang-document"
title: "04 — Yin/Yang Document Template"
artifact_type: "Template"
template_family: "yin-yang.yin-yang-document"
status: "Draft"
version: "0.2.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - template
  - yin-yang
  - yin-yang-document
---

# 04 — Yin/Yang Document Template

## What Is a Yin/Yang Document?

A **Yin/Yang Document** is a single-file specification artifact that contains both:

1. a complete **Yin Page** for human intent, product meaning, workflows, domain logic, UI context, data concepts, roles, dependencies, privacy/safety expectations, source traceability, and scope boundaries
2. a complete **Yang Core Module** for the AI-facing technical execution contract

Use this template when one module or submodule needs both the human/product/domain layer and the technical execution contract in one document.

The Yin section prevents loss of intent.

The Yang section prevents uncontrolled implementation invention.

Together, they provide a bounded, high-signal context package for AI-assisted implementation.

---

## When to Use This Template

Use this full Yin/Yang template when:

- the module is non-trivial
- the module has both product/domain intent and executable technical logic
- the work may affect business logic, permissions, persistence, APIs, shared state, queues, audit, telemetry, integrations, or architecture
- the implementation agent must not infer missing behavior
- Yin and Yang should travel together in one file
- future review, triage, maintenance, or implementation needs a complete single-file specification

Do **not** use this template for:

- trivial CSS fixes
- static copy edits
- isolated label changes
- small visual tweaks with no contract impact
- simple notes or README prose
- Yin-only product documentation
- Yang-only technical contracts
- small executable tasks that fit Yin/Yang Compact

Use:

- `02_yin_template.md` for a full Yin Page only
- `02_yin_template_compact.md` for a Compact Yin Page only
- `03_yang_template.md` for a standalone full Yang Core Module
- `04_yin_yang_template_compact.md` for small low-risk executable tasks needing concise intent and execution rules
- Direct Scoped Prompt for trivial isolated work

There is no standalone **Yang Compact** artifact.

---

## Language Rules

- The Yin section follows the configured `Yin output language`.
- The Yang section is always English.
- Technical identifiers remain English in both sections.
- If the document mixes non-English Yang prose into the Yang section, the Yang section is invalid and must be regenerated.

---

## Boundary Rules

- Do not shorten the Yang section when full Yang is required.
- Do not replace the Yang section with informal technical notes.
- Do not mix product prose into Yang as primary content.
- Do not mix implementation contracts into Yin as primary content.
- Do not remove source traceability.
- Do not remove retrieval metadata.
- Do not create or imply `Yang Compact`.
- If the task is small and does not need full Yang, use `04_yin_yang_template_compact.md` instead.
- If the work only needs human intent, use `02_yin_template.md` or `02_yin_template_compact.md`.

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
title: "[MODULE_NAME] — Yin/Yang Document"
document_type: "Yin/Yang Document"
document_role: "Human Intent and Technical Execution Specification"
layer: "[Infrastructure / Backend | System | Core | Ecosystem | Utilities | Framework | Other]"
status: "[Draft | Review | Approved | Deprecated]"
version: "0.1.0"
metadata_version: "1.0.0"
created: "[YYYY-MM-DD]"
updated: "[YYYY-MM-DD]"
language: "[Yin output language for Yin section; Yang section is English]"
technical_identifiers_language: "English"
tags:
  - yin-yang
  - yin-yang-document
  - yin-page
  - yang-core-module
  - allzy-framework
aliases: []
summary: "[One to three sentences summarizing the module and what this Yin/Yang Document specifies.]"
retrieval_description: "[When should this Yin/Yang Document be retrieved for AI-assisted implementation, review, triage, or verification?]"
source:
  source_documents: []
  source_blocks: []
  generated_from_template: "04_yin_yang_template.md"
  generated_by_prompt: ""
  source_context_package: ""
scope:
  project: ""
  product: ""
  system: ""
  domain: ""
  module_id: "[module-id]"
  submodule_id: "[submodule-id-or-empty]"
  component_id: ""
  feature_id: ""
yin_yang:
  is_yin_yang_document: true
  yin_document: "[this-file#yin-section]"
  yang_document: "[this-file#yang-section]"
  paired_yin: "[this-file#yin-section]"
  paired_yang: "[this-file#yang-section]"
retrieval:
  retrieval_ready: true
  retrieval_confidence: "[High | Medium | Low | Unknown]"
  retrieval_priority: "[primary | normal | supporting | low | exclude]"
  preferred_retrieval_keys:
    - "[module-id]"
    - "[submodule-id]"
  excluded_from_retrieval: false
  exclusion_reason: ""
contract:
  schema_version: "[SCHEMA_VERSION]"
  config_version: "[CONFIG_VERSION]"
  core_signature: "[ResultType] = f([ConfigType], [StateSnapshotType], [InputEventType])"
  idempotency_anchor: "[InputEvent.eventId or domain-specific field]"
  action_registry_defined: false
  decision_matrix_defined: false
  preflight_gap_check_passed: false
validation:
  metadata_inferred: false
  uncertain_fields: []
  missing_context: []
  needs_human_review: false
  validation_notes: []
---

# [MODULE_NAME] — Yin/Yang Document

**Yin output language:** `[English | German | other]`  
**Module ID:** `[module-id]`  
**Submodule ID:** `[submodule-id or Not applicable]`  
**Layer:** `[Infrastructure / Backend | System | Core | Ecosystem | Utilities | Framework | Other]`  
**Version:** `[0.1.0]`  
**Status:** `[Draft | Review | Approved | Deprecated]`  
**Owner:** `[Team or person responsible]`  
**Last updated:** `[YYYY-MM-DD]`

---

# Part 1 — YIN: Human Intent

## 1. Short Description

[One to three sentences explaining what this module does in plain human language.

Avoid implementation details.]

---

## 2. Purpose and Product Meaning

[Explain why this module exists, which product/domain problem it solves, and what role it plays.]

---

## 3. Target Audience

| Audience / Actor | Need or expectation | Context |
|---|---|---|
| [Actor] | [Need] | [Context] |
| [Actor] | [Need] | [Context] |

---

## 4. Core Value

[Describe the value this module provides.]

---

## 5. Main Capabilities

| Capability | Description | Practical example | Status |
|---|---|---|---|
| [Capability] | [Description] | [Example] | `[Planned | Active | Deprecated]` |
| [Capability] | [Description] | [Example] | `[Planned | Active | Deprecated]` |

---

## 6. Domain Logic / Business Rules

| Rule | Meaning | Example | Priority |
|---|---|---|---|
| [Rule] | [Meaning] | [Example] | `[Required | Recommended | Optional]` |
| [Rule] | [Meaning] | [Example] | `[Required | Recommended | Optional]` |

---

## 7. Workflows

### 7.1 Workflow Overview

| Workflow | Trigger | Actor | Outcome |
|---|---|---|---|
| [Workflow] | [Trigger] | [Actor] | [Outcome] |
| [Workflow] | [Trigger] | [Actor] | [Outcome] |

### 7.2 [Primary Workflow Name]

1. [Trigger]
2. [User/admin/system action]
3. [Conceptual product processing]
4. [Result]
5. [Follow-up]

**Expected result:** [Successful end state.]

**Important alternatives / edge cases:** [Relevant alternatives.]

---

## 8. UI / Interaction Meaning

[Describe screens, controls, states, visibility rules, or feedback behavior.

Do not write CSS, code, framework-specific instructions, or implementation markup.]

### Screens / Views

| View name | Purpose | Primary actor | Notes |
|---|---|---|---|
| [View] | [Purpose] | [Actor] | [Notes] |

### States and Feedback

| State | Meaning | User-facing feedback | Notes |
|---|---|---|---|
| [State] | [Meaning] | [Feedback] | [Notes] |

---

## 9. Data Concepts and Field Definitions

[Human-level field dictionary. This is not the formal JSON schema.]

### [Primary Entity Name]

| Field | Type | Required | Meaning | Validation / constraint | Example |
|---|---|---:|---|---|---|
| `[field_name]` | [type] | [Yes / No] | [Meaning] | [Constraint] | [Example] |

---

## 10. Roles, Permissions, Privacy, and Safety

| Role | Expected access / capability | Restriction | Notes |
|---|---|---|---|
| `[ROLE_KEY]` | [Capability] | [Restriction] | [Notes] |

### Security and Privacy Considerations

- [Sensitive data category and handling expectation]
- [Audit/logging/redaction expectation]
- [Privacy, GDPR/DSGVO, compliance, or retention expectation]
- [Safety or abuse-prevention concern]

Environment variables required by this module, if relevant:

- `$ENV_[VARIABLE_NAME]` — [What it is used for, no real value]

---

## 11. Integrations and Dependencies

| Dependency | Type | Purpose | Required |
|---|---|---|---|
| `[dependency-name]` | [Internal module / External service / Library / Human process] | [Purpose] | [Yes / No] |

### Upstream Dependencies

- `[module-id]` — [What it provides]

### Downstream Dependents

- `[module-id]` — [How it uses this module]

---

## 12. Out of Scope

- This module does not [excluded behavior].
- This module does not [excluded feature].
- This module does not [responsibility belonging to another module].
- This module must not assume [unconfirmed rule or behavior].

---

## 13. Example Application

**Scenario:** [Describe who the actor is, what they want to accomplish, and why this module matters.]

1. [Step]
2. [Step]
3. [Step]
4. [Step]

**Result:** [Value delivered.]

---

## 14. Source Traceability for Yin

| Source | Type | Relevant sections / blocks | Used for |
|---|---|---|---|
| [Source document/path] | [Master Document / notes / screenshot / transcript / existing doc / other] | [Section or block ID] | [Intent / rule / workflow / UI meaning / constraint] |

---

## 15. Yin Open Questions

- [Question or missing decision]
- [Question or missing decision]

---

# Part 2 — YANG: Technical Execution Contract

## 16. Domain Context

[Write one concise factual paragraph.

Describe what this core computes, which domain it belongs to, which problem it solves at the technical contract level, and where it sits in the system.

Do not include marketing language, long product vision, user-story prose, or UI explanation. That belongs in Yin.]

**Bounded context:** `[BOUNDED_CONTEXT_NAME]`  
**Upstream dependencies:** `[MODULE_A]`, `[MODULE_B]`  
**Downstream dependents:** `[MODULE_C]`, `[MODULE_D]`  
**Triggering event or entry point:** `[WHAT TRIGGERS THIS CORE]`

---

## 17. Architecture Overview

| Property | Value |
|---|---|
| Module name | `[MODULE_NAME]` |
| Paradigm | Functional Core / Imperative Shell |
| Core signature | `[ResultType] = f([ConfigType], [StateSnapshotType], [InputEventType])` |
| Side-effect strategy | Action objects returned to Imperative Shell |
| Idempotency anchor | `[InputEvent.eventId or domain-specific idempotency field]` |
| Schema version | `[SCHEMA_VERSION]` |
| Config version | `[CONFIG_VERSION]` |

### Core Guarantees

| Guarantee | Required | Contract statement |
|---|---:|---|
| Deterministic | ✅ | Same `Config`, `StateSnapshot`, and `InputEvent` must produce the same `FunctionalResult`. |
| Idempotent | ✅ | Reprocessing the same idempotency anchor must not produce uncontrolled duplicate side effects. |
| Side-effect-free | ✅ | The Functional Core performs no I/O and mutates no external state. |
| Schema-validatable | ✅ | All inputs and outputs must be validated against defined schemas. |
| Testable | ✅ | All decision paths must be testable without external services. |
| Auditable | ✅ | Every decision must include reason, traceability, and audit data. |
| Versionable | ✅ | Schema and configuration versions must be explicit. |

---

## 18. API Contract

All four schema blocks are required.

### 18.1 Configuration Schema

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "[MODULE_ID]/config/v[CONFIG_VERSION]",
  "title": "[MODULE_NAME] Configuration",
  "type": "object",
  "required": [
    "configVersion",
    "[REQUIRED_CONFIG_FIELD_1]"
  ],
  "additionalProperties": false,
  "properties": {
    "configVersion": {
      "type": "integer",
      "description": "Configuration schema version. Increment on breaking configuration changes.",
      "example": 1
    },
    "[REQUIRED_CONFIG_FIELD_1]": {
      "type": "[string | integer | boolean | number | object | array]",
      "description": "[What this configuration field controls]",
      "example": "[EXAMPLE_VALUE]"
    },
    "[OPTIONAL_FEATURE_FLAG]": {
      "type": "boolean",
      "description": "[What this flag enables or disables]",
      "default": false
    }
  }
}
```

### 18.2 State Snapshot Schema

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "[MODULE_ID]/state-snapshot/v[SCHEMA_VERSION]",
  "title": "[MODULE_NAME] State Snapshot",
  "type": "object",
  "required": [
    "snapshotId",
    "currentTime",
    "[REQUIRED_STATE_FIELD_1]"
  ],
  "additionalProperties": false,
  "properties": {
    "snapshotId": {
      "type": "string",
      "format": "uuid",
      "description": "Unique identifier for this state snapshot. Used for traceability."
    },
    "currentTime": {
      "type": "string",
      "format": "date-time",
      "description": "Injected UTC time. The core must never read system time directly."
    },
    "[REQUIRED_STATE_FIELD_1]": {
      "type": "[string | object | array | boolean | integer | number]",
      "description": "[What this state field represents and where it comes from]"
    },
    "status": {
      "type": "string",
      "description": "[Current status relevant to this module's decision logic]",
      "enum": ["[STATUS_A]", "[STATUS_B]", "[STATUS_C]"]
    },
    "phase": {
      "type": "string",
      "description": "[Current lifecycle phase or workflow phase, if relevant]"
    },
    "errorCode": {
      "type": ["string", "null"],
      "description": "[Last known error code from a prior attempt, if relevant. Null if no prior error.]"
    }
  }
}
```

### 18.3 Input Event / Command Schema

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "[MODULE_ID]/input-event/v[SCHEMA_VERSION]",
  "title": "[MODULE_NAME] Input Event",
  "type": "object",
  "required": ["eventId", "traceId", "correlationId", "eventType", "timestamp", "actor", "payload"],
  "additionalProperties": false,
  "properties": {
    "eventId": {
      "type": "string",
      "format": "uuid"
    },
    "traceId": {
      "type": "string"
    },
    "correlationId": {
      "type": "string"
    },
    "eventType": {
      "type": "string"
    },
    "timestamp": {
      "type": "string",
      "format": "date-time"
    },
    "actor": {
      "type": "object",
      "required": ["actorId", "actorType"],
      "additionalProperties": false,
      "properties": {
        "actorId": {
          "type": "string",
          "description": "Identifier of the user, service, admin, or system actor."
        },
        "actorType": {
          "type": "string",
          "enum": ["USER", "SERVICE", "ADMIN", "SYSTEM"],
          "description": "Type of actor that triggered the event."
        }
      }
    },
    "payload": {
      "type": "object",
      "description": "Event-type-specific payload.",
      "required": ["[PAYLOAD_FIELD_1]"],
      "additionalProperties": false,
      "properties": {
        "[PAYLOAD_FIELD_1]": {
          "type": "[string | integer | boolean | object | array | number]",
          "description": "[Payload field description]"
        },
        "[PAYLOAD_FIELD_2]": {
          "type": "[string | integer | boolean | object | array | number]",
          "description": "[Payload field description]"
        }
      }
    }
  }
}
```

### 18.4 Functional Result Schema

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "[MODULE_ID]/functional-result/v[SCHEMA_VERSION]",
  "title": "[MODULE_NAME] Functional Result",
  "type": "object",
  "required": ["resultId", "eventId", "traceId", "verdict", "decision", "reason", "actions", "telemetry", "auditLog"],
  "additionalProperties": false,
  "properties": {
    "resultId": {
      "type": "string",
      "format": "uuid"
    },
    "eventId": {
      "type": "string",
      "format": "uuid"
    },
    "traceId": {
      "type": "string"
    },
    "verdict": {
      "type": "string",
      "enum": ["ALLOW", "DENY", "RETRY", "NOOP", "ERROR"]
    },
    "decision": {
      "type": "string"
    },
    "reason": {
      "type": "string"
    },
    "actions": {
      "type": "array"
    },
    "telemetry": {
      "type": "object"
    },
    "auditLog": {
      "type": "object"
    }
  }
}
```

---

## 19. Decision Pipeline

| Step | Name | Input used | Decision / output | Failure behavior |
|---|---|---|---|---|
| 1 | [Validate input] | `InputEvent` | [Valid / invalid] | [Return ERROR / DENY] |
| 2 | [Check permissions] | `StateSnapshot`, `InputEvent.actor` | [Allowed / denied] | [Return DENY] |
| 3 | [Evaluate rule] | `Config`, `StateSnapshot`, `InputEvent.payload` | [Decision] | [Behavior] |

---

## 20. Decision Matrix

| Case | Conditions | Verdict | Decision | Actions | Audit reason |
|---|---|---|---|---|---|
| [Case name] | [Condition set] | `[ALLOW | DENY | RETRY | NOOP | ERROR]` | `[DECISION_CODE]` | [Action types] | [Reason] |

---

## 21. Action Registry

| Action type | Purpose | Payload schema / fields | Executed by | Idempotency key | Retry behavior |
|---|---|---|---|---|---|
| `[ACTION_TYPE]` | [Purpose] | [Fields] | [Shell / service / adapter] | [Key] | [Retry / no retry] |

### Action Object Rules

- Every action must have a stable `actionType`.
- Every action must include a safe idempotency key.
- Actions must not contain secrets.
- Actions must not require the Imperative Shell to re-evaluate business logic.
- If an action cannot be safely retried, state that explicitly.

---

## 22. Invariants

| Invariant | Why it matters | Verification method |
|---|---|---|
| [Invariant] | [Reason] | [Test / assertion / review] |

---

## 23. Idempotency and Duplicate Handling

**Idempotency anchor:** `[field]`

| Scenario | Expected behavior |
|---|---|
| Same event processed twice | [Behavior] |
| Action already executed | [Behavior] |
| Retry after transient failure | [Behavior] |
| Duplicate with changed payload | [Behavior] |

---

## 24. Error and Edge Case Behavior

| Case | Detection | Expected result | Actions | Audit / telemetry |
|---|---|---|---|---|
| Missing required input | [How detected] | [ERROR / DENY / NOOP] | [None / action] | [What to record] |
| Invalid actor permissions | [How detected] | [DENY] | [None / action] | [What to record] |
| Missing state snapshot field | [How detected] | [ERROR] | [None / action] | [What to record] |

---

## 25. Observability

### Logs

| Log event | Level | Fields | Redaction rule |
|---|---|---|---|
| `[LOG_EVENT]` | `[debug | info | warn | error]` | [Fields] | [What must be redacted] |

### Metrics

| Metric | Type | Labels | Purpose |
|---|---|---|---|
| `[metric_name]` | `[counter | gauge | histogram]` | [Labels] | [Purpose] |

### Trace Fields

| Field | Source | Purpose |
|---|---|---|
| `traceId` | Input event | Distributed trace propagation |
| `correlationId` | Input event | Business workflow grouping |
| `resultId` | Functional result | Result traceability |

---

## 26. Audit Requirements

| Audit field | Required | Meaning | Sensitive? |
|---|---:|---|---|
| `eventId` | ✅ | Input event ID | No |
| `actorId` | ✅ | Actor identifier or redacted actor reference | Potentially |
| `decision` | ✅ | Decision code | No |
| `reason` | ✅ | Decision reason | No |

---

## 27. Test Matrix

| Test ID | Scenario | Given | When | Then |
|---|---|---|---|---|
| `[TEST_ID]` | [Scenario] | [Config + StateSnapshot + InputEvent] | [Core runs] | [Expected FunctionalResult] |

### Required Test Coverage

- [ ] Valid happy path
- [ ] Invalid input
- [ ] Missing required state
- [ ] Permission denied
- [ ] Duplicate/idempotent event
- [ ] Action generation
- [ ] No forbidden side effects inside Functional Core
- [ ] Audit data present
- [ ] Telemetry data present
- [ ] Edge cases listed in this contract

---

## 28. Imperative Shell Responsibilities

### Before Calling the Core

- [ ] Load and validate `Config`.
- [ ] Assemble `StateSnapshot`.
- [ ] Validate or normalize `InputEvent`.
- [ ] Inject current time into `StateSnapshot`.
- [ ] Provide trace and correlation IDs.
- [ ] Ensure no secrets are passed unless explicitly allowed and safe.

### After Calling the Core

- [ ] Execute returned Action objects.
- [ ] Enforce idempotency keys for side effects.
- [ ] Persist audit logs where required.
- [ ] Emit telemetry and traces.
- [ ] Handle retries according to action policy.
- [ ] Do not re-evaluate business logic outside the core.

---

## 29. Source Traceability for Yang

| Source | Type | Section / block | Contract element derived |
|---|---|---|---|
| [Source document/path] | [Yin Page / Master Document / existing code / issue / screenshot / other] | [Section or block ID] | [Schema / rule / action / invariant / test] |

---

## 30. Yin-to-Yang Trace Map

| Yin concept / rule | Yang contract element | Status |
|---|---|---|
| [Yin rule or concept] | [Schema / decision step / action / invariant / test] | `[Covered | Partial | Missing | Open]` |

---

## 31. Open Questions / Contract Gaps

- [Question or contract gap]
- [Question or contract gap]

---

## 32. Pre-Flight Gap-Check

Before sending this Yin/Yang Document to an AI implementation agent, verify:

- [ ] The document is entirely in English (Yang section).
- [ ] Yin output language was followed in the Yin section.
- [ ] Technical identifiers remained in English in both sections.
- [ ] Document frontmatter is complete enough for deterministic retrieval.
- [ ] Matching Yin section is complete.
- [ ] Source traceability is recorded where known.
- [ ] Configuration Schema is complete.
- [ ] State Snapshot Schema is complete.
- [ ] Input Event / Command Schema is complete.
- [ ] Functional Result Schema is complete.
- [ ] Decision Pipeline is complete.
- [ ] Decision Matrix is complete enough to implement from.
- [ ] Action Registry is complete.
- [ ] Invariants are explicit.
- [ ] Idempotency behavior is defined.
- [ ] Errors and edge cases are defined.
- [ ] Observability expectations are defined.
- [ ] Audit requirements are defined.
- [ ] Test Matrix covers all meaningful paths.
- [ ] Imperative Shell responsibilities are explicit.
- [ ] No secrets, tokens, passwords, or private credentials appear anywhere.
- [ ] Open questions are marked instead of invented.
- [ ] The implementation agent can execute from this contract without inferring missing business logic.

---

## 33. Quality Checklist

- [ ] Yin output language was followed in the Yin section.
- [ ] Yang section is entirely English.
- [ ] Technical identifiers remained in English.
- [ ] Document frontmatter is complete enough for deterministic retrieval.
- [ ] Yin explains human/product/domain intent clearly.
- [ ] Yang defines a complete technical execution contract.
- [ ] Source traceability is recorded where known.
- [ ] Configuration Schema is complete.
- [ ] State Snapshot Schema is complete.
- [ ] Input Event / Command Schema is complete.
- [ ] Functional Result Schema is complete.
- [ ] Decision Pipeline is complete.
- [ ] Decision Matrix is complete enough to implement from.
- [ ] Action Registry is complete.
- [ ] Invariants are explicit.
- [ ] Idempotency behavior is defined.
- [ ] Errors and edge cases are defined.
- [ ] Observability expectations are defined.
- [ ] Audit requirements are defined.
- [ ] Test Matrix covers meaningful paths.
- [ ] Imperative Shell responsibilities are explicit.
- [ ] No secrets, tokens, passwords, or private credentials appear anywhere.
- [ ] Open questions are marked instead of invented.
```
