---
id: "allzy.framework.docs.02.architecture"
title: "02 — Architecture"
artifact_type: "Framework Documentation"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - architecture
---

# 02 — Architecture

## Summary

Architecture in the Allzy Framework does not primarily mean the architecture of one software product. It means the architecture of the method that turns a raw idea into an implementable, testable, maintainable product through AI-assisted specification.

The framework is built around one practical goal:

```text
Make the AI execute instead of guess.
```

To achieve that, the framework front-loads human thinking, AI-assisted clarification, decomposition, specification, contract writing, and context preparation before implementation begins. The implementation agent should receive a small, precise, well-scoped task with enough context to act safely.

The Allzy Framework architecture has five major dimensions:

1. **Pipeline architecture** — how an idea moves through Genesis, Segmentation, Modularization, Specification, and Execution.
2. **Layer architecture** — how Vision, Infrastructure / Backend, System, Core, Ecosystem, and Utilities relate.
3. **Documentation architecture** — how Master Documents, modules, submodules, Yin/Yang contracts, state files, handoffs, and metadata relationships work together.
4. **Workspace context architecture** — how `plan.md`, `memory.md`, `context_retrieval.md`, context packages, Search Logs, metadata indexes, and optional skills prepare a target implementation workspace.
5. **AI execution architecture** — how prompts, model references, platform references, triage, state management, and implementation agents are coordinated.

The framework is not code-first. It is specification-first.

The intended balance is closer to:

```text
More thinking, decomposition, documentation, and verification before coding.
Less guessing, rework, and debugging during coding.
```

The exact ratio will vary by project, but the principle is stable: the more complete the specification, the less the implementation agent must infer.

---

## Source Authority

This document is based on the current Allzy Framework workflow, finalized prompts, finalized templates, finalized examples, README/folder structure decisions, and practical usage decisions.

Older documentation and previous master specifications are useful input, but they are not automatically correct. If an older document conflicts with finalized templates, finalized prompts, finalized examples, current state-management rules, current triage rules, or the current practical workflow, the current source-of-truth files win.

This document is explanatory framework documentation. It is not itself a copy-ready prompt, template, or implementation contract.

---

## What Architecture Means Here

In this document, architecture means the structural method by which the framework organizes work.

It answers:

- How does a raw idea become a complete Master Document?
- How does the Master Document become an architecture tree?
- How are topics segmented into modules and submodules?
- When are Yin/Yang documents created?
- How does specification become implementation?
- What is reusable across products?
- What changes per product?
- How are AI agents prevented from guessing?
- How are model and platform differences handled?
- How is context preserved across sessions?
- How are bugs and maintenance handled without broad rework?

This is not a single product architecture diagram. It is the architecture of an AI-assisted software engineering workflow.

---

## Core Architecture Principle

The Allzy Framework separates work into layers and phases so that each AI interaction receives the correct context at the correct time.

The framework does not ask an AI to infer the whole product from a vague instruction.

Instead, it creates a chain:

```text
Idea
→ Vision
→ Infrastructure / Backend decisions
→ System capabilities
→ Core product logic
→ Modules
→ Submodules
→ Yin/Yang contracts
→ Workspace context setup
→ Agent handoffs
→ Implementation
→ Verification
→ State update
```

The architect and the framework do the thinking before implementation. The implementation agent receives the results of that thinking.

This is why the implementation step can be smaller, cheaper, faster, and safer than in code-first workflows.

---

# 1. The Five-Phase Pipeline

The Allzy Framework uses a five-phase pipeline.

```text
1. Genesis
2. Segmentation
3. Modularization
4. Specification
5. Execution
```

Each phase has a distinct job. A later phase must not be performed prematurely inside an earlier phase.

The pipeline is intentionally strict because most AI failure starts when phases are mixed:

- Genesis starts generating architecture too early.
- Segmentation invents implementation details.
- Modularization skips boundaries.
- Specification happens before module structure is stable.
- Execution begins before contracts are complete.

The framework prevents that by assigning one job to each phase.

---

## Phase 1 — Genesis

### Purpose

Genesis is the collaborative human/AI ideation and requirements phase.

It turns raw, unstructured human intent into a complete Master Document.

Genesis is not passive intake. It is a working conversation between the human architect and an AI assistant.

The human brings:

- ideas
- goals
- constraints
- product intuition
- business context
- workflows
- preferences
- rejected directions
- open concerns

The AI helps:

- clarify the idea
- ask missing questions
- challenge weak assumptions
- identify risks
- suggest possible features
- suggest what should not be included
- organize the conversation
- separate confirmed decisions from assumptions
- preserve deferred ideas
- prepare the final Master Document

Genesis continues until the idea is clear enough that later phases can proceed without guessing.

### Genesis Output

Genesis produces:

```text
Master Document
```

For smaller projects, it may produce:

```text
Master Document Compact
```

The Master Document captures the complete discussed context.

It may include:

- product identity
- purpose
- target audience
- problem / motivation
- core value
- workflows
- first-release scope
- future ideas
- out-of-scope boundaries
- data/content expectations
- constraints
- privacy/security/compliance notes
- success criteria
- confirmed decisions
- rejected ideas
- deferred ideas
- open questions
- Phase 2 Segmentation inputs

Genesis may prepare information that later helps architecture, segmentation, or Yin/Yang specification, but it does not perform those phases.

### What Genesis Must Not Do

Genesis must not create:

- final architecture
- final modules
- final submodules
- Project Tree
- Yin Pages
- Yang Core Modules
- Functional Core / Imperative Shell contracts
- JSON schemas
- API contracts
- database schemas
- implementation plans
- execution prompts
- code

This boundary matters.

If Genesis creates modules or contracts too early, the framework loses the ability to see the full product before decomposition. Early contracts often target the wrong unit and must later be discarded.

### Genesis Full and Genesis Compact

The framework supports two Genesis scales.

| Workflow | Output | Use when |
|---|---|---|
| Genesis Full | Master Document | Large products, platforms, systems, SaaS ideas, major features, or long-lived products |
| Genesis Compact | Master Document Compact | Small tools, scripts, utilities, low-risk tasks, or narrow ideas |

