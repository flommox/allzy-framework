---
id: "allzy.framework.docs.03.yin-yang-contracts"
title: "03 — Yin/Yang Contracts"
artifact_type: "Framework Documentation"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - yin-yang
  - contracts
---

# 03 — Yin/Yang Contracts

## Summary

Yin/Yang Contracts are the Allzy Framework's primary specification mechanism for turning human intent into implementation-safe AI execution context.

A Yin document explains the human, product, and domain meaning of a module. A Yang document defines the technical execution contract that an implementation agent or developer must satisfy. Yin prevents loss of intent. Yang prevents uncontrolled implementation invention. Together, they reduce hallucination risk, architectural drift, token waste, and ambiguous handoffs.

This document explains the Yin/Yang principle, the role of each document type, the template family, the Compact boundary, the Functional Core / Imperative Shell model, the required Yang contract structure, the Pre-Flight Gap-Check, metadata/traceability expectations, and the documentation lifecycle.

This document is explanatory framework documentation. It is not itself a reusable template.

The reusable templates are:

- `02_yin_template.md`
- `02_yin_template_compact.md`
- `03_yang_template.md`
- `04_yin_yang_template.md`
- `04_yin_yang_template_compact.md`

Filled examples belong in `examples/`. Examples show completed reference documents. They are not blank templates.

---

## Source Authority

The Allzy Framework documentation must be interpreted through the current finalized templates, prompts, examples, README structure, folder structure, and practical workflow decisions.

Older documentation and earlier master specifications are useful historical input, but they are not automatically correct. When an older document conflicts with the finalized templates, finalized prompts, finalized examples, or the current workflow, the finalized source files win.

The correct hierarchy is:

1. Finalized templates, prompts, examples, README files, and folder structure
2. Current practical workflow decisions
3. Explanatory docs such as this file
4. Older docs and previous master specifications as legacy input only

This matters because the framework has evolved through practical use. Outdated names, outdated file paths, and outdated workflow assumptions may still appear in drafts or older working material. They should not be preserved in current documentation unless they match the finalized source-of-truth files.

---

## Compact Terminology

The framework uses **Compact** as the official name for reduced-overhead variants.

The word order matters. Use `Genesis Compact`, not `Compact Genesis`.

`Compact` means the same framework method with smaller scope and lower overhead. It does not mean weaker quality, reduced safety, or permission to skip critical boundaries.

---

## The Yin/Yang Documentation Principle

Every non-trivial Allzy module should be specified from two complementary perspectives:

```text
Yin  = human intent, product meaning, domain rules, workflows, UI meaning, scope boundaries
Yang = technical execution contract, schemas, decision logic, actions, invariants, tests
```

Yin answers:

```text
What is this module?
Why does it exist?
Who uses it?
Which domain rules matter?
How should the system behave from a human and product perspective?
What is explicitly out of scope?
```

Yang answers:

```text
Which inputs are accepted?
Which runtime state is injected?
Which rules are evaluated?
Which decisions are possible?
Which outputs are returned?
Which side effects are proposed as Action objects?
Which invariants, edge cases, tests, and audit requirements must hold?
```

Neither layer replaces the other.

A Yin Page without a Yang contract can explain intent but cannot safely drive implementation of deterministic core logic.

A Yang Core Module without Yin can define rules but may lack the human context needed to understand why those rules exist and what product meaning they protect.

Together, they create a bounded, high-signal context package for AI-assisted implementation.

---

## Relationship to the Allzy Pipeline

Yin/Yang documents are created in **Phase 4: Specification**.

The full pipeline is:

1. **Genesis** — raw idea to Master Document
2. **Segmentation** — Master Document to Project Tree
3. **Modularization** — Project Tree to Modules and Submodules
4. **Specification** — Submodules to Yin/Yang Contracts
5. **Execution** — Contracts to prompts and code

Genesis does not create Yin/Yang documents.

Genesis Full produces a Master Document for larger products, platforms, systems, SaaS ideas, or major features. Genesis Compact produces a Compact Master Document for small tools, scripts, utilities, or low-risk tasks. Both are Phase 1 workflows. They may gather information that later helps Yin/Yang specification, but they must not create Yin Pages, Yang Core Modules, implementation plans, database schemas, APIs, code, or execution prompts.

Yin/Yang specification begins only after enough architecture decomposition exists to know what the actual implementable unit is.

This rule prevents premature contracts. A Yang Core Module written before segmentation and modularization are stable may describe the wrong boundary. It may later need to be split, merged, or discarded. The correct unit for full Yin/Yang specification is an implementable module or submodule, not an early idea fragment.

---

## Relationship to the Framework Layer Model

Yin/Yang Contracts are not limited to product Core features.

They may be used wherever human intent, technical execution rules, or implementation boundaries must be preserved clearly enough for AI-assisted work.

The Allzy Framework layer model is:

```text
Vision Layer
Infrastructure / Backend Layer
System Layer
Core Layer
Ecosystem Layer (optional)
Utilities Layer (optional)
```

Yin/Yang applies differently per layer.

| Layer | Typical Yin/Yang usage |
|---|---|
| Vision | Usually Yin-like strategic intent, roadmap, pricing, positioning, branding, and ecosystem context. Full Yang is rare unless deterministic planning or evaluation logic must be defined. |
| Infrastructure / Backend | Yang may be useful for deployment, queue, runtime, API, SDK, environment, backup, or operational contracts. Yin may explain why the infrastructure exists and which constraints shaped it. |
| System | Often needs strong Yang contracts because authentication, search, datastore, communication, observability, privacy, audit, and access logic require precise execution boundaries. |
| Core | The most common Yin/Yang target. Core contains product-specific business logic, workflows, domain rules, and customer-facing behavior. |
| Ecosystem | May use Yin/Yang when independent but connected products require shared contracts, integration boundaries, or cross-product workflows. |
| Utilities | May use Yin/Yang for tools such as prompt compilers, document processors, localization tools, research utilities, UI builders, or template libraries. |

The decision to create Yin/Yang is based on risk, complexity, and implementation ambiguity, not only on layer.

A Vision document may need no Yang.

A System or Core module may require Full Yin/Yang.

A small Utility feature may use Yin/Yang Compact.

A trivial copy or CSS fix may use a Direct Scoped Prompt.

The framework does not force every layer into the same document shape. It selects the smallest structure that safely preserves intent and execution boundaries.


---

## Yin/Yang Prompt Generator Workflow

The operational Yin/Yang prompt workflow is handled by:

```text
yin_yang_prompt_generator.md
```

This prompt is an **Agent-1 prompt generator**.

It does not directly create the final Yin/Yang document.

It creates a specialized Agent-2 prompt that tells a second AI agent how to generate the final specification document from the required source context and template.

```text
Agent 1 = Yin/Yang Prompt Generator
Agent 2 = Yin/Yang Specification Agent
```

