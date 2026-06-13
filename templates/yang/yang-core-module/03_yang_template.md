---
id: "allzy.framework.templates.yang.yang-core-module"
title: "03 — Yang Core Module Template"
artifact_type: "Template"
template_family: "yang.yang-core-module"
status: "Draft"
version: "0.2.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - template
  - yang
  - yang-core-module
---

# 03 — Yang Core Module Template

## What Is a Yang Core Module?

A **Yang Core Module** is the AI-facing technical execution contract for a single Allzy Framework module or submodule.

It defines the deterministic core logic that can be implemented, tested, audited, reviewed, and maintained. It specifies:

- configuration
- injected state
- input events or commands
- validation rules
- decision logic
- result schema
- Action objects
- invariants
- idempotency behavior
- error and edge cases
- observability requirements
- audit requirements
- source traceability
- relationship to the matching Yin Page

Yang answers:

```text
How is the pure core logic computed?
Which inputs are accepted?
Which state is injected?
Which decisions are allowed?
Which outputs are produced?
Which side effects are returned as actions?
Which invariants must never break?
Which errors and edge cases must be handled?
How can the behavior be tested?
How is the implementation traced back to Yin and source context?
```

A Yang document is **not** final source code.

It is the technical contract the implementation must satisfy.

A Yang document is always written in English. No exceptions. Mixed-language Yang documents are invalid and must be regenerated before use.

---

## When to Use This Template

Use this template when the object or task defines architecture-relevant executable logic, especially when any of the following are true:

- the object type is `Core Module`
- the module has deterministic decision logic
- configuration affects decisions
- runtime state must be injected
- input events or commands must be validated
- outputs must be structured and testable
- side effects must be controlled through Action objects
- idempotency matters
- permissions, authorization, quotas, limits, retries, or compliance rules are involved
- persistence, queueing, API calls, email sending, notifications, or external side effects must be coordinated by an Imperative Shell
- the module requires formal test cases, observability, audit, or traceability
- contract drift would create implementation risk
- future AI agents must implement from a precise technical contract rather than infer behavior

Do **not** use this template for:

- Yin Pages or human-facing product/domain documentation
- marketing text
- UI-only descriptions with no core logic
- trivial CSS fixes
- static copy edits
- one-off label changes
- simple notes, README text, or onboarding prose
- small executable tasks that fit the Yin/Yang Compact criteria

If this template feels too heavy, do **not** create a compact Yang variant.

There is no standalone **Yang Compact** artifact.

Use `04_yin_yang_template_compact.md` only for small, low-risk executable tasks without persistence, permissions, shared state, API contracts, queues, complex data flows, or formal audit/idempotency needs.

---

## Relationship to Yin

Yang pairs with a Yin Page.

- **Yin** defines human intent, target audience, product meaning, domain rules, workflows, UI concepts, and out-of-scope boundaries.
- **Yang** defines the technical execution contract that implements the relevant core logic safely and deterministically.

A Yang Core Module may reference the matching Yin Page for intent, but it must not duplicate long product prose.

The Yang document must translate relevant Yin concepts into explicit technical rules, schemas, decisions, actions, tests, and traceability.

If the matching Yin Page is missing, incomplete, outdated, or contradictory, mark this in **Open Questions / Contract Gaps** instead of inventing intent.

---

## Security Rules

- No API keys in this document — ever.
- No passwords in this document — ever.
- No access tokens, refresh tokens, bearer tokens, private keys, or session secrets in this document — ever.
- Reference secrets only through environment variable placeholders.
- Actual secret values live in the environment or a secrets manager, not in any specification file.
- Do not include private infrastructure values, internal IP addresses, private user data, production credentials, or confidential operational details unless explicitly allowed by the project owner.
- All logs, telemetry, audit examples, and test fixtures must avoid sensitive values.
- Use fictional, redacted, or placeholder values in examples.

Allowed examples:

```text
$ENV_SERVICE_API_KEY
$ENV_DATABASE_URL
$ENV_WEBHOOK_SECRET
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

## Architecture Model

Every Yang Core Module follows the **Functional Core / Imperative Shell** pattern.

| Layer | Responsibility | May perform I/O? |
|---|---|---:|
| **Functional Core** | Validates inputs, checks permissions from injected state, evaluates rules, makes decisions, creates result objects, proposes Action objects, structures telemetry and audit data | No |
| **Imperative Shell** | Reads external state, calls the Functional Core, executes Action objects, performs database writes, HTTP calls, queue publication, emails, notifications, file I/O, and other side effects | Yes |

Standard core signature:

```text
Result = f(Config, StateSnapshot, InputEvent)
```

The core is a pure function. It receives structured input. It produces structured output. It never performs I/O.

### What the Functional Core May Do

- Validate inputs against defined schemas
- Check permissions and authorization rules from injected state
- Evaluate multi-step decision logic
- Produce structured results with explicit verdicts and decisions
- Propose Action objects for the Imperative Shell to execute
- Produce telemetry, audit, and trace data
- Return explicit errors, rejection decisions, or retry instructions

### What the Functional Core Must Never Do

- Write to databases directly
- Send HTTP requests directly
- Read or write files directly
- Publish to message queues directly
- Send emails directly
- Send notifications directly
- Call external APIs directly
- Read process environment variables directly
- Read system time directly
- Use hidden global state
- Mutate external state
- Perform side effects outside returned Action objects

Runtime facts must be injected through `Config`, `StateSnapshot`, or `InputEvent`.

---

## How to Use This Template

1. Copy the template body below.
2. Replace every `[PLACEHOLDER]` with module-specific content.
3. Keep the document entirely in English.
4. Fill in document frontmatter.
5. Fill in all four required schemas:
   - Configuration Schema
   - State Snapshot Schema
   - Input Event / Command Schema
   - Functional Result Schema
6. Define the Decision Pipeline and Decision Matrix.
7. Define the Action Registry.
8. Define invariants, idempotency, errors, tests, observability, audit, and traceability.
9. Mark unresolved items in `Open Questions / Contract Gaps`.
10. Run the Pre-Flight Gap-Check before sending the Yang document to an AI implementation agent.

A Yang contract with placeholder schemas, undefined decisions, missing errors, missing idempotency, or no trace map is incomplete.

---

## Template Body

Copy everything below this line.

---

```markdown
---
id: "[document-id]"
title: "[MODULE_NAME] — Yang Core Module"
document_type: "Yang Core Module"
document_role: "Technical Execution Contract"
layer: "[Infrastructure / Backend | System | Core | Ecosystem | Utilities | Framework | Other]"
status: "[Draft | Review | Approved | Deprecated]"
version: "0.1.0"
metadata_version: "1.0.0"
created: "[YYYY-MM-DD]"
updated: "[YYYY-MM-DD]"
language: "English"
technical_identifiers_language: "English"
tags:
  - yang
  - yang-core-module
  - technical-contract
  - allzy-framework
aliases: []
summary: "[One to three sentences summarizing what this Yang Core Module technically specifies.]"
retrieval_description: "[When should this Yang Core Module be retrieved for AI-assisted implementation, review, triage, or verification?]"
source:
  source_documents: []
  source_blocks: []
  generated_from_template: "03_yang_template.md"
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
  is_yin_yang_document: false  # Set to true once this document is paired with a Yin document
  yin_document: ""
  yang_document: "[this-file]"
  paired_yin: "[yin-document-id-or-path]"
  paired_yang: ""
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

# [MODULE_NAME] — Yang Core Module

**Document type:** `Yang Core Module`  
**Module ID:** `[MODULE_ID]`  
**Submodule ID:** `[SUBMODULE_ID or Not applicable]`  
**Layer:** `[Infrastructure / Backend | System | Core | Ecosystem | Utilities | Framework | Other]`  
**Schema version:** `[SCHEMA_VERSION]`  
**Config version:** `[CONFIG_VERSION]`  
**Paired Yin document:** `[YIN_DOCUMENT_TITLE]` — `[YIN_DOCUMENT_ID_OR_PATH]`  
**Status:** `[Draft | Review | Approved | Deprecated]`  
**Owner:** `[Team or person responsible]`  
**Last updated:** `[YYYY-MM-DD]`

---

## 1. Domain Context

[Write one concise factual paragraph.

Describe what this core computes, which domain it belongs to, which problem it solves at the technical contract level, and where it sits in the system.

Do not include marketing language, long product vision, user-story prose, or UI explanation. That belongs in Yin.]