Genesis Compact is not a weaker method. It is a smaller version for smaller scope.

Both workflows remain Phase 1. Both must avoid architecture, modules, Yin/Yang, implementation plans, and code.

### Genesis and the Vision Layer

Genesis creates the first version of the Vision Layer.

The Vision Layer is the product's strategic and conceptual foundation:

- what the product is
- why it should exist
- who it serves
- what it must become
- what it must not become
- strategic direction
- roadmap direction
- branding direction
- pricing direction
- ecosystem direction
- future product intent

The Vision Layer is not implementation. It is the north star for later decomposition.

---

## Phase 2 — Segmentation

### Purpose

Segmentation turns the Master Document into structured topic blocks.

It identifies:

- product areas
- feature areas
- strategy areas
- infrastructure concerns
- system capabilities
- core product logic
- optional ecosystem areas
- utilities or tooling areas
- privacy/security concerns
- data/content areas
- user workflows
- operational concerns
- dependencies and boundaries

Segmentation is the first structural pass.

It does not yet need to finalize every module. Its job is to reveal the shape of the product.

### Segmentation Output

Segmentation produces:

```text
Project Tree
Topic Blocks
Category Blocks
Potential Module Areas
Potential Boundary Notes
```

The output may be processed manually, through Splice, or through another block workflow.

### Why Segmentation Exists

A Master Document can contain many ideas. If the framework jumps directly from a Master Document to implementation, the AI must decide the structure itself.

That creates risk:

- important concerns are merged
- unrelated workflows are grouped
- hidden dependencies are missed
- implementation units become too large
- contracts are written for the wrong boundaries

Segmentation prevents that by exposing the structure before specification begins.

---

## Phase 3 — Modularization

### Purpose

Modularization turns segmented topic areas into modules and submodules.

A module is a larger functional or architectural area.

A submodule is a smaller independent responsibility inside a module.

The goal is to produce implementable units.

```text
Master Document
→ Segmented Areas
→ Modules
→ Submodules
```

### Module

A module is a coherent area of responsibility.

Examples:

- Account Management
- Search
- Notifications
- Billing
- Settings
- Content Publishing
- Analytics
- Customer Support
- Automation
- Workspace Management

A module may contain multiple submodules.

### Submodule

A submodule is a focused, independently implementable unit.

Examples:

- create notification
- resolve user permission
- update workspace setting
- validate import file
- generate report summary
- handle failed payment state
- sync external account
- apply content visibility rule

A submodule should be small enough that one focused AI work session can implement or modify it safely.

If a submodule requires multiple unrelated sessions, it is probably too large.

### Why Modularization Matters

AI systems perform better when the task boundary is small and explicit.

Modularization reduces:

- guessing
- hallucination
- broad repository exploration
- scope drift
- token cost
- test ambiguity
- review difficulty
- rework

The smaller and clearer the module, the less the implementation agent must infer.

### Module and Submodule Documentation

A module may receive documentation at multiple levels:

- module overview
- module Yin Page
- module Yang contract if the module itself has deterministic logic
- submodule Yin/Yang documents
- schemas
- trace maps
- API contracts
- implementation handoffs

Not every module needs every document type.

The framework chooses the smallest documentation set that safely preserves intent and execution boundaries.

---

## Phase 4 — Specification

### Purpose

Specification turns modules and submodules into usable documents for AI-assisted implementation.

This is where formal Yin/Yang documents are created.

Yin/Yang documents are not created in Genesis.

They are not created before modularization is stable.

They are created only after the framework knows what the implementable unit is.

### Yin/Yang Specification

Yin and Yang separate human intent from technical execution.

```text
Yin  = human intent, product meaning, domain rules, workflows, UI meaning, scope boundaries
Yang = technical execution contract, schemas, decision logic, actions, invariants, tests
```

Yin answers:

- what this module is
- why it exists
- who uses it
- which domain rules matter
- what is out of scope

Yang answers:

- which inputs are accepted
- which state is injected
- which decisions are allowed
- which outputs are produced
- which actions are returned
- which invariants and tests must hold

### Full, Compact, and Direct Scope

Specification scales by task size.

| Scope | Use when |
|---|---|
| Full Yin/Yang | Non-trivial modules, backend logic, stateful flows, APIs, permissions, audit, persistence, or deterministic business logic |
| Compact Yin | Smaller features need intent context but no formal execution contract |
| Yin/Yang Compact | Small, self-contained, low-risk executable tasks need concise intent and execution rules |
| Direct Scoped Prompt | Trivial CSS, copy, label, spacing, or isolated visual fixes with no contract/state impact |

There is no separate Compact Yang.

When Yang is needed, it must be complete enough to prevent AI invention.

### Splice and Block Processing

After segmentation and modularization, projects may have dozens or hundreds of blocks.

Processing them as one large prompt is unsafe and expensive.

Splice or an equivalent block-processing workflow can be used to process blocks one at a time.

A typical workflow:

1. Prepare the Master Document or overview document.
2. Prepare the module/submodule blocks.
3. Add the relevant Yin/Yang template or prompt as reference.
4. Process one block at a time.
5. Generate one Yin/Yang document or specification artifact per block.
6. Review each output.
7. Store the accepted documents in the documentation set.
8. Use them later for implementation, review, or handoff.

Splice is not the framework itself. It is a practical workbench for safely applying the framework to many blocks.

---

## Phase 5 — Execution

### Purpose

Execution turns specifications into implementation work.

Execution should not begin from raw ideas.

It should begin from:

- a completed contract
- a focused plan
- a scoped handoff
- acceptance criteria
- relevant state excerpts
- relevant model/platform references when optimization is needed

### Execution Inputs

Execution may use:

- Yin/Yang contracts
- implementation handoff
- `plan.md`
- relevant `memory.md` excerpts
- schemas
- trace maps
- model references
- platform references
- Prompt Library / Reference Package
- metadata graph references
- `context_retrieval.md`
- `context_package.md`
- Search Log where deterministic retrieval was used
- current code inspection
- tests
- acceptance criteria