### Agent 1 — Yin/Yang Prompt Generator

Agent 1 resolves:

- target artifact
- scope size
- source mode
- required template
- available source inputs
- target AI model
- target platform / execution environment
- language settings
- optimization/fallback status
- output filename strategy
- Existing Document Conversion Mode when enabled

Agent 1 produces the Agent-2 prompt.

Agent 1 must not create the final Yin/Yang document unless the user explicitly switches away from the generator workflow.

### Agent 2 — Yin/Yang Specification Agent

Agent 2 receives the generated prompt.

Agent 2 creates the final specification document.

Agent 2 must use the required attached/pasted/readable template as structural source of truth.

Agent 2 must not recreate the template from memory.

Agent 2 must not use a different template.

Agent 2 must not produce the final document if the required template content is missing and fallback is not explicitly allowed.

### Valid Target Artifacts

The generator may target one of these artifact combinations:

| Generation target | Scope size | Required artifact |
|---|---|---|
| `yin` | `full` | Yin Page |
| `yin` | `compact` | Compact Yin Page |
| `yang` | `full` | Yang Core Module |
| `yin_yang` | `full` | Yin/Yang Document |
| `yin_yang` | `compact` | Yin/Yang Compact |

Invalid combination:

```text
generation_target: yang
scope_size: compact
```

There is no standalone Yang Compact.

If a user requests Yang Compact, the correct response is to reject that combination and recommend either:

- full Yang Core Module
- Yin/Yang Compact
- Compact Yin
- Direct scoped prompt

depending on the work.

### Required Template Matrix

Agent 2 must use the correct template file.

| Target artifact | Required template |
|---|---|
| Yin Page | `02_yin_template.md` |
| Compact Yin Page | `02_yin_template_compact.md` |
| Yang Core Module | `03_yang_template.md` |
| Yin/Yang Document | `04_yin_yang_template.md` |
| Yin/Yang Compact | `04_yin_yang_template_compact.md` |

### Template Availability Rule

A repository link is only a pointer.

It helps the user find a template.

It does not count as attached template content.

The required template counts as available only if:

- the template file is attached
- the template text is pasted
- the execution environment has direct file access and can read it

Agent 2 needs the actual template content.

If the required template is missing, the generated prompt must clearly state that the final document cannot be produced reliably until the template is provided, unless the user explicitly allows a labeled fallback.

### Model and Platform Rule

The target AI model and the execution platform are separate.

Examples:

```text
Cursor       = platform
Claude Code  = platform
ChatGPT      = platform / execution environment
Codex CLI    = platform / execution environment
Claude       = model family
GPT          = model family
Gemini       = model family
Compose 2.6  = model
```

Do not infer model from platform.

Do not infer platform from model.

Model-optimized output requires model reference content.

Platform-optimized output requires platform reference content.

If references are missing, label the generated Agent-2 prompt as Universal Markdown fallback or platform-neutral/default as appropriate.

### Language Configuration

Yin and Yang output languages are configurable.

Default:

```yaml
yin_output_language: "English"
yang_output_language: "English"
document_output_language: "English"
technical_identifiers_language: "English"
```

Technical identifiers remain English unless explicitly overridden.

This allows human-facing Yin to be generated in a configured language while keeping technical identifiers stable and implementation-friendly.


---

## Existing Document Conversion Mode

The Yin/Yang Prompt Generator also supports **Existing Document Conversion Mode**.

Use this mode when the source input is an existing document, such as:

- old Markdown document
- product document
- architecture note
- specification
- research note
- project note
- mixed source document
- rough source material that should become a framework specification

The existing document is treated as source context.

It is not treated as the template.

Agent 2 must still use the required Allzy template.

### Conversion Config

The generator may include conversion settings such as:

```yaml
conversion:
  enabled: false
  source_document_type: "" # old_markdown | product_doc | architecture_note | specification | research_note | project_note | mixed | unknown
  preserve_source_meaning: true
  allow_restructure: true
  allow_inference: false
  mark_missing_as_open_questions: true
  mark_contract_gaps: true
  source_is_primary_context: true
```

### Conversion Rules

Agent 2 must preserve confirmed source meaning.

Agent 2 must preserve:

- confirmed intent
- rules
- workflows
- constraints
- domain facts
- technical facts
- known boundaries
- known dependencies
- known open issues

Agent 2 must not invent:

- product decisions
- business rules
- technical contract details
- schemas
- APIs
- database behavior
- side effects
- idempotency behavior
- permission logic
- security behavior
- persistence rules

Missing product decisions become Open Questions.

Missing technical execution details become Contract Gaps.

### Conversion Is Not Metadata Enrichment

Existing Document Conversion Mode is different from Document Metadata Enrichment.

| Workflow | Purpose |
|---|---|
| Document Metadata Enrichment | Add/update metadata/frontmatter while preserving document body |
| Existing Document Conversion Mode | Generate an Agent-2 prompt for converting source content into a Yin/Yang artifact using the required template |

Do not use Document Metadata Enrichment to create Yin/Yang documents.

Do not use Existing Document Conversion Mode merely to add frontmatter to a document.


## Template Family

The current Yin/Yang template family contains five core files.

| File | Role | Use when |
|---|---|---|
| `02_yin_template.md` | Full Yin Page | A module or larger product area needs complete human intent, domain, workflow, UI, role, dependency, and scope documentation |
| `02_yin_template_compact.md` | Compact Yin Page | A small or medium feature needs clear intent context but does not need a full technical execution contract |
| `03_yang_template.md` | Full Yang Core Module | A module defines architecture-relevant deterministic executable logic |
| `04_yin_yang_template.md` | Standard single-file Yin/Yang Template | A module needs complete Yin and complete Yang in one document |
| `04_yin_yang_template_compact.md` | Yin/Yang Compact | A small, self-contained, low-risk executable task needs more structure than a direct prompt but does not require a full Yang Core Module |

There is no separate Compact Yang template.

The generator combination `generation_target: yang` with `scope_size: compact` is invalid.

If a full Yang Core Module feels too heavy, the correct response is not to write a reduced Yang contract. Choose one of the following instead:

- use Compact Yin when only human intent context is needed
- use Yin/Yang Compact when a small executable task needs concise execution rules
- use a direct scoped prompt for trivial visual or copy-only fixes
- use full Yang when deterministic core logic, state, contracts, side effects, idempotency, permissions, or auditability matter

A partial Yang is dangerous because it looks like a contract while leaving undefined behavior. Undefined behavior is where AI systems invent.

---

## Examples vs. Templates

Templates are reusable structures with placeholders. They define the required shape, rules, and quality bar for future documents.

Examples are filled reference documents. They show how a completed document should look in practice. They may be used for learning, review, and calibration, but they must not be copied as if they were blank templates.

For example, a filled login/auth Yin/Yang example can demonstrate:

- a configured Yin output language
- a complete human-facing Yin layer
- a complete AI-facing Yang Core Module
- Functional Core / Imperative Shell separation
- Action objects returned by the core
- shell-only execution of side effects
- decision matrices
- action registries
- idempotency rules
- invariants
- errors and edge cases
- tests
- observability and audit requirements
- a Yin/Yang Trace Map

The example demonstrates the standard. The template defines the reusable structure.

---

## Yin Page

### Purpose

A Yin Page is the human-facing intent layer of a module.

It captures what the module is, why it exists, who it serves, how it is used, which domain rules matter, which boundaries must not be crossed, and which product or workflow meaning must remain stable across future implementation work.

A Yin Page is useful to:

- the architect, because it preserves intent and product reasoning
- product or design collaborators, because it explains behavior without code
- AI systems, because it provides semantic context during contract writing, review, debugging, and implementation handoff
- future maintainers, because it explains why the technical contract exists

A Yin Page is not source code. It is not a database schema. It is not an API contract. It is not a Functional Core specification. It is the source of truth for human intent and domain meaning.

### Yin Source of Truth

Yin is the source of truth for:

- product meaning
- target audience
- user, admin, operator, or system actors
- domain rules in human terms
- business or policy logic in human terms
- user-facing workflows
- UI and interaction meaning
- data concepts in human-readable form
- roles and permission expectations in human terms
- security and privacy expectations at the intent level
- integrations and dependencies at the product or domain level
- out-of-scope boundaries
- open product or domain questions

Yin is not the source of truth for:

- JSON schemas
- Functional Core signatures
- database schema design
- API route design
- TypeScript interfaces
- Zod schemas
- framework or library choices
- implementation algorithms
- side-effect execution mechanics
- deterministic decision matrices
- formal idempotency rules

Those belong in Yang when a technical execution contract is required.

### Yin Language Rule

A Yin document follows the configured `Yin output language` declared at the top of the document.

This makes Yin usable across teams, languages, and public/private contexts. For one project, Yin may be German. For another, it may be English or Spanish. The language is a document-level configuration, not a hardcoded framework requirement.

Technical identifiers remain English regardless of the Yin output language.

Technical identifiers include:

- module IDs
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

Yang documents are always written in English. The Yin output language does not change the Yang language rule.

### Yin Audience

The primary audience for Yin is human.

That includes:

- the architect
- product owners
- designers
- maintainers
- reviewers
- domain experts
- future AI sessions that need intent context

Yin must remain understandable without reading implementation code.

A good Yin Page lets a new reader answer:

```text
What is this module?
Why does it exist?
Who depends on it?
What does success mean?
Which behavior must not be changed accidentally?
Which assumptions are still open?
```

### Full Yin Required Sections

A full Yin Page should cover the following areas:

| Section | Purpose |
|---|---|
| Short Description | Concise human explanation of the module |
| Target Audience | Who uses or is affected by the module |
| Concept and Objective | The module's mental model and purpose |
| Problem / Motivation | Why the module exists |
| Core Value | What becomes better, safer, clearer, faster, or more reliable |
| Main Features | Product/domain capabilities in human terms |
| Domain Logic / Business Rules | Real-world rules the module must respect |
| Workflows | End-to-end behavior from trigger to outcome |
| UI Details and Interface | Screens, states, controls, feedback, and interaction meaning |
| Data Concepts and Field Definitions | Human-readable field dictionary, not a technical schema |
| Roles, Permissions, and Security | Intent-level access and security expectations |
| Integrations and Dependencies | Connected modules, systems, processes, or external services |
| Out of Scope | Explicit boundaries to prevent feature creep and AI invention |
| Example Application | One realistic scenario showing the module in use |
| Connection to the Core Module | Which Yin concepts require formal Yang specification |
| Open Questions | Missing decisions that must not be invented |
| Quality Checklist | Validation before using the Yin Page as source context |

If a section is not applicable, keep the heading and mark it as `Not applicable` with a short reason. Do not silently remove sections that reveal missing decisions.

### What Yin Must Not Contain

Yin must not contain:

- real API keys, passwords, tokens, private keys, or credentials
- complete JSON schemas as the primary content
- full database schema definitions
- Functional Core signatures as primary content
- implementation invariants as primary content
- API contracts as primary content
- library-specific implementation instructions
- code-level architecture decisions that belong in Yang
- hidden assumptions presented as facts
- private infrastructure details unless explicitly allowed by the project owner
- sensitive personal data unless explicitly allowed and necessary

Technical examples may appear as supporting explanation, but they must not become the main content.

### Compact Yin

Compact Yin is a shorter Yin-only document for smaller or medium-sized features that still need human intent context but do not justify the full Yin template.

Use Compact Yin when:

- the feature is small enough that full Yin would be excessive
- the work needs product/domain context
- the work does not yet require a formal technical execution contract
- the feature may later be expanded into a full Yin/Yang pair
- the primary risk is AI misunderstanding intent, not executing complex deterministic logic

Compact Yin preserves the most important Yin responsibilities:

- purpose
- target audience
- core value
- expected behavior
- domain rules
- UI or interaction notes
- data concepts
- out-of-scope boundaries
- Yang handoff notes if later needed
- open questions
- quality checklist

Compact Yin is not a technical execution contract. It does not replace Yang when Yang is required.

---

## Yang Core Module

### Purpose

A Yang Core Module is the AI-facing technical execution contract for a module.