**Bounded context:** `[BOUNDED_CONTEXT_NAME]`  
**Upstream dependencies:** `[MODULE_A]`, `[MODULE_B]`  
**Downstream dependents:** `[MODULE_C]`, `[MODULE_D]`  
**Triggering event or entry point:** `[WHAT TRIGGERS THIS CORE]`

---

## 2. Architecture Overview

| Property | Value |
|---|---|
| Module name | `[MODULE_NAME]` |
| Paradigm | Functional Core / Imperative Shell |
| Core signature | `[ResultType] = f([ConfigType], [StateSnapshotType], [InputEventType])` |
| Side-effect strategy | Action objects returned to Imperative Shell |
| Idempotency anchor | `[InputEvent.eventId or domain-specific idempotency field]` |
| Schema version | `[SCHEMA_VERSION]` |
| Config version | `[CONFIG_VERSION]` |

### 2.1 Core Guarantees

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

## 3. API Contract

The API contract is mandatory for every Yang Core Module.

All four schema blocks are required:

1. Configuration Schema
2. State Snapshot Schema
3. Input Event / Command Schema
4. Functional Result Schema

Partial schemas, undefined payloads, or placeholder-only contracts are incomplete.

Use JSON Schema as the primary language-agnostic contract format. TypeScript interfaces, Zod schemas, or other implementation-specific types may be derived later, but they are not the primary framework contract unless the project explicitly decides otherwise.

---

### 3.1 Configuration Schema

[Define static or versioned configuration.

Configuration contains rules, limits, thresholds, feature flags, retry policies, timeout values, compliance rules, and other stable settings that affect decisions.

Configuration must not contain runtime state, secrets, or user-specific live data.]

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "[MODULE_ID]/config/v[CONFIG_VERSION]",
  "title": "[MODULE_NAME] Configuration",
  "type": "object",
  "required": [
    "configVersion",
    "[REQUIRED_CONFIG_FIELD_1]",
    "[REQUIRED_CONFIG_FIELD_2]"
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
    "[REQUIRED_CONFIG_FIELD_2]": {
      "type": "[string | integer | boolean | number | object | array]",
      "description": "[What this configuration field controls]",
      "example": "[EXAMPLE_VALUE]"
    },
    "[OPTIONAL_FEATURE_FLAG]": {
      "type": "boolean",
      "description": "[What this flag enables or disables]",
      "default": false
    },
    "[OPTIONAL_THRESHOLD]": {
      "type": "number",
      "description": "[Threshold description and unit]",
      "example": 1000
    }
  }
}
```

#### Configuration Field Summary

| Field | Type | Required | Description | Example |
|---|---|---:|---|---|
| `configVersion` | integer | ✅ | Config schema version | `1` |
| `[REQUIRED_CONFIG_FIELD_1]` | [type] | ✅ | [Description] | `[example]` |
| `[REQUIRED_CONFIG_FIELD_2]` | [type] | ✅ | [Description] | `[example]` |
| `[OPTIONAL_FEATURE_FLAG]` | boolean | ❌ | [Description] | `false` |

---

### 3.2 State Snapshot Schema

[Define all runtime state injected into the core.

The Functional Core does not fetch this state itself. The Imperative Shell assembles the state snapshot and passes it into the core.

The State Snapshot is the complete list of external facts the core is allowed to know at decision time.]

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
      "description": "Injected current UTC time. The core must never read system time directly."
    },
    "[REQUIRED_STATE_FIELD_1]": {
      "type": "[string | object | array | boolean | integer | number]",
      "description": "[What this state field represents and where it comes from]"
    },
    "[OPTIONAL_PERMISSIONS_FIELD]": {
      "type": "object",
      "description": "[Actor permissions relevant to this module]",
      "additionalProperties": false,
      "properties": {
        "[PERMISSION_KEY]": {
          "type": "boolean",
          "description": "[What this permission grants]"
        }
      }
    },
    "[OPTIONAL_DEDUP_CACHE_FIELD]": {
      "type": "array",
      "description": "Processed idempotency anchors or event IDs used for duplicate detection.",
      "items": {
        "type": "string"
      }
    }
  }
}
```

#### State Field Summary