### Execution Units

The default execution unit is small:

```text
one submodule
one bug
one topic
one narrow functional area
```

Do not batch unrelated work.

Batching increases token use and hallucination risk because the model reasons across unrelated concerns simultaneously.

### Execution Agents

Implementation can be performed by different agents or platforms:

- coding assistant
- IDE agent
- CLI agent
- hosted coding agent
- local model
- code review agent
- future automated pipeline

The framework does not prescribe one execution platform.

It prescribes the structure of the handoff.

### Execution Output

Agent output should include:

- what changed
- files changed
- tests or checks run
- verification result
- unresolved blockers
- out-of-scope items not touched
- documentation updates needed

Execution is not complete until verification is performed.

---

# 2. Allzy Framework Layer Model

The framework uses a layer model to separate strategy, infrastructure, shared system capabilities, product-specific logic, optional ecosystems, and tooling.

Recommended layers:

```text
Vision Layer
Infrastructure / Backend Layer
System Layer
Core Layer
Ecosystem Layer (optional)
Utilities Layer (optional)
```

The key principle:

```text
Infrastructure and System are reusable.
Core is replaceable.
```

A project invests once into Infrastructure and System capabilities. Those capabilities can be reused across future products. The Core changes when the product idea changes.

---

## Vision Layer

The Vision Layer contains the strategic and conceptual foundation.

It includes:

- product concept
- purpose
- target audience
- value proposition
- business direction
- roadmap direction
- pricing direction
- branding direction
- growth direction
- ecosystem direction
- market assumptions
- product boundaries
- first-release vs future-release thinking
- rejected ideas
- deferred ideas
- open strategic questions

The Vision Layer is usually created during Genesis.

It is not implementation.

It guides every later phase.

### Vision Layer Output

Common artifacts:

- Master Document
- Master Document Compact
- product vision notes
- strategy pages
- roadmap notes
- pricing notes
- branding notes
- ecosystem notes
- open questions

### Vision Layer Failure Mode

If the Vision Layer is weak, later phases compensate by guessing.

Symptoms:

- modules exist but purpose is unclear
- features are implemented without priority
- user workflows feel arbitrary
- scope keeps expanding
- AI agents invent product decisions
- architecture serves no clear product direction

The fix is not code. The fix is stronger Genesis and clearer Vision.

---

## Infrastructure / Backend Layer

The Infrastructure / Backend Layer is the technical foundation that allows products to run.

It answers:

- where does the system run?
- how is it deployed?
- which runtime is used?
- is Docker enough?
- is Kubernetes needed?
- is serverless appropriate?
- which database is used?
- which queue or event system is used?
- how are APIs exposed?
- how are SDKs structured?
- how are services built and deployed?
- how are secrets managed?
- how are environments separated?
- how is CI/CD handled?
- how are backups handled?
- how are logs and metrics collected?

Examples of Infrastructure / Backend concerns:

- hosting
- runtime
- containers
- orchestration
- deployment
- build system
- service boundaries
- database infrastructure
- queues
- event buses
- API gateway infrastructure
- SDK foundations
- secrets management
- environment configuration
- backup and restore
- scaling
- uptime strategy

The framework is infrastructure-agnostic. It does not require Docker, Kubernetes, serverless, a specific queue, or a specific cloud.

The architect chooses the infrastructure based on project needs.

### Reuse Principle

Infrastructure is an investment.

Once stable, it can support multiple products or Cores.

The goal is not to rebuild deployment, runtime, database, and API foundations for every new product.

---

## System Layer

The System Layer contains reusable platform capabilities.

It is built on top of Infrastructure / Backend and supports one or more Cores.

System capabilities are not the product's unique business idea. They are shared capabilities that many products need.

Examples:

- authentication
- identity and access
- user accounts
- permissions
- search
- indexing
- datastore access patterns
- file storage
- communication
- notifications
- observability
- audit logging
- billing support
- organization / tenant handling
- settings infrastructure
- import/export foundation
- user experience primitives
- privacy and data protection
- security baseline
- admin infrastructure
- integration foundation

The System Layer should be reusable.

A future product should be able to connect to the same System capabilities without rebuilding them.

### Privacy and Data Protection as System Concerns

Privacy and data protection are system-level architecture concerns.

They must be defined before Core implementation begins.

If privacy is not defined at the System Layer, each Core module may invent its own inconsistent handling of:

- personal data
- logging
- retention
- deletion
- export
- access
- consent
- audit
- redaction
- external AI provider exposure
- sensitive operational data

This creates risk and inconsistency.

Privacy and data protection should therefore be treated as baseline system capabilities, not late-stage polish.

### System Layer Failure Mode

If the System Layer is unclear, every Core module re-invents basic platform behavior.

Symptoms:

- inconsistent permission checks
- multiple search patterns
- repeated datastore logic
- duplicated notification logic
- unclear audit behavior
- privacy handled differently in each feature
- AI agents reimplement shared capabilities inside product modules

The fix is to define the System Layer before Core implementation.

---

## Core Layer

The Core Layer contains product-specific business logic.

It is the part that makes the product what it is.

The Core is what users experience as the actual product value.

Examples of Core logic:

- booking workflow
- content publishing workflow
- project planning workflow
- customer support workflow
- AI workspace workflow
- analytics workflow
- automation workflow
- collaboration workflow
- reporting workflow
- import-processing workflow
- marketplace workflow
- learning workflow
- creator workflow
- compliance review workflow

The Core uses Infrastructure and System capabilities.

It should not reimplement them unless the architecture explicitly requires a new System capability.

### Core Is Replaceable

The Core can change from product to product.

A company may reuse the same authentication, search, datastore, notifications, observability, and privacy foundations while replacing the Core product logic.

This is the main scalability benefit:

```text
Build Infrastructure and System once.
Reuse them.
Replace the Core for each product.
```

### Core vs. Yang Core Module

Do not confuse the Core Layer with a Yang Core Module.