It defines the deterministic logic that must be implemented, tested, audited, and maintained. It specifies the configuration, injected state, input events or commands, decision logic, result schema, action objects, invariants, idempotency behavior, error cases, observability, audit requirements, traceability, and implementation handoff constraints.

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
```

Yang is not final source code. It is the contract the implementation must satisfy.


### Core Layer vs. Yang Core Module

Do not confuse the **Core Layer** from the architecture model with a **Yang Core Module**.

| Term | Meaning |
|---|---|
| Core Layer | The product-specific business logic layer. It contains what the product actually does for users or customers. |
| Yang Core Module | A technical Functional Core contract. It defines deterministic executable logic for a module or submodule. |

A Core Layer feature may have a Yang Core Module.

A System Layer capability may also have a Yang Core Module.

An Infrastructure / Backend module may also have a Yang contract when deterministic execution rules, configuration, deployment behavior, or operational invariants must be defined.

The word `Core` in `Yang Core Module` refers to the Functional Core / Imperative Shell pattern. It does not mean that Yang is only allowed inside the product Core Layer.

This distinction prevents terminology drift:

```text
Core Layer = product/business layer.
Yang Core Module = technical execution contract.
```


### Yang Source of Truth

Yang is the source of truth for:

- technical execution boundaries
- Functional Core signature
- allowed inputs
- injected runtime state
- configuration rules
- decision pipeline
- decision matrix
- result schema
- Action objects
- Action Registry
- forbidden shell behavior
- invariants
- idempotency
- error and edge case behavior
- test cases
- observability and audit requirements
- traceability to Yin
- implementation handoff notes

Yang must translate relevant Yin concepts into explicit technical rules.

Yang may reference Yin for intent, but it must not duplicate long product prose. Product meaning belongs in Yin. Technical contract rules belong in Yang.

### English-Only Rule

All Yang prose must be written in English. No exceptions.

Technical identifiers are also English.

Mixed-language Yang documents are invalid and must be regenerated before use.

This rule exists because Yang is directly used as implementation context. English is the dominant language of code repositories, technical documentation, APIs, schemas, and model training data. An English Yang contract reduces translation ambiguity and improves consistency between contract and implementation.

### When Full Yang Is Required

Use a full Yang Core Module when any of the following apply:

- the module defines deterministic decision logic
- configuration affects decisions
- runtime state must be injected
- input events or commands must be validated
- outputs must be structured and testable
- side effects must be controlled through Action objects
- idempotency matters
- permissions or authorization rules are involved
- quotas, limits, retries, lockouts, or thresholds are involved
- persistence is affected
- queueing, jobs, webhooks, notifications, emails, or external side effects are coordinated
- API contracts are affected
- multiple systems depend on the result
- the module requires formal test cases
- observability, audit, compliance, or traceability matters
- changing the behavior later could create architecture drift

If any of these conditions apply, do not use Yin/Yang Compact as a substitute.

### No Compact Yang

There is no separate Compact Yang variant.

A reduced Yang contract is structurally unsafe because it can look authoritative while omitting the exact details that make Yang useful: schemas, decisions, actions, idempotency, edge cases, tests, and traceability.

If full Yang is too heavy for the task, choose the correct lower-overhead workflow:

| Situation | Correct format |
|---|---|
| Human intent is needed, but no execution contract | Compact Yin |
| Small executable task needs concise rules | Yin/Yang Compact |
| Trivial CSS/copy/label/spacing fix | Direct scoped prompt |
| Architecture-relevant executable logic | Full Yang |

Do not invent a partial Yang format.

---

## Functional Core / Imperative Shell

Every Yang Core Module follows the Functional Core / Imperative Shell pattern.

```text
Imperative Shell
  reads config, runtime state, input event
  calls Functional Core

Functional Core
  validates inputs
  checks injected state
  evaluates rules
  makes decisions
  returns Functional Result with Action objects

Imperative Shell
  receives Functional Result
  executes returned Action objects
  performs database writes, HTTP calls, queue publication, email sends, file I/O, metrics, and other side effects