| Field | Type | Required | Description | Provided by |
|---|---|---:|---|---|
| `snapshotId` | string (uuid) | ✅ | Snapshot traceability ID | Imperative Shell |
| `currentTime` | string (date-time) | ✅ | Injected UTC time | Imperative Shell |
| `[REQUIRED_STATE_FIELD_1]` | [type] | ✅ | [Description] | [DB / cache / upstream service / caller] |
| `[OPTIONAL_PERMISSIONS_FIELD]` | object | ❌ | [Description] | [Auth service / session / policy engine] |
| `[OPTIONAL_DEDUP_CACHE_FIELD]` | string[] | ❌ | Deduplication state | [Cache / DB / idempotency store] |

---

### 3.3 Input Event / Command Schema

[Define the incoming event or command.

Use a discriminated-union pattern when multiple event types exist. Every union member must have a complete payload schema. Undefined payloads are incomplete.]

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "[MODULE_ID]/input-event/v[SCHEMA_VERSION]",
  "title": "[MODULE_NAME] Input Event",
  "oneOf": [
    {
      "title": "[EVENT_TYPE_1]",
      "type": "object",
      "required": [
        "eventId",
        "traceId",
        "correlationId",
        "eventType",
        "timestamp",
        "actor",
        "payload"
      ],
      "additionalProperties": false,
      "properties": {
        "eventId": {
          "type": "string",
          "format": "uuid",
          "description": "Globally unique event identifier. Used as the default idempotency anchor unless another domain-specific anchor is defined."
        },
        "traceId": {
          "type": "string",
          "description": "Distributed trace identifier propagated from the upstream caller."
        },
        "correlationId": {
          "type": "string",
          "description": "Business correlation ID linking related events, commands, sessions, transactions, or workflows."
        },
        "eventType": {
          "type": "string",
          "const": "[EVENT_TYPE_1]",
          "description": "Discriminator field."
        },
        "timestamp": {
          "type": "string",
          "format": "date-time",
          "description": "Event creation time in UTC ISO 8601."
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
          "description": "Event-type-specific payload for [EVENT_TYPE_1].",
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
  ]
}
```

If additional event types exist, add additional objects to the `oneOf` array. Each event type must define its own `eventType` discriminator and payload schema.

#### Input Event Field Summary

| Field | Type | Required | Description |
|---|---|---:|---|
| `eventId` | string (uuid) | ✅ | Default idempotency anchor |
| `traceId` | string | ✅ | Distributed trace propagation |
| `correlationId` | string | ✅ | Business correlation linkage |
| `eventType` | string | ✅ | Discriminator |
| `timestamp` | string (date-time) | ✅ | Event creation time UTC |
| `actor.actorId` | string | ✅ | Actor identifier |
| `actor.actorType` | enum | ✅ | `USER | SERVICE | ADMIN | SYSTEM` |
| `payload.[PAYLOAD_FIELD_1]` | [type] | ✅ | [Description] |

---

### 3.4 Functional Result Schema

[Define the full output of the Functional Core.

The result must be sufficient for the Imperative Shell to execute side effects without re-evaluating business logic.]

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "[MODULE_ID]/functional-result/v[SCHEMA_VERSION]",
  "title": "[MODULE_NAME] Functional Result",
  "type": "object",
  "required": [
    "resultId",
    "eventId",
    "traceId",
    "verdict",
    "decision",
    "reason",
    "actions",
    "telemetry",
    "auditLog"
  ],
  "additionalProperties": false,
  "properties": {
    "resultId": {
      "type": "string",
      "format": "uuid",
      "description": "Unique identifier for this result."
    },
    "eventId": {
      "type": "string",
      "format": "uuid",
      "description": "Input event ID."
    },
    "traceId": {
      "type": "string",
      "description": "Distributed trace identifier copied from input."
    },
    "verdict": {
      "type": "string",
      "enum": ["ALLOW", "DENY", "RETRY", "NOOP", "ERROR"],
      "description": "High-level outcome of the functional decision."
    },
    "decision": {
      "type": "string",
      "description": "Domain-specific decision code."
    },
    "reason": {
      "type": "string",
      "description": "Human-readable reason for the decision."
    },
    "actions": {
      "type": "array",
      "description": "Action objects proposed for the Imperative Shell.",
      "items": {
        "$ref": "#/$defs/Action"
      }
    },
    "telemetry": {
      "type": "object",
      "description": "Structured telemetry emitted by the core without sensitive data."
    },
    "auditLog": {
      "type": "object",
      "description": "Audit data needed to explain the decision."
    }
  },
  "$defs": {
    "Action": {
      "type": "object",
      "required": ["actionId", "actionType", "payload", "idempotencyKey"],
      "additionalProperties": false,
      "properties": {
        "actionId": {
          "type": "string",
          "format": "uuid"
        },
        "actionType": {
          "type": "string",
          "description": "Action type from the Action Registry."
        },
        "payload": {
          "type": "object",
          "description": "Action-specific payload."
        },
        "idempotencyKey": {
          "type": "string",
          "description": "Key used by the Imperative Shell to prevent duplicate side effects."
        }
      }
    }
  }
}
```

#### Functional Result Field Summary

| Field | Type | Required | Description |
|---|---|---:|---|
| `resultId` | string (uuid) | ✅ | Unique result ID |
| `eventId` | string (uuid) | ✅ | Input event ID |
| `traceId` | string | ✅ | Trace propagation |
| `verdict` | enum | ✅ | `ALLOW | DENY | RETRY | NOOP | ERROR` |
| `decision` | string | ✅ | Domain-specific decision code |
| `reason` | string | ✅ | Human-readable decision reason |
| `actions` | Action[] | ✅ | Proposed side effects for Imperative Shell |
| `telemetry` | object | ✅ | Non-sensitive telemetry |
| `auditLog` | object | ✅ | Audit explanation |

---

## 4. Decision Pipeline

[Define the ordered evaluation steps.

Every step should be deterministic and testable.]

| Step | Name | Input used | Decision / output | Failure behavior |
|---|---|---|---|---|
| 1 | [Validate input] | `InputEvent` | [Valid / invalid] | [Return ERROR / DENY] |
| 2 | [Check permissions] | `StateSnapshot`, `InputEvent.actor` | [Allowed / denied] | [Return DENY] |
| 3 | [Evaluate rule] | `Config`, `StateSnapshot`, `InputEvent.payload` | [Decision] | [Behavior] |

---

## 5. Decision Matrix

[Define important rule combinations and expected outcomes.]

| Case | Conditions | Verdict | Decision | Actions | Audit reason |
|---|---|---|---|---|---|
| [Case name] | [Condition set] | `[ALLOW | DENY | RETRY | NOOP | ERROR]` | `[DECISION_CODE]` | [Action types] | [Reason] |
| [Case name] | [Condition set] | `[ALLOW | DENY | RETRY | NOOP | ERROR]` | `[DECISION_CODE]` | [Action types] | [Reason] |

---

## 6. Action Registry

[Define every Action object the Functional Core may return.

The Functional Core does not execute actions.
The Imperative Shell executes actions.]

| Action type | Purpose | Payload schema / fields | Executed by | Idempotency key | Retry behavior |
|---|---|---|---|---|---|
| `[ACTION_TYPE]` | [Why this action exists] | [Fields] | [Shell / service / adapter] | [Key] | [Retry / no retry] |
| `[ACTION_TYPE]` | [Why this action exists] | [Fields] | [Shell / service / adapter] | [Key] | [Retry / no retry] |

### Action Object Rules

- Every action must have a stable `actionType`.
- Every action must include a safe idempotency key.
- Actions must not contain secrets.
- Actions must not require the Imperative Shell to re-evaluate business logic.
- If an action cannot be safely retried, state that explicitly.

---

## 7. Invariants

[Define rules that must never be violated.]

| Invariant | Why it matters | Verification method |
|---|---|---|
| [Invariant] | [Reason] | [Test / assertion / review] |
| [Invariant] | [Reason] | [Test / assertion / review] |

---

## 8. Idempotency and Duplicate Handling

[Define how repeated events, retries, duplicate commands, and partial side-effect execution are handled.]

**Idempotency anchor:** `[field]`

| Scenario | Expected behavior |
|---|---|
| Same event processed twice | [Behavior] |
| Action already executed | [Behavior] |
| Retry after transient failure | [Behavior] |
| Duplicate with changed payload | [Behavior] |

---

## 9. Error and Edge Case Behavior

[Define expected behavior for invalid input, missing state, unavailable dependencies, forbidden actions, and unexpected conditions.]

| Case | Detection | Expected result | Actions | Audit / telemetry |
|---|---|---|---|---|
| Missing required input | [How detected] | [ERROR / DENY / NOOP] | [None / action] | [What to record] |
| Invalid actor permissions | [How detected] | [DENY] | [None / action] | [What to record] |
| Missing state snapshot field | [How detected] | [ERROR] | [None / action] | [What to record] |
| Unsupported event type | [How detected] | [ERROR] | [None] | [What to record] |

---

## 10. Observability

[Define logs, metrics, traces, and telemetry generated by the Functional Core and/or Imperative Shell.

Do not include secrets or sensitive values.]

### 10.1 Logs

| Log event | Level | Fields | Redaction rule |
|---|---|---|---|
| `[LOG_EVENT]` | `[debug | info | warn | error]` | [Fields] | [What must be redacted] |

### 10.2 Metrics

| Metric | Type | Labels | Purpose |
|---|---|---|---|
| `[metric_name]` | `[counter | gauge | histogram]` | [Labels] | [Purpose] |

### 10.3 Trace Fields

| Field | Source | Purpose |
|---|---|---|
| `traceId` | Input event | Distributed trace propagation |
| `correlationId` | Input event | Business workflow grouping |
| `resultId` | Functional result | Result traceability |

---

## 11. Audit Requirements

[Define what must be recorded to explain decisions later.]

| Audit field | Required | Meaning | Sensitive? |
|---|---:|---|---|
| `eventId` | ✅ | Input event ID | No |
| `actorId` | ✅ | Actor identifier or redacted actor reference | Potentially |
| `decision` | ✅ | Decision code | No |
| `reason` | ✅ | Decision reason | No |
| `[FIELD]` | [Yes / No] | [Meaning] | [No / Potentially / Yes] |

### Audit Rules

- Audit entries must explain why the decision happened.
- Audit data must not include real secrets.
- Sensitive values must be redacted, hashed, tokenized, or replaced with safe references.
- Audit retention expectations must be defined elsewhere if retention is product- or compliance-specific.

---

## 12. Test Matrix

[Define tests needed to verify the contract.]

| Test ID | Scenario | Given | When | Then |
|---|---|---|---|---|
| `[TEST_ID]` | [Scenario] | [Config + StateSnapshot + InputEvent] | [Core runs] | [Expected FunctionalResult] |
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

## 13. Imperative Shell Responsibilities

[Define what the shell must do before and after calling the Functional Core.]

### 13.1 Before Calling the Core

- [ ] Load and validate `Config`.
- [ ] Assemble `StateSnapshot`.
- [ ] Validate or normalize `InputEvent`.
- [ ] Inject current time into `StateSnapshot`.
- [ ] Provide trace and correlation IDs.
- [ ] Ensure no secrets are passed unless explicitly allowed and safe.

### 13.2 After Calling the Core

- [ ] Execute returned Action objects.
- [ ] Enforce idempotency keys for side effects.
- [ ] Persist audit logs where required.
- [ ] Emit telemetry and traces.
- [ ] Handle retries according to action policy.
- [ ] Do not re-evaluate business logic outside the core.

---

## 14. Source Traceability

[Record where the technical contract came from.

Use source documents, Yin sections, source blocks, context packages, diagrams, existing code, tickets, or human decisions where known.

Do not invent sources.]

| Source | Type | Section / block | Contract element derived |
|---|---|---|---|
| [Source document/path] | [Yin Page / Master Document / existing code / issue / screenshot / other] | [Section or block ID] | [Schema / rule / action / invariant / test] |

---

## 15. Yin-to-Yang Trace Map

[Map relevant Yin concepts to Yang contract elements.]

| Yin concept / rule | Yang contract element | Status |
|---|---|---|
| [Yin rule or concept] | [Schema / decision step / action / invariant / test] | `[Covered | Partial | Missing | Open]` |
| [Yin rule or concept] | [Schema / decision step / action / invariant / test] | `[Covered | Partial | Missing | Open]` |

---

## 16. Open Questions / Contract Gaps

[Mark unresolved decisions, missing schemas, unclear state, missing source context, or contradictions.

Do not invent answers.]

- [Question or contract gap]
- [Question or contract gap]
- [Question or contract gap]

---

## 17. Pre-Flight Gap-Check

Before sending this Yang Core Module to an AI implementation agent, verify:

- [ ] The document is entirely in English.
- [ ] Document frontmatter is complete enough for deterministic retrieval.
- [ ] Matching Yin Page is linked or missing Yin is explicitly marked.
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

*This Yang Core Module is a technical execution contract. Implementation must satisfy this document rather than infer missing behavior.*
```