| Term | Meaning |
|---|---|
| Core Layer | Product-specific business logic layer |
| Yang Core Module | Technical execution contract for deterministic logic in a module or submodule |

A Core feature may have a Yang Core Module.

A System capability may also have a Yang Core Module.

The word `Core` in `Yang Core Module` refers to Functional Core logic, not necessarily the product Core Layer.

This distinction prevents terminology drift.

---

## Ecosystem Layer Optional

The Ecosystem Layer is optional.

Use it when a project contains multiple independent but connected products, apps, platforms, or service areas under one umbrella.

An ecosystem may share:

- identity
- brand
- infrastructure
- system capabilities
- account model
- billing model
- data model
- documentation standards
- integration standards
- developer tooling
- strategic direction

Not every product needs an Ecosystem Layer.

A single focused product may only need Vision, Infrastructure / Backend, System, and Core.

### Ecosystem Examples

Use neutral examples:

- one company with several connected productivity products
- a platform with multiple standalone tools
- a suite containing an editor, dashboard, automation tool, and analytics product
- a marketplace plus creator tools plus admin platform
- a developer platform plus local utilities plus hosted services

The Ecosystem Layer should not turn every idea into a suite. It exists only when multiple independent products or platforms genuinely belong together.

---

## Utilities Layer Optional

The Utilities Layer contains tools that support the development, specification, or workflow process rather than serving as the main product Core.

Examples:

- prompt compiler
- document block processor
- localization utility
- research/knowledge utility
- UI composition helper
- template library
- reference package manager
- model/platform prompt adapter

Allzy Utilities such as Prism and Splice can support the framework workflow, but the framework method does not depend on proprietary tooling.

A project can apply the method manually with Markdown files and prompts.

Utilities improve convenience, consistency, speed, and repeatability.

### Utilities and Product Architecture

Utilities should not be mixed into the main product Core unless the project explicitly makes them part of the product.

A utility may belong to the same ecosystem and brand while remaining architecturally separate.

This prevents the main product architecture from becoming confused with internal development tooling.

---

# 3. Layer Order and Dependency Direction

The recommended order is:

```text
Vision
→ Infrastructure / Backend
→ System
→ Core
→ Ecosystem / Utilities where applicable
```

This order matters.

## Vision Before Infrastructure

Do not choose infrastructure before the product direction is understood.

A small local utility does not need the same infrastructure as a large SaaS platform.

A multi-tenant product does not need the same infrastructure as a single-user local tool.

Genesis creates the Vision needed to make infrastructure decisions.

## Infrastructure Before System

The System Layer needs a technical base.

Authentication, search, datastore, communication, observability, and privacy architecture depend on runtime and infrastructure assumptions.

For example:

- a local-first app handles data differently than a hosted SaaS
- a Kubernetes deployment has different service assumptions than a single Docker app
- a serverless workflow affects background jobs and queues
- a multi-tenant system affects datastore and auth design

## System Before Core

Core features should not invent basic system behavior.

Before Core implementation, define:

- identity model
- access rules
- search/indexing strategy
- datastore boundaries
- communication patterns
- observability expectations
- privacy/data handling rules
- API/SDK access patterns
- tenant/project/user model where relevant

Then Core features can build on those capabilities instead of re-creating them.

## Core After Foundations

Core is the product idea made executable.

Once Vision, Infrastructure, and System are clear, Core can be decomposed into modules and submodules.

This keeps business logic focused and prevents every product feature from carrying hidden infrastructure decisions.

---

# 4. Module and Submodule Architecture

## Module

A module is a coherent area of responsibility.

A module may belong to:

- Vision
- Infrastructure / Backend
- System
- Core
- Ecosystem
- Utilities

Examples:

| Layer | Example module |
|---|---|
| Vision | Pricing Strategy |
| Infrastructure / Backend | Deployment Runtime |
| System | Identity and Access |
| System | Search and Indexing |
| Core | Content Workflow |
| Core | Analytics Workflow |
| Ecosystem | Shared Account Portal |
| Utilities | Prompt Library |

## Submodule

A submodule is a smaller independent responsibility inside a module.

Examples:

| Module | Example submodule |
|---|---|
| Identity and Access | Resolve permissions |
| Search and Indexing | Update search index |
| Content Workflow | Publish content item |
| Analytics Workflow | Generate daily report |
| Settings | Update notification preference |
| Import Workflow | Validate uploaded file |

A submodule should be:

- small
- clear
- testable
- independently implementable
- bounded
- documented
- linked to relevant contracts
- suitable for one focused AI work session

## Module/Submodule Granularity

The framework does not prescribe exact module size.

The rule is practical:

```text
If one AI work session cannot safely implement or modify it, split it further.
```

Signals that a unit is too large:

- it mixes unrelated workflows
- it requires many unrelated files
- it touches several data domains
- it combines UI, backend, permissions, and migration work without a clear boundary
- it has several root causes
- its acceptance criteria cannot be checked independently
- it would need multiple separate prompts to implement safely

---

# 5. Modular Execution Architecture

The framework favors isolated execution units connected through explicit boundaries.

This can be implemented through:

- service gateways
- API gateways
- event buses
- job queues
- message queues
- workflow engines
- internal SDKs
- module boundaries
- adapter layers
- explicit contracts

Examples of technologies may include queues or buses such as BullMQ, NATS, or other messaging systems. The framework does not require any specific technology.

The principle is:

```text
Modules communicate through explicit boundaries.
They do not depend on hidden shared behavior.
```

## Why This Matters

Explicit modular execution improves:

- fault isolation
- update safety
- deployability
- testability
- observability
- replaceability
- AI implementation scope
- rollback safety
- future scaling

If one module fails, the whole product should not automatically become unrecoverable.

If one module needs an update, the whole system should not need to be rewritten.

If one submodule changes, unrelated submodules should not be touched.

## Functional Core / Imperative Shell Relationship

At the module/submodule level, deterministic logic should follow the Functional Core / Imperative Shell pattern when appropriate.

The Functional Core decides.

The Imperative Shell executes.

This pattern is defined in detail in the Yang contract documents.

Architecture defines where the module sits. Yang defines exactly how the deterministic logic behaves.