```

The boundary is strict.

The Functional Core decides. The Imperative Shell executes.

The core must not perform I/O. The shell must not duplicate decision logic.

### Standard Core Signature

The canonical signature is:

```text
Result = f(Config, StateSnapshot, InputEvent)
```

Concrete modules may use domain-specific names:

```text
LoginResult        = f(LoginConfig, LoginStateSnapshot, LoginAttemptEvent)
NotificationResult = f(NotificationConfig, NotificationStateSnapshot, NotificationTrigger)
WebhookResult      = f(WebhookConfig, WebhookStateSnapshot, WebhookEvent)
```

The signature is not implementation syntax. It is a contract declaration.

### What the Functional Core May Do

The Functional Core may:

- validate inputs against defined schemas
- check permissions and authorization rules from injected state
- evaluate multi-step decision logic
- check limits, quotas, thresholds, lockouts, or conflicts
- produce structured results with explicit verdicts and decisions
- produce Action objects for the Imperative Shell
- structure telemetry, audit, and trace data
- return explicit errors, rejection decisions, retry instructions, or no-op decisions

### What the Functional Core Must Never Do

The Functional Core must never:

- write to a database
- read from a database
- send HTTP requests
- call external APIs
- read or write files
- publish to queues
- send emails
- send notifications
- read process environment variables directly
- read system time directly
- use hidden global state
- mutate external state
- generate random values unless the randomness is injected
- execute side effects outside returned Action objects

Runtime facts must be injected through `Config`, `StateSnapshot`, or `InputEvent`.

### What the Imperative Shell May Do

The Imperative Shell may:

- read external state
- assemble the `StateSnapshot`
- load configuration
- perform credential checks outside the core when appropriate
- call the Functional Core
- execute Action objects returned by the core
- write to databases
- publish to queues
- call APIs
- send emails or notifications
- emit metrics
- persist audit events
- enforce infrastructure-level retries or timeouts

### What the Imperative Shell Must Not Do

The Imperative Shell must not:

- invent business decisions not returned by the core
- duplicate decision logic from the core
- silently change the meaning of a core decision
- execute side effects that the core did not return unless they are infrastructure-level and explicitly allowed
- skip required actions without recording failure
- expose internal rejection reasons directly to end users when the contract forbids it
- resolve missing contract decisions by assumption

If the shell needs a decision not present in the Yang contract, the contract has a gap. The correct response is to update the Yang contract, not to hide decision logic inside the shell.

---

## Required Yang Contract Structure

A Yang Core Module must be complete enough that an implementation agent can implement and test the module without asking for missing technical decisions.

A complete Yang Core Module includes the following areas.

### 1. Domain Context

A concise factual explanation of:

- what the core computes
- which bounded context it belongs to
- which problem it solves at the technical contract level
- where it sits in the system
- upstream dependencies
- downstream dependents
- triggering event or entry point
- explicit out-of-scope boundaries

This section must not contain long product vision or user-story prose. That belongs in Yin.

### 2. Architecture Overview

The architecture overview declares:

- module name
- paradigm
- core signature
- side-effect strategy
- idempotency anchor
- schema version
- configuration version
- core guarantees

### 3. API Contract

The API Contract is mandatory for every Yang Core Module.

All four schema blocks are required:

1. Configuration Schema
2. State Snapshot Schema
3. Input Event / Command Schema
4. Functional Result Schema

JSON Schema is the primary language-agnostic contract format. TypeScript interfaces, Zod schemas, or other implementation-specific types may be derived later, but they do not replace the framework contract unless the project explicitly decides otherwise.

Partial schemas are incomplete. Placeholder-only schemas are incomplete. Undefined payloads are incomplete.

### 4. Decision Logic

The Yang contract must define:

- ordered decision pipeline
- early exits
- decision matrix
- allowed verdicts
- allowed decisions
- allowed rejection or error reasons
- branch behavior
- priority between checks
- fallback behavior for unknown or invalid cases

The decision pipeline must be explicit. The implementation agent must not infer the order of checks.

### 5. Actions for the Imperative Shell

All side effects are represented as Action objects.

The Yang contract must define:

- Action Registry
- allowed action types
- when each action is emitted
- action priority
- required parameters
- action idempotency key
- shell execution expectations
- forbidden shell behavior
- action sets by decision path when useful

The shell must be able to execute the action list without consulting hidden rules outside the contract.

### 6. Invariants

Invariants are conditions that must never break.

They may include:

- schema version invariants
- configuration version invariants
- required state presence
- allowed enum values
- required relationships between fields
- time handling rules
- identity consistency rules
- action registry consistency
- audit consistency
- side-effect boundary rules

If an invariant is violated, the Yang contract must define the result.

### 7. Idempotency Contract

Idempotency is mandatory when duplicate processing could create repeated side effects.

The contract must define:

- idempotency anchor
- where duplicate state is injected
- duplicate detection strategy
- result returned for duplicates
- whether actions are empty or replayed
- action-level idempotency keys
- dedup cache requirements if relevant
- shell responsibilities

A Yang contract without explicit duplicate behavior has a specification gap.

### 8. Errors and Edge Cases

The Yang contract must cover at minimum:

- invalid input
- missing permission
- missing state
- corrupt state
- contradictory configuration
- configuration version mismatch
- exceeded limit or quota
- duplicate event
- expired timestamp
- unknown event type
- conflict with existing state
- failed side-effect execution expectations where applicable
- forbidden or unsupported operation
- partial external failure if the module coordinates shell actions

Every case must define decision, reason, verdict, and actions where applicable.

### 9. Test Cases

A Yang Core Module must contain testable decision coverage.

Test cases should include:

- successful path
- each rejection path
- each invalid input path
- duplicate/idempotent path
- configuration mismatch path
- missing or corrupt state path
- edge cases around thresholds, time, limits, and boundary values
- action set expectations
- audit or telemetry expectations where relevant

If a decision path cannot be tested from the contract, the contract is incomplete.

### 10. Observability and Audit

The Yang contract must define observability expectations where relevant:

- metric names
- metric labels
- audit event fields
- trace IDs
- correlation IDs
- result IDs
- emitted telemetry
- retention or privacy notes if applicable
- redaction rules
- sensitive-value handling

Audit is not optional for security-sensitive or compliance-relevant logic.

### 11. Trace Map

The Trace Map links Yin intent to Yang contract elements.

It should show how:

- Yin domain rules map to Yang decision logic
- Yin data concepts map to schemas
- Yin workflows map to decision paths
- Yin roles and permissions map to authorization checks
- Yin security expectations map to audit and redaction rules
- Yin out-of-scope boundaries map to forbidden behavior
- Yin open questions map to Yang contract gaps where applicable

The Trace Map is the bridge from human intent to executable contract.

### 12. Open Questions / Contract Gaps

Open questions must be explicit.

Do not invent missing decisions.

An open question should state:

- what is unknown
- why it matters
- which section is affected
- whether the gap blocks implementation
- who must decide it

Contract gaps that affect executable behavior are blockers.

### 13. Pre-Flight Gap-Check

Before a Yang contract is used for implementation, it must pass a Pre-Flight Gap-Check.

The check verifies:

- all required schemas are complete
- no placeholders remain
- decisions are exhaustive
- action types are defined
- idempotency is explicit
- errors and edge cases are covered
- tests map to decisions
- audit and telemetry are defined where needed
- security rules are explicit
- traceability to Yin exists
- open questions are clearly marked
- blockers are not ignored

### 14. Implementation Handoff Notes

A Yang contract may include implementation handoff notes.

These notes should tell the implementation agent:

- which contract is authoritative
- what to implement
- which files or modules are expected to be affected if known
- what not to change
- which behavior must remain unchanged
- what to do when missing information is encountered
- which tests or checks must pass

Implementation notes must not weaken the contract.

---

## Structured Actions

Action objects are the framework mechanism for keeping side effects outside the Functional Core.

A typical Action object contains:

| Field | Purpose |
|---|---|
| `actionType` | Identifies what the shell must execute |
| `priority` | Defines execution order or priority |
| `parameters` | Contains all data needed for execution |
| `idempotencyKey` | Helps prevent duplicate execution |
| `reason` | Explains why the action was proposed |

Common action types may include:

- `CREATE_DATABASE_RECORD`
- `UPDATE_DATABASE_RECORD`
- `DELETE_DATABASE_RECORD`
- `CREATE_SESSION`
- `LOCK_ACCOUNT`
- `SEND_EMAIL`
- `SEND_NOTIFICATION`
- `PUBLISH_QUEUE_MESSAGE`
- `HTTP_POST_WEBHOOK`
- `SCHEDULE_RETRY`
- `UPDATE_DEDUP_CACHE`
- `EMIT_AUDIT_EVENT`
- `EMIT_METRIC`
- `ALERT_ADMIN`
- `REQUEST_APPROVAL`
- `REJECT_OPERATION`

The action set must be module-specific and exhaustive for the contract.

The core decides which actions are needed. The shell executes them.

A critical design rule follows:

```text
If an action requires a business decision, the core decides.
If an action is only the execution of a returned instruction, the shell executes.
```

For example, if an account should be locked after too many failed login attempts, the core must return a `LOCK_ACCOUNT` action. The shell must not independently decide to lock the account.

---

## Core Guarantees

Every valid Yang Core Module must satisfy these guarantees.

| Guarantee | Meaning |
|---|---|
| Deterministic | Same `Config`, `StateSnapshot`, and `InputEvent` produce the same result |
| Idempotent | Duplicate processing does not create uncontrolled repeated side effects |
| Side-effect-free | The Functional Core performs no I/O and mutates no external state |
| Schema-validatable | Inputs and outputs are defined through schemas |
| Testable | Decision paths can be tested without external services |
| Auditable | Decisions include reason, traceability, and audit data where relevant |
| Versionable | Schema and configuration versions are explicit |
| Bounded | The module does only what the contract says |
| Traceable | Yin intent maps to Yang rules, schemas, actions, and tests |

A contract that violates these guarantees is not a valid Yang Core Module.

---

## Yin/Yang Scope of Application

The framework should be applied with proportionality.

Too little structure creates ambiguity. Too much structure creates overhead. The goal is not to document everything equally. The goal is to choose the smallest format that safely preserves intent and execution boundaries.

### Scope Decision Table

| Scope | Format | Use when |
|---|---|---|
| Full Yin + Full Yang | `04_yin_yang_template.md` or separate `02_yin_template.md` + `03_yang_template.md` | A module has meaningful product intent and architecture-relevant executable logic |
| Full Yin only | `02_yin_template.md` | A larger product area or module needs complete human/domain documentation but no immediate technical execution contract |
| Compact Yin only | `02_yin_template_compact.md` | A smaller feature needs intent context but no technical execution contract |
| Full Yang only | `03_yang_template.md` | The human intent is already documented elsewhere and only the technical execution contract is being authored or updated |
| Yin/Yang Compact | `04_yin_yang_template_compact.md` | A small, self-contained, low-risk executable task needs concise intent and execution rules |
| Direct Scoped Prompt | No Yin/Yang template | A trivial isolated fix does not affect documented behavior, contracts, state, data flow, permissions, APIs, or persistence |

### Mandatory Full Yin/Yang

Use full Yin/Yang when the work involves:

- Core modules
- backend logic
- complex state management
- persistence
- APIs
- queues
- jobs
- event systems
- permissions
- authorization
- authentication
- security-sensitive behavior
- audit-relevant decisions
- compliance-relevant behavior
- deterministic business logic
- shared contracts used by other modules
- complex UI workflows that change persistent state
- multi-step workflows with failure states
- external integrations
- idempotency requirements

### Recommended Full Yin/Yang

Full Yin/Yang is recommended when:

- multiple actors interact with the module
- UI behavior coordinates with backend state
- the module will be maintained over time
- future AI sessions need stable context
- incorrect behavior would be expensive to debug
- unclear intent could cause implementation drift
- the module is small now but expected to grow

### Compact Yin

Use Compact Yin when:

- the task primarily needs product/domain clarity
- the feature is smaller than a full module
- a formal core contract would be premature
- there is no complex runtime state
- no side effects require Action objects
- no shared API contract is being defined
- no formal idempotency or audit contract is needed

### Yin/Yang Compact

Use Yin/Yang Compact when the task is:

- small
- self-contained
- low-risk
- executable
- bounded to known files or a narrow area
- more complex than a direct prompt
- not architecture-relevant enough for full Yang

Yin/Yang Compact may define:

- purpose
- expected behavior
- domain rules
- out-of-scope boundaries
- hard execution rules
- inputs
- outputs
- constraints
- forbidden actions
- error behavior
- acceptance criteria
- open questions
- quality checklist

Do not use Yin/Yang Compact when the task involves:

- database writes or migrations
- shared state
- public APIs or shared contracts
- permission or access-control systems
- queue, job, or event systems
- complex data flows
- multi-step coordinated workflows
- formal idempotency
- audit or telemetry requirements
- traceability requirements
- architecture-relevant Core Module logic

### Direct Scoped Prompt

Use a direct scoped prompt for:

- small CSS adjustments
- static copy edits
- label changes
- spacing fixes
- small visual alignment fixes
- isolated UI tweaks that do not affect behavior
- changes that do not touch contracts, state, data flow, permissions, APIs, or persistence

A direct scoped prompt should still include:

- exact target
- allowed files or area if known
- desired change
- out-of-scope boundaries
- acceptance criteria

A direct prompt is not a license for vague instructions.

---

## Metadata and Graph Requirements for Yin/Yang Documents

Yin/Yang documents should participate in the Deterministic Metadata Graph when used inside an Allzy Framework documentation set.

A Yin or Yang document should be readable by humans and selectable by tools.

That requires stable metadata.

Recommended frontmatter fields:

```yaml
---
id: "core.settings.input.yang"
title: "Settings Input — Yang Core Module"
document_type: "Yang Core Module"
layer: "Core"
module_id: "settings"
submodule_id: "settings.input"
parent: "core.settings"
paired_yin: "core.settings.input.yin"
paired_yang: null
schemas:
  - "core.settings.input.config.schema"
  - "core.settings.input.state.schema"
  - "core.settings.input.event.schema"
  - "core.settings.input.result.schema"
trace_map: "core.settings.input.trace"
source_block_id: "block-023"
generated_from: "master-document-v1.md"
status: "Review"
version: "0.2.0"
created: "2026-06-06"
updated: "2026-06-06"
tags:
  - settings
  - input
  - ui-state
  - deterministic-core
---
```

A Yin Page may use similar metadata:

```yaml
---
id: "core.settings.input.yin"
title: "Settings Input — Yin Page"
document_type: "Yin Page"
layer: "Core"
module_id: "settings"
submodule_id: "settings.input"
parent: "core.settings"
paired_yang: "core.settings.input.yang"
source_block_id: "block-023"
generated_from: "master-document-v1.md"
status: "Review"
version: "0.2.0"
tags:
  - settings
  - input
  - product-intent
  - ui-state
---
```

Metadata is not decoration.

It allows deterministic retrieval:

- find the Yin for a Yang contract
- find the Yang for a Yin page
- locate all documents for a module
- locate all documents for a submodule
- filter by layer
- filter by status
- retrieve related schemas
- trace generated documents back to source blocks
- prepare Agent-2 handoffs with correct context
- connect memory entries to the right contract

Yin/Yang documents should therefore declare their identity and relationships explicitly instead of relying on file names or semantic similarity alone.

### Metadata Minimum

Small projects may use a smaller header.

Minimum recommended fields:

```yaml
---
id:
title:
document_type:
layer:
status:
version:
tags:
---
```

For implementation-relevant Yin/Yang documents, add:

```yaml
module_id:
submodule_id:
paired_yin:
paired_yang:
source_block_id:
generated_from:
```

The full metadata model is defined in `04_Deterministic_Metadata_Graph.md`. This document only defines the Yin/Yang-specific expectations.


### Generator Metadata Expectations

Generated Yin/Yang documents should preserve source traceability where possible.

Recommended fields include:

```yaml
source_block_id: ""
generated_from: ""
module_id: ""
submodule_id: ""
paired_yin: ""
paired_yang: ""
```

If the document was created from an existing source document, include source metadata where appropriate:

```yaml
source:
  type: ""
  filename: ""
  path: ""
  source_document_id: ""