---

# 6. Documentation Architecture

The framework uses documents as operational architecture artifacts.

Documents are not only explanations. They are the source material that allows AI systems to produce consistent output.

## Main Document Types

| Document | Role |
|---|---|
| Master Document | Complete product intent from Genesis |
| Master Document Compact | Smaller intent document for compact Genesis workflows |
| Project Tree | Segmented architecture tree |
| Module document | Describes a module area |
| Submodule document | Describes an implementable unit |
| Yin Page | Human intent and product/domain context |
| Yang Core Module | AI-facing technical execution contract |
| Trace Map | Links Yin intent to Yang contract elements |
| Schema | Defines structured data or contract shape |
| Handoff | Scoped execution context for an agent |
| plan.md | Current task focus |
| memory.md | Confirmed project/architecture memory |
| context_retrieval.md | Reusable deterministic retrieval method |
| context_package.md | Temporary selected context for one task/session |
| metadata_index.json / metadata_index.md | Optional generated lookup index for document metadata |
| Search Log | Auditable record of how context was selected |
| Reference Package | Model/platform prompt adaptation material |
| Metadata header | Machine-readable relationship data |

## Documentation as Context Control

The framework does not document for bureaucracy.

It documents to control AI context.

A well-structured document:

- reduces missing assumptions
- narrows the model's decision space
- makes scope boundaries explicit
- provides stable terminology
- makes validation possible
- makes agent switching possible
- turns product intent into implementation context

The documentation is the architecture surface the AI reads.

---


## Retrieval Artifacts in the Architecture

The documentation architecture also includes retrieval artifacts.

These artifacts are not product features. They are context-selection infrastructure for AI-assisted work.

| Artifact | Architectural role |
|---|---|
| `context_retrieval.md` | Defines how agents and scripts should search the documentation graph |
| `metadata_index.json` / `metadata_index.md` | Optional generated index of IDs, paths, tags, layers, document types, and relationships |
| `context_package.md` | Temporary context bundle generated for one task, handoff, review, or agent session |
| Search Log | Records which filters were used, which documents were selected, and which files were excluded |

The distinction is important:

```text
memory.md            = confirmed project state
context_retrieval.md = retrieval method
context_package.md   = selected context for one task
metadata_index       = optional lookup table
Search Log           = retrieval audit trail
```

`memory.md` should not become the place where the whole retrieval procedure is stored.

`context_retrieval.md` should define the method.

`context_package.md` should contain the task-specific selected context.

The Metadata Graph should make context selection repeatable, not force every agent to invent a new search strategy.


# 7. Prompt Library, Reference Packages, and Future Prism Registry

The framework separates task method from model/platform rendering.

A framework prompt defines what must be done.

A model reference defines how to write for a target AI model.

A platform reference defines how to write for a target execution environment.

```text
Framework prompt
+ AI model reference
+ Platform reference
= target-adapted handoff or prompt
```

## Current Manual Workflow

Today, references may be loaded manually from a Prompt Library or Reference Package.

A Reference Package may contain:

- AI model prompting references
- platform execution references
- output format conventions
- handoff rendering examples
- anti-patterns
- model/platform compatibility notes
- task-mode-specific prompt guidance

A reference counts only if its content is present in the current context.

A link or file name is not enough.

## Future Prism Registry

In the future, Prism may resolve model and platform references automatically through a registry.

The registry may choose the right references based on:

- target model
- target platform
- task type
- output type
- execution mode
- desired prompt shape
- available tools

Until that exists, manual reference loading is the operational workflow.

This principle applies beyond Triage. It can apply to Genesis, review, Yin/Yang generation, implementation handoffs, research prompts, and system prompt generation.

---

# 8. Splice in the Architecture Workflow

Splice is a practical block-processing workbench.

It is especially useful when a Master Document or architecture document is split into many blocks.

A typical Splice workflow:

1. Create or gather the Master Document.
2. Segment the document into module/submodule blocks.
3. Load the relevant universal prompt.
4. Load the relevant Yin/Yang template or reference.
5. Process one block at a time.
6. Generate one document per block.
7. Review each generated document.
8. Store accepted outputs in the documentation set.
9. Use accepted documents for implementation or review.

This workflow avoids the Batching Trap.

Instead of asking one model to process an enormous document and produce everything at once, the architect processes small blocks with reusable prompts.

Splice can also support other document workflows. In this architecture, its primary role is safe block processing between Modularization and Specification.

---

# 9. Specification-First Efficiency

The framework shifts effort from late debugging to early thinking.

The architect and AI collaborate to define the product before implementation. The implementation agent should not need to discover the product by reading the entire repository or guessing missing requirements.

This creates efficiency:

- fewer hallucinated requirements
- fewer wrong assumptions
- fewer repeated bugs
- fewer broad code searches
- fewer unscoped prompts
- fewer revision loops
- smaller implementation contexts
- better use of smaller models
- easier review by larger models

## Model Size Strategy

Large models remain valuable for:

- Genesis
- architecture reasoning
- contract review
- conflict detection
- QA Partner mode
- difficult debugging
- system-level validation
- broad analysis
- source-grounded research

Smaller, faster, or cheaper models can often handle:

- tightly scoped implementation
- simple submodule execution
- test generation from a complete contract
- small bugfixes
- repetitive structured work
- code translation from detailed specifications

This is possible because the specification does much of the reasoning work before the implementation agent starts.

The claim is not that small models are always equal to large models.

The claim is that complete context and narrow scope reduce the amount of inference required, making smaller models more useful and safer for execution tasks.

---

# 10. Relationship to Other Framework Documents

## `01_Philosophy.md`

Defines why the framework exists:

- AI invention is a specification gap
- Eager Execution is dangerous
- Docs-First prevents drift
- Atomic prompting reduces context contamination
- high-signal context matters

## `02_Architecture.md`

This document.

Defines how the framework parts fit together:

- pipeline
- layers
- modules
- submodules
- execution flow
- tool relationships

## `03_Yin_Yang_Contracts.md`

Defines the specification model:

- Yin as human intent
- Yang as technical execution contract
- Full / Compact / Direct Prompt boundaries
- Functional Core / Imperative Shell
- Pre-Flight Gap-Check
- Trace Map

## `04_Deterministic_Metadata_Graph.md`

Defines explicit document relationships:

- stable IDs
- metadata headers
- links/backlinks
- trace relationships
- schema references
- deterministic retrieval
- RAG boundary

## `05_Triage_and_Maintenance.md`

Defines maintenance workflow:

- Agent 1 / Agent 2
- visual context compression
- multi-scope splitting
- model/platform-aware handoffs
- bug classification
- contract-gap handling

## `06_State_Management.md`

Defines continuity across sessions:

- `plan.md`
- `memory.md`
- temporary context packages
- compression
- agent switching
- context cleanup

## `07_Metadata_Config_and_Retrieval_Conventions.md`

Defines metadata, config, frontmatter, retrieval, Search Log, context package, and metadata index conventions:

- document metadata fields and schema
- config conventions for prompts and workspace context
- deterministic retrieval rules
- Search Log and context package structure

## `08_Glossary_and_Terminology.md`

Defines terminology and glossary for the framework:

- canonical definitions for all framework terms
- artifact names (Full, Compact, Direct, Yin Page, Yang Core Module, etc.)
- naming rules and usage guidance

## `09_Origin_and_Principles.md`

Defines background and principles:

- origin
- motivation
- privacy/security baseline
- AI collaboration philosophy
- scope notes

It is background context, not the primary technical contract.

---

# 11. Relationship to Deterministic Metadata Graph

The architecture produces many documents.

Without explicit relationships, a future AI agent must guess which documents belong together.

The Deterministic Metadata Graph solves this by encoding relationships directly through metadata.

Examples:

- this module belongs to this product
- this submodule belongs to this module
- this Yin page pairs with this Yang contract
- this Yang contract references these schemas
- this trace map links these rules
- this ADR affects this module
- this handoff targets this contract

The architecture defines the document types and lifecycle.

The metadata graph defines how those documents are linked and retrieved.

Together, they prevent context selection from becoming a semantic guessing problem.


Recommended artifact split:

```text
metadata/frontmatter = identity and relationships inside documents
metadata_index       = optional generated lookup index
context_retrieval.md = reusable deterministic search method
context_package.md   = temporary selected context for a task
Search Log           = record of how context was selected
memory.md            = confirmed project/architecture state
```

This prevents the architecture from depending on broad semantic retrieval or unbounded memory injection.

A future agent should be able to:

1. read `context_retrieval.md`
2. search metadata or `metadata_index`
3. follow explicit graph relationships
4. generate a compact `context_package.md`
5. include a Search Log
6. perform the task with selected context only


---

# 12. Relationship to Triage and Maintenance

Architecture is not only for first implementation.

It also controls maintenance.

When a bug appears, the framework asks:

```text
Is the implementation wrong,
or is the architecture/specification missing something?
```

Triage uses the architecture to decide:

- which layer is affected
- which module or submodule is involved
- whether the bug is a contract flaw
- whether the bug is a state issue
- whether the task should be split
- which handoff Agent 2 should receive

If the architecture is clear, maintenance is targeted.

If the architecture is unclear, maintenance becomes broad exploration.

---

# 13. Relationship to State Management

State Management preserves continuity across AI sessions.

Architecture defines the system of documents and layers.

State Management defines how active work continues between agents and sessions.

Use:

```text
plan.md   = current task focus
memory.md = confirmed project/architecture memory
handoff   = scoped execution context
```

Architecture and State Management work together:

- Architecture defines where work belongs.
- `plan.md` defines what is being worked on now.
- `memory.md` records confirmed changes.
- Handoffs move relevant context to the next agent.

This prevents each AI session from starting cold.


The architecture should keep state and retrieval separate:

```text
plan.md              = what is being worked on now
memory.md            = what is confirmed about the project
context_retrieval.md = how relevant context is found
context_package.md   = what context was selected for this task
```

This separation prevents two common failures:

- `memory.md` becomes a procedural search manual instead of confirmed state.
- each agent invents a different retrieval process and selects different context.

For large projects, `context_retrieval.md` becomes part of the architecture because it defines how AI agents navigate the documentation graph before implementation or review.


---

# 14. Security, Privacy, and Data Protection

Security, privacy, and data protection must be included at architecture time.

They are not late implementation details.

Architecture should define:

- what sensitive data exists
- where personal data is stored
- how data is retained or deleted
- how export/backup works
- how access is controlled
- what is logged
- what must be redacted
- what external AI systems may receive
- which secrets must never enter documents or prompts
- which environment variables are required
- which compliance concerns apply

The framework does not replace legal review.

It does ensure privacy and security are not forgotten during AI-assisted implementation.

## No Secrets in Documents

No framework document, prompt, template, or handoff should contain real secrets.

Use placeholders:

```text
$ENV_API_KEY
$ENV_DATABASE_URL
$ENV_SESSION_SECRET
process.env.SERVICE_TOKEN
```

Real values belong in environment files or secret managers, not in AI-visible documents.

---

# 15. Architecture Anti-Patterns


## Retrieval/State Confusion

The project stores confirmed project memory, search method, temporary context packages, and old search logs in one file.

Result:

- `memory.md` becomes too large
- retrieval rules are distorted by compression
- agents select context inconsistently
- old task context is reused as if current
- confirmed truth and search procedure are mixed

Fix:

- keep `memory.md` for confirmed state
- keep `context_retrieval.md` for retrieval method
- use `context_package.md` as temporary selected context
- include Search Logs only where they explain a specific retrieval result


## Code-First Architecture

The AI starts coding before the product is decomposed.

Result:

- hidden assumptions
- brittle architecture
- repeated rework
- unclear ownership
- inconsistent modules

Fix:

- complete Genesis, Segmentation, Modularization, and Specification before execution.

## Premature Yin/Yang

Contracts are created before the module tree is stable.

Result:

- contracts cover the wrong scope
- modules later split or merge
- specifications must be rewritten
- implementation agents receive oversized contracts

Fix:

- create Yin/Yang documents only in Phase 4 after modularization.

## System/Core Confusion

Product-specific Core logic reimplements reusable System capabilities.

Result:

- duplicated authentication
- inconsistent permissions
- inconsistent privacy handling
- repeated datastore patterns
- more bugs

Fix:

- define Infrastructure and System before Core.

## Utility/Product Confusion

Internal workflow tools are mixed into the product Core.

Result:

- product architecture becomes polluted
- developer tooling and customer-facing logic blur
- future maintenance becomes confusing

Fix:

- keep Utilities separate unless intentionally productized.

## Ecosystem Inflation

Every product idea becomes an ecosystem too early.

Result:

- unnecessary complexity
- vague product boundaries
- roadmap bloat
- implementation delay

Fix:

- use Ecosystem Layer only when multiple independent products or platforms genuinely exist.

## Over-Broad Submodule

A submodule contains too much work.

Result:

- one AI session cannot implement it safely
- prompts become huge
- tests are unclear
- changes touch unrelated areas

Fix:

- split into smaller submodules.

## Tool-First Architecture

The project chooses tools before understanding the product.

Result:

- overbuilt infrastructure
- wrong deployment model
- unnecessary complexity
- tool lock-in

Fix:

- Vision first, then infrastructure choices.

## Hidden Privacy Layer

Privacy is handled inside individual features instead of system-wide.

Result:

- inconsistent handling
- accidental logging
- missing deletion/export behavior
- compliance gaps

Fix:

- define Privacy and Data Protection as System concerns.


## Workspace Context Anti-Patterns

Additional architecture anti-patterns:

- treating workspace context initialization as application implementation
- treating workspace state maintenance as Triage
- treating `skills/` as Memory 2.0
- storing search method inside skills instead of `context_retrieval.md`
- treating `skills_bundle.md` as source of truth
- rewriting `AGENTS.md` or `agenten.md` as part of default state maintenance
- treating a repository link as attached template content
- treating Document Metadata Enrichment as Yin/Yang conversion
- treating Context Retrieval Builder as only Agent-2 packaging

---

# 16. Architecture Quality Checklist

Before moving from Genesis to Segmentation:

- [ ] Product purpose is clear.
- [ ] Target audience is clear.
- [ ] First-release scope is separated from future ideas.
- [ ] Out-of-scope boundaries are explicit.
- [ ] Security/privacy concerns are visible.
- [ ] Open questions are listed.
- [ ] Confirmed decisions are separated from assumptions.
- [ ] Master Document is complete enough for Phase 2.

Before moving from Segmentation to Modularization:

- [ ] Major product areas are identified.
- [ ] Vision, Infrastructure, System, Core, Ecosystem, and Utilities concerns are separated where applicable.
- [ ] Privacy/Data Protection concerns are visible.
- [ ] Obvious boundaries are identified.
- [ ] Potential dependencies are noted.
- [ ] No final module contracts have been created prematurely.

Before moving from Modularization to Specification:

- [ ] Modules are coherent.
- [ ] Submodules are small enough for focused AI work.
- [ ] Shared System capabilities are separated from product Core logic.
- [ ] Optional Ecosystem and Utilities areas are not mixed into Core.
- [ ] Implementation units are clear.
- [ ] Scope boundaries are explicit.

Before moving from Specification to Execution:

- [ ] Required Yin/Yang documents are complete.
- [ ] Compact/direct prompt path is justified where used.
- [ ] Yang contracts pass Pre-Flight Gap-Check.
- [ ] Open questions are marked.
- [ ] Acceptance criteria are testable.
- [ ] Relevant state excerpts are prepared.
- [ ] Relevant metadata IDs or graph references are available where applicable.
- [ ] `context_retrieval.md` is used where the project provides it.
- [ ] A `context_package.md` or equivalent selected context is prepared for complex tasks.
- [ ] Search Log is included when deterministic retrieval was used.
- [ ] Agent handoff is scoped.
- [ ] Model/platform reference status is clear.
- [ ] No secrets are included.

---

---

# 17. Workspace Context Architecture

Workspace Context Architecture describes how a target implementation workspace is prepared for AI-assisted work.

It is not a new framework pipeline phase.

It supports the existing pipeline, especially the transition into Execution and Maintenance.

The core idea:

```text
Do not start implementation from an empty or noisy workspace.
Prepare the workspace context layer first.
```

## Target Implementation Workspace

Workspace context artifacts belong to the target implementation workspace.

They are not the same thing as the Framework GitHub repository prompt organization.

A target workspace may be:

- a repository
- a local project folder
- a coding-agent workspace
- an IDE workspace
- a CLI agent workspace
- a documentation workspace
- a Yin/Yang specification workspace
- a multi-agent implementation workspace

The framework repo stores framework docs, templates, prompts, examples, and references.

The target implementation workspace stores project-specific state, context, and retrieval artifacts.

Do not mix these layers.

## Core Workspace Context Artifacts

The workspace context layer may include:

```text
plan.md              = current task focus
memory.md            = confirmed project / architecture memory
context_retrieval.md = reusable deterministic retrieval method
context_package.md   = temporary selected context for one task
Search Log           = audit trail for how context was selected
metadata_index       = optional generated lookup index
skills/              = optional reusable helper rules for AI agents
handoff              = scoped execution context for one agent or task
```

These artifacts are project / AI-session state.

They are not application runtime state.

Application runtime state is specified in architecture documents, Yin/Yang contracts, and implementation.

## Workspace Context Initialization

Workspace Context Initialization is the setup, inspection, or repair step for the workspace context layer.

Operational prompt:

```text
workspace_context_initialization_prompt.md
```

It may create or check:

```text
plan.md
memory.md
context_retrieval.md
context_package_template.md
search_log_template.md
metadata_index.md / metadata_index.json
skills/
```

It does not:

- write application code
- implement features
- fix bugs
- perform Triage
- create Yin/Yang documents
- rewrite architecture
- refactor a repository
- replace application runtime state architecture