```

If a source field is unknown, leave it empty or mark it as uncertain.

Do not invent source IDs or file paths.


---

## Splice Source Block Traceability

Yin/Yang documents are often generated from segmented module or submodule blocks.

When a Yin/Yang document is generated from Splice or another block-processing workflow, it should preserve source traceability where possible.

Recommended fields:

```yaml
source_block_id: "block-023"
source_document: "master-document-v1.md"
generated_from: "splice-session-2026-06-06"
```

This creates a traceable chain:

```text
Master Document
→ Source Block
→ Yin Page
→ Yang Core Module
→ Agent Handoff
→ Implementation
→ Verification
```

Source block traceability helps when:

- a generated document seems incomplete
- a module boundary changes
- a block must be reprocessed
- a contract needs review against the original Master Document
- a later agent must understand where the requirement came from
- multiple generated documents must be compared or regenerated

Splice is not required by the framework, but block traceability is strongly recommended for large documentation sets.

---

## Yin/Yang as Documentation Source Material

Yin/Yang documents are operational framework artifacts first.

They may also become source material for user-facing or developer-facing documentation later.

Typical reuse:

- Yin can become human-facing module documentation, product explanation, workflow description, onboarding text, or feature documentation.
- Yang can become technical reference documentation, implementation notes, API behavior explanation, test guidance, or contract reference.

However, reuse must not corrupt the contract.

A Yin document should not be rewritten into marketing language if it is still used as source-of-truth intent.

A Yang document should not be softened into prose if implementation agents still depend on its MUST/NEVER rules, schemas, invariants, and tests.

If a public documentation version is needed, create a derived documentation artifact rather than weakening the original contract.


## Relationship to Maintenance and Triage

Yin/Yang Contracts remain relevant during maintenance.

When a bug appears, do not immediately patch code if the failure indicates a missing or incorrect contract. First determine whether the bug is:

1. an implementation error against a correct contract
2. a contract gap
3. a stale Yin/Yang document
4. a mismatch between Yin intent and Yang execution rules
5. a state management or handoff problem

If the contract is correct and the implementation is wrong, the implementation agent should fix the code against the existing Yang contract.

If the contract is missing behavior, update the Yang contract before implementation.

If the bug reveals missing product/domain intent, update Yin before updating Yang.

Triage follows the Agent 1 / Agent 2 separation:

- Agent 1 diagnoses and compiles a scoped handoff.
- Agent 1 does not write code.
- Agent 2 executes from the handoff.
- Agent 2 should receive only the context needed for the task.

A Triage handoff may reference relevant Yin/Yang contracts. It does not replace them.

---


## Relationship to Model/Platform-Aware Handoffs

Yang defines execution truth.

It does not automatically define the final prompt shape for every target AI model or execution platform.

A Yang Core Module may contain Implementation Handoff Notes, but the final Agent-2 handoff may still need to be rendered differently depending on:

- target AI model
- target platform / execution environment
- available tools
- file access model
- expected patch format
- output conventions
- model-specific prompting reference
- platform-specific execution reference

The separation is:

```text
Yang = technical execution contract
Triage / handoff renderer = scoped task delivery
Reference Package / future Prism Registry = model/platform adaptation
```

Therefore:

- A Yang document should not claim model-specific optimization by itself.
- A Yang document may provide the source material for an optimized handoff.
- A model-optimized handoff requires a matching model reference.
- A platform-optimized handoff requires a matching platform reference.
- If references are missing, the handoff should be labeled as Universal Markdown fallback.

This keeps the contract stable while allowing handoffs to adapt to Claude Code, Cursor, Codex CLI, ChatGPT, Gemini/Antigravity-style environments, or other target platforms.


## Relationship to State Management

Yin/Yang Contracts define product intent and technical execution contracts. They are not a replacement for project/session state files.

Use:

```text
plan.md   = current task focus
memory.md = confirmed current project and architecture memory
handoff   = scoped execution context for Agent 2
```

`plan.md` may point to the Yin/Yang contract being worked on.

`memory.md` may record confirmed changes after implementation. It should not preserve failed attempts, debug noise, or obsolete states.

When a confirmed implementation change affects behavior, contracts, state flows, public APIs, persistence, security, or architecture, the relevant Yin/Yang documents should be updated. `memory.md` can stage the fact that a documentation update is needed, but it is not itself the final contract.


Yin/Yang contracts and state files must not replace each other.

Use this rule:

```text
Contract changes first.
Memory records confirmed current truth after verification.
```

If implementation changes confirmed behavior, update the relevant Yin/Yang documents when the change affects intent, business logic, state flow, API behavior, persistence, security, privacy, or technical execution rules.

Only after the behavior is confirmed should `memory.md` record it as current project truth.

If an issue is unresolved, `memory.md` may temporarily contain compact troubleshooting notes, but those notes do not override Yin or Yang.


---

## Pre-Flight Gap-Check

The Pre-Flight Gap-Check is the validation pass before using a Yin/Yang document for implementation.

It catches the Illusion of Precision: documents that look complete because they are structured, but still omit critical behavior.

### Yin Pre-Flight Questions

Before using a Yin Page as source context, verify:

- Is the configured Yin output language followed?
- Are technical identifiers still in English?
- Is the module understandable without reading code?
- Is the target audience clear?
- Is the core value clear?
- Are domain rules explicit?
- Are workflows concrete?
- Are UI and interaction meanings clear where relevant?
- Are data concepts listed in human terms?
- Are roles, permission expectations, security, and privacy visible?
- Are integrations and dependencies listed?
- Are out-of-scope boundaries explicit?
- Are open questions marked instead of invented?
- Can a matching Yang contract be logically derived from the Yin Page?
- Are secrets, tokens, passwords, and private credentials absent?

### Yang Pre-Flight Questions

Before using a Yang contract for implementation, verify:

- Is the document entirely in English?
- Is the Functional Core / Imperative Shell boundary clear?
- Is the core signature explicit?
- Are Configuration, State Snapshot, Input Event / Command, and Functional Result schemas complete?
- Are schema versions and config versions explicit?
- Is the decision pipeline ordered?
- Is the decision matrix exhaustive?
- Are all verdicts, decisions, and reasons defined?
- Is the Action Registry complete?
- Are action parameters defined?
- Are forbidden shell behaviors listed?
- Is idempotency defined?
- Are duplicates safe?
- Are invariants defined?
- Are all relevant errors and edge cases covered?
- Are tests mapped to decisions?
- Are observability and audit requirements defined where relevant?
- Is the Trace Map present?
- Are open questions or contract gaps clearly marked?
- Are blockers resolved before implementation?
- Are secrets absent?

### Compact Pre-Flight Questions

Before using Yin/Yang Compact, verify:

- Is the task small, self-contained, and low-risk?
- Does it avoid database writes, shared state, APIs, permissions, queues, jobs, complex data flows, and Core Module logic?
- Are hard rules explicit?
- Are inputs and outputs clear?
- Are forbidden actions listed?
- Is error behavior defined?
- Are acceptance criteria testable?
- Are open questions marked?

If any answer indicates architectural relevance, do not use Yin/Yang Compact. Use full Yin/Yang or full Yang.

---

## Yin/Yang Trace Map

The Trace Map is the explicit link between human intent and technical execution.

It prevents a common failure mode: Yang implements rules that are technically plausible but not traceable to Yin intent.

A basic Trace Map should include:

| Yin source | Yang destination | Purpose |
|---|---|---|
| Domain rule | Decision pipeline / decision matrix | Ensures product rules become executable checks |
| Workflow step | Decision path / action set | Ensures user/system flows become implemented outcomes |
| Data concept | Schema field | Ensures human data meaning maps to structured input/output |
| Role or permission expectation | Authorization check | Ensures access rules are enforced |
| Security expectation | Audit, redaction, or rejection behavior | Ensures privacy/security requirements become contract rules |
| Out-of-scope boundary | Forbidden behavior | Ensures the implementation does not expand scope |
| Open question | Contract gap | Ensures unresolved decisions are not silently invented |

A Trace Map does not need to repeat the entire document. It needs to prove that every important intent statement has a corresponding technical home.

---

## Docs-First Update Workflow

For any change that affects documented behavior, module logic, contracts, state, data flows, permissions, APIs, persistence, audit, or integration boundaries, the update sequence is:

1. Update the Yin document if intent, domain behavior, workflow meaning, or product scope changes.
2. Update the Yang document if technical execution logic, schemas, decisions, actions, invariants, tests, audit, or traceability changes.
3. Run the Pre-Flight Gap-Check.
4. Provide the updated contract to the implementation agent.
5. Implement or regenerate the affected code from the updated contract.
6. Verify behavior against acceptance criteria and tests.
7. Update `memory.md` only after the change is confirmed and intentionally kept.

Do not patch implementation first when the contract is wrong.

Code-first patching creates Documentation Drift. The next AI session will operate from stale contracts and may reintroduce the same bug or produce incompatible behavior.

### Trivial Fix Exception

The full Docs-First workflow is not required for trivial isolated changes that do not affect behavior or contracts.

Examples:

- CSS spacing
- visual alignment
- static copy
- one-off label correction
- isolated UI polish
- non-behavioral formatting

The criterion is not file size. The criterion is whether the change touches documented behavior, logic, state, contracts, permissions, APIs, persistence, audit, or integration boundaries.

If it does, Docs-First applies.

---

## Documentation-Driven Debugging

When a bug occurs, classify it before patching.

| Bug class | Correct response |
|---|---|
| Implementation violates correct Yang | Fix implementation against the Yang contract |
| Yang omits required behavior | Update Yang first, then implement |
| Yin omits domain intent | Update Yin first, then update Yang if needed |
| Yin and Yang conflict | Stop and reconcile the documents before implementation |
| Contract is correct but state handoff is wrong | Fix `plan.md`, `memory.md`, or the Agent-2 handoff context |
| Bug is outside current scope | Record it separately; do not expand the current task |

A bug fix that changes intended behavior must be promoted into documentation. Otherwise the system's documented truth diverges from the running system.

---

## Named Anti-Patterns

### Illusion of Precision

A document appears complete because it is structured and detailed, but important behavior is still undefined.

Symptoms:

- many headings, few decisions
- schemas with placeholder fields
- decision values not exhaustively defined
- action types listed but not parameterized
- edge cases acknowledged but not resolved
- open questions hidden or omitted
- tests not mapped to decision paths

The fix is not more prose. The fix is to close the missing decisions or mark them as contract gaps.

### Documentation Drift

The implementation changes but Yin/Yang documents remain unchanged.

Symptoms:

- code behavior no longer matches Yang
- UI behavior no longer matches Yin
- maintenance agents follow outdated contracts
- bugs reappear after later regeneration
- future prompts require re-explaining context manually

The fix is Docs-First discipline and confirmed-state updates after implementation.

### Eager Execution

An AI agent patches the visible symptom before understanding the contract.

Symptoms:

- local fix appears correct
- root cause remains
- adjacent behavior breaks
- shell gains hidden decision logic
- state synchronization becomes inconsistent
- documentation is not updated

The fix is to separate diagnosis, contract review, and implementation.

### Contract Theater

A document uses formal words such as schema, invariant, idempotency, or audit, but does not define them concretely.

Symptoms:

- “handle errors gracefully”
- “ensure idempotency”
- “log everything”
- “validate input”
- “follow best practices”
- “create appropriate actions”

These are not contract statements. A contract must define exact behavior.

### Shell Decision Leakage

Business or domain decisions leak into the Imperative Shell.

Symptoms:

- shell decides whether to lock an account
- shell decides whether to send a domain notification
- shell decides whether a request is approved
- shell evaluates thresholds that should belong to core logic
- shell changes rejection reasons

The fix is to move decisions into the Functional Core and return explicit Action objects.

### Scope Inflation

A focused module contract grows to include adjacent features, future roadmap items, or unrelated fixes.

Symptoms:

- one Yin Page describes multiple unrelated concerns
- one Yang contract touches multiple independent decision systems
- one prompt batches several modules
- out-of-scope boundaries are missing
- examples become hidden requirements

The fix is modularization, explicit scope boundaries, and separate documents.

---

## Quality Bar

A Yin/Yang document is ready for implementation only when a qualified reviewer can answer:

```text
What is this module?
Why does it exist?
Who uses it?
Which behavior is required?
Which behavior is forbidden?
Which inputs are accepted?
Which state is injected?
Which decisions can be made?
Which actions may be returned?
Which side effects are outside the core?
Which edge cases are covered?
Which tests prove the behavior?
Which open questions remain?
```

If any answer requires guessing, the document is not ready.

---

## Website-Ready Summary

Yin/Yang Contracts are the Allzy Framework's method for separating human intent from technical execution.

Yin explains what a module means: the people, workflows, rules, boundaries, and domain context behind it.

Yang defines how the module must execute: inputs, state, decisions, outputs, actions, invariants, tests, audit, and traceability.

This separation gives AI systems the context they need without letting them invent missing architecture. Human intent stays readable. Technical behavior stays testable. Side effects stay outside the Functional Core. Open questions stay visible instead of becoming hidden assumptions.

Use Full Yin/Yang for architecture-relevant modules. Use Compact formats only for smaller, lower-risk work. Use direct prompts only for trivial isolated fixes.

Yin/Yang documents can apply across the framework layer model: Vision, Infrastructure / Backend, System, Core, Ecosystem, and Utilities. They should participate in the Deterministic Metadata Graph through stable IDs, metadata, paired links, and source block traceability when used inside a larger documentation set.

Yang defines execution truth. Triage, Reference Packages, and future Prism Registry workflows may render that truth into model/platform-aware Agent-2 handoffs.

The goal is not more documentation. The goal is fewer guesses.


---

## Yin/Yang Generation Workflow

The recommended operational workflow is:

```text
1. Genesis creates Master Document or Master Document Compact.
2. Segmentation and Modularization identify the module/submodule/block.
3. User provides the relevant source block or existing source document.
4. User provides the required template content.
5. User identifies target AI model and optional target platform.
6. Agent 1 runs `yin_yang_prompt_generator.md`.
7. Agent 1 creates a specialized Agent-2 prompt.
8. Agent 2 uses the generated prompt and required template.
9. Agent 2 creates the final Yin/Yang specification document.
10. Human reviews and accepts or requests correction.
```

This keeps the generator focused.

The generator creates the execution prompt.

The specification agent creates the document.

The template defines the structure.

The source context defines the content.

### Prompt + Template + Source Context

Yin/Yang generation should normally work as:

```text
Prompt + Template + Block / Document Input
```

Do not embed every possible template, example, source, and framework rule into one giant prompt when smaller structured inputs are available.

The prompt instructs.

The template structures.

The source block/document supplies content.

The metadata links the output back to its source.


## Anti-Patterns


Additional anti-patterns:

- treating a repository link as attached template content
- asking Agent 2 to recreate a template from memory
- using a source document as if it were the template
- using Document Metadata Enrichment as Yin/Yang conversion
- inventing missing contract details during conversion
- generating standalone Yang Compact
- inferring model from platform or platform from model