### Setup Profiles

The initialization workflow supports:

| Profile | Purpose |
|---|---|
| `inspect_only` | inspect existing context setup only |
| `minimal` | create/check `plan.md` and `memory.md` |
| `standard` | minimal + `context_retrieval.md` |
| `full` | standard + context package template, Search Log template, optional metadata index, optional skills |
| `custom` | explicit config choices |

Use `standard` as the normal baseline.

Use `full` for larger projects, Yin/Yang-heavy projects, Triage-heavy projects, or multi-agent workflows.

## Workspace State Maintenance

Workspace State Maintenance keeps living workspace state useful and compressed.

Operational prompt:

```text
workspace_state_maintenance_prompt.md
```

It maintains:

```text
plan.md
memory.md
skills/
skills_index.md
skills_bundle.md
```

It may health-check optional artifacts when explicitly requested, but it does not rewrite them by default:

```text
context_retrieval.md
metadata_index.md
metadata_index.json
context packages
search logs
```

It does not initialize the workspace.

It does not implement code.

It does not perform Triage.

It does not rewrite framework templates or prompts.

It does not maintain `AGENTS.md` or `agenten.md` unless explicitly requested.

## Optional Workspace Skills

The workspace may include:

```text
context/skills/
```

Skills are reusable objective helper rules for AI agents.

They are not Memory 2.0.

They are not search methods.

They are not temporary context packages.

Skills may store:

- local procedures
- recurring fix patterns
- verification checklists
- mistake-prevention rules
- stable workflow lessons

Skills must not store:

- project status
- raw chat history
- plan items
- full memory
- search method
- context packages
- secrets
- speculative notes

Recommended structure:

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

Each individual `SKILL.md` is the source of truth.

`skills_bundle.md` is generated and must not become the source of truth.

## Context Retrieval Builder

The Context Retrieval Builder searches existing metadata-tagged documents and builds a selected output artifact.

Operational prompt:

```text
context_retrieval_builder_prompt.md
```

It may produce:

```text
summary
deep_brief
agent_context_package
patch_handoff_context
document_source_pack
review_context
custom
```

It does not implement code, fix bugs, rewrite documents, or create Yin/Yang documents.

It supports architecture by giving future agents selected, auditable, task-specific context instead of raw repository dumps.

## Document Metadata Enrichment

Document Metadata Enrichment makes existing documents retrieval-ready by adding or updating standardized metadata/frontmatter.

Operational prompt:

```text
document_metadata_enrichment_prompt.md
```

It does not convert documents into Yin/Yang.

It does not rewrite document meaning.

It does not perform Genesis, Triage, implementation, or bugfixing.

It supports architecture by allowing older or arbitrary documents to join the deterministic metadata graph.

## Yin/Yang Prompt Generator

The Yin/Yang Prompt Generator creates a specialized Agent-2 prompt for producing a Yin/Yang specification document.

Operational prompt:

```text
yin_yang_prompt_generator.md
```

It does not directly create the final Yin/Yang document.

It creates the prompt for the specification agent.

Agent 2 must have the required template content attached, pasted, or directly readable.

A repository link is only a pointer and does not count as attached template content.

## Workspace Context Architecture in the Pipeline

Workspace context may appear at several points:

| Pipeline area | Workspace/context role |
|---|---|
| After Genesis | prepare the target workspace before segmentation/specification/implementation work |
| During Specification | store generated Yin/Yang docs with metadata and retrieval rules |
| Before Execution | build task-specific context packages and handoffs |
| During Maintenance | retrieve context, preserve state, and avoid repeated ineffective fixes |
| Across agent switches | let work continue across models/platforms without relying on chat memory |

Workspace Context Architecture is a support layer.

It does not replace Genesis, Segmentation, Modularization, Specification, or Execution.


---

---

# 18. Operational Prompt Family in Architecture

Operational prompts are not separate framework phases.

They are execution helpers for specific framework jobs.

Current prompt families:

| Family | Prompts | Architectural role |
|---|---|---|
| Genesis | Genesis Full, Genesis Compact | Phase 1 clarification into Master Document / Master Document Compact |
| Triage | Fast, Standard, Deep | Maintenance diagnosis and Agent-2 handoff generation |
| Workspace / Context | Workspace Context Initialization, Workspace State Maintenance | Prepare and maintain target workspace context |
| Retrieval / Metadata | Context Retrieval Builder, Document Metadata Enrichment | Make context findable and package selected context |
| Specification | Yin/Yang Prompt Generator | Generate Agent-2 prompts for Yin/Yang specification |

Future focused single-artifact prompts may be derived from the Workspace Context Initialization workflow, for example:

```text
plan_md_prompt.md
memory_md_prompt.md
context_retrieval_prompt.md
context_package_generation_prompt.md
metadata_index_generation_prompt.md
skills_maintenance_prompt.md
```

These are optional convenience prompts.

They should not be treated as required source files until they exist.



---

## Website-Ready Summary

The Allzy Framework architecture describes how a product moves from raw idea to implemented software through structured AI-assisted work.

Genesis turns a raw idea into a complete Vision foundation. Segmentation breaks that vision into topic blocks. Modularization turns those blocks into modules and submodules. Specification creates Yin/Yang contracts for the implementable units. Execution uses those contracts to generate code through focused, model/platform-aware handoffs.

The layer model separates reusable foundations from product-specific logic:

```text
Vision defines direction.
Infrastructure / Backend provides the technical base.
System provides reusable platform capabilities.
Core contains replaceable product logic.
Ecosystem and Utilities are optional extensions.
```

The most important architectural rule is:

```text
Infrastructure and System are reusable.
Core is replaceable.
```

The framework front-loads thinking, decomposition, and specification so implementation agents do not need to infer the product from vague prompts. Deterministic metadata, `context_retrieval.md`, optional metadata indexes, task-specific context packages, and Search Logs make the right context findable without broad semantic guessing.

This reduces hallucination risk, token waste, rework, and architecture drift.

The goal is not to make documentation heavier. The goal is to make coding smaller, safer, faster, and more predictable.


---