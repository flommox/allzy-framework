---
id: "allzy.framework.master-specification.v5"
title: "Allzy Framework Master Specification V5"
artifact_type: "Master Specification"
status: "Stable"
version: "5.0.2"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - specification
  - ai-assisted-development
---

# Allzy Framework Master Specification V5

## Status

This is the consolidated V5 master specification for the Allzy Framework.

It summarizes and coordinates the complete framework method across the current documentation set:

- `01_Philosophy.md`
- `02_Architecture.md`
- `03_Yin_Yang_Contracts.md`
- `04_Deterministic_Metadata_Graph.md`
- `05_Triage_and_Maintenance.md`
- `06_State_Management.md`
- `09_Origin_and_Principles.md`
- `07_Metadata_Config_and_Retrieval_Conventions.md`
- `08_Glossary_and_Terminology.md`

This file is intended to be usable as a standalone working overview of the framework.

The detailed topic documents remain the specialized source files for their respective domains, but this specification contains the unified operating model, terminology, artifact map, process model, and quality rules.

---

# 1. Purpose

The Allzy Framework is a specification-first method for AI-assisted software development.

It exists to reduce AI guessing.

The framework turns raw ideas, natural-language discussion, screenshots, bug reports, project memory, and documentation blocks into structured artifacts that AI agents can use safely.

The core idea:

```text
The AI should execute from defined context, not infer the product from vague prompts.
```

The framework achieves this through:

- collaborative Genesis
- architecture decomposition
- module/submodule segmentation
- Yin/Yang contracts
- deterministic metadata retrieval
- scoped triage handoffs
- explicit project/session state
- model/platform-aware prompting
- privacy/security boundaries
- verification and documentation update loops

The result is not more documentation for its own sake.

The result is controlled context for AI execution.

---

# 2. Scope of This Specification

This V5 specification defines:

- the framework philosophy
- the five-phase pipeline
- the framework layer model
- the document and artifact model
- the Yin/Yang contract system
- the deterministic metadata graph
- the triage and maintenance workflow
- the state-management workflow
- the workspace context architecture
- metadata/config/frontmatter conventions
- context retrieval builder workflow
- document metadata enrichment workflow
- workspace state maintenance workflow
- the model/platform reference model
- the role of prompts, templates, examples, and utilities
- quality gates
- anti-patterns
- operational workflows

This file does not fully duplicate the operational prompts or templates.

Prompts and templates are executable artifacts stored separately. This specification defines where they belong, what role they play, and which rules they must follow.

---

# 3. Source-of-Truth Hierarchy

The Allzy Framework uses a layered source-of-truth model.

## 3.1 Primary Framework Documentation

The current explanatory framework source is:

```text
docs/
├── 01_Philosophy.md
├── 02_Architecture.md
├── 03_Yin_Yang_Contracts.md
├── 04_Deterministic_Metadata_Graph.md
├── 05_Triage_and_Maintenance.md
├── 06_State_Management.md
├── 07_Metadata_Config_and_Retrieval_Conventions.md
├── 08_Glossary_and_Terminology.md
└── 09_Origin_and_Principles.md
```

Roles:

| Document | Role |
|---|---|
| `01_Philosophy.md` | Neutral framework principles |
| `02_Architecture.md` | Method architecture, pipeline, layers, artifact relationships |
| `03_Yin_Yang_Contracts.md` | Human-intent and technical-contract model |
| `04_Deterministic_Metadata_Graph.md` | Metadata, IDs, retrieval, graph relationships |
| `05_Triage_and_Maintenance.md` | Bugfix and maintenance handoff workflow |
| `06_State_Management.md` | `plan.md`, `memory.md`, retrieval state, context continuity |
| `07_Metadata_Config_and_Retrieval_Conventions.md` | Metadata, config, frontmatter, retrieval, Search Log, context package conventions |
| `08_Glossary_and_Terminology.md` | Canonical terminology, artifact names, naming rules |
| `09_Origin_and_Principles.md` | Background, motivation, origin, stable principles |

## 3.2 Operational Artifacts

Operational artifacts live outside `docs/`.

They include:

```text
prompts/
├── Genesis/
├── Triage/
├── Workspace/
├── Retrieval/
├── Specification/
└── Review/

templates/
├── yin/
├── yang/
├── yin-yang/
├── context/
└── state/

examples/
└── user-login/
```

Roles:

| Artifact area | Role |
|---|---|
| `prompts/` | Operational prompt families (Genesis, Triage, Workspace, Retrieval, Specification, Review); `000_universal.md` is the canonical prompt in each prompt-type folder |
| `templates/` | Reusable artifact structures (Yin, Yang, Yin/Yang, context, state); the numbered template file in each leaf folder is canonical |
| `examples/` | Filled reference examples, not templates |

Prompts and templates execute the method.

Docs explain the method.

Examples demonstrate the method.

`Referenzen/`, where present, holds optional, supporting, internal reference material and is not part of the primary active publication surface.


## 3.3 Conflict Rule

If an old draft, old prompt, old template, or old master specification conflicts with current finalized docs and templates, the current finalized source wins.

Current terminology and structure must not preserve outdated names simply because they existed in drafts.



## 3.4 Current Operational Prompt Set

The current operational prompt set is:

### Genesis

```text
Genesis Full
Genesis Compact
```

Genesis creates:

```text
Master Document
Master Document Compact
```

Genesis does not create architecture, modules, Yin/Yang documents, implementation plans, or code.

### Triage

```text
prompts/Triage/fast/000_universal.md
prompts/Triage/standard/000_universal.md
prompts/Triage/deep/000_universal.md
```

Triage separates Agent 1 diagnosis from Agent 2 execution.

Fast / Standard / Deep change diagnostic depth and output length, not the Agent 1 / Agent 2 separation.

### Workspace / Context

```text
workspace_context_initialization_prompt.md
workspace_state_maintenance_prompt.md
context_retrieval_builder_prompt.md
document_metadata_enrichment_prompt.md
```

These prompts prepare, maintain, retrieve, or enrich workspace context.

They do not implement application code.

### Specification

```text
yin_yang_prompt_generator.md
```

The Yin/Yang Prompt Generator creates a specialized Agent-2 prompt.

It does not directly create the final Yin/Yang document.

### Optional Future Single-Artifact Prompts

The Workspace Context Initialization workflow may later be split into focused single-artifact prompts:

```text
plan_md_prompt.md
memory_md_prompt.md
context_retrieval_builder_prompt.md
context_package_generation_prompt.md
metadata_index_generation_prompt.md
skills_maintenance_prompt.md
```

These are optional convenience prompts and should not be treated as required source files until they exist.

---

# 4. Current Terminology

The current framework uses:

```text
Full
Compact
Direct
```

There is no public legacy terminology to support in this baseline.

## 4.1 Full

Use Full for:

- large products
- platforms
- systems
- SaaS ideas
- major features
- high-risk workflows
- backend/system modules
- permissions
- privacy/security logic
- persistence
- APIs
- audit
- deterministic business logic
- long-lived modules

Full means complete framework structure.

## 4.2 Compact

Use Compact for:

- smaller tools
- scripts
- utilities
- low-risk tasks
- narrow features
- smaller but non-trivial workflows
- intent/execution work that still needs boundaries

Compact means reduced overhead, not reduced safety.

Compact must still preserve:

- intent
- scope
- out-of-scope boundaries
- privacy/security checks
- acceptance criteria
- open questions
- implementation constraints

## 4.3 Direct

Use Direct for trivial isolated fixes.

Examples:

- small copy fix
- label change
- spacing fix
- isolated CSS adjustment
- small visual tweak with no state or contract impact

Direct must not be used when the task touches:

- architecture
- state transitions
- persistence
- APIs
- permissions
- privacy/security
- business logic
- cross-module behavior
- model/platform-specific handoff needs
- unresolved open questions

---

# 5. Core Philosophy

The framework is built on these principles.

## 5.1 AI Should Execute, Not Guess

AI implementation becomes unreliable when the model must invent missing context.

Missing context becomes invented behavior.

The framework reduces invention by making intent, contracts, scope, metadata, and state explicit.

## 5.2 Human Intent Comes First

The human owns:

- product intent
- business logic
- judgment
- accepted risk
- priorities
- tradeoffs
- final approval

The AI may assist with:

- questioning
- structuring
- summarizing
- generating
- reviewing
- implementing

The AI may propose. The human decides.

## 5.3 Documentation Is Context Control

Documentation is not paperwork.

Documentation tells the AI:

- what is true
- what is current
- what is out of scope
- what belongs together
- what should be retrieved
- what should not be changed
- how output will be verified

## 5.4 High Context Volume Is Not High-Quality Context

More context is not automatically better.

Useful context is:

- relevant
- current
- scoped
- structured
- verified
- traceable
- compressed

Unfiltered context produces noise and drift.

## 5.5 Small Scopes Reduce AI Failure

Use one narrow scope whenever possible:

```text
one bug
one topic
one module
one submodule
one root cause
one handoff
```

Same-area bundles are allowed only when context is shared.

Unrelated topics should be split.

## 5.6 Contract Flaws and Code Flaws Are Different

A bug may require:

- a code fix
- a contract update
- a Yin clarification
- a Yang correction
- a state update
- a new handoff

Do not patch contract gaps as hidden code behavior.

## 5.7 Privacy and Security Are Architecture Conditions

Privacy and security are not late-stage polish.

They must be defined before implementation.

Real secrets must not enter prompts, documents, logs, screenshots, context windows, or handoffs.

Use placeholders and environment variables.

---

# 6. The Five-Phase Pipeline

The Allzy Framework pipeline:

```text
1. Genesis
2. Segmentation
3. Modularization
4. Specification
5. Execution
```

Each phase has one job.

Later phases must not be performed prematurely.

---

## 6.1 Phase 1 — Genesis

Genesis is the collaborative human/AI ideation and requirements phase.

The human provides:

- ideas
- goals
- product intuition
- constraints
- workflows
- examples
- rejected directions
- open concerns

The AI helps:

- ask questions
- refine the idea
- challenge assumptions
- identify risks
- suggest missing areas
- separate decisions from assumptions
- preserve rejected and deferred ideas
- produce the final Master Document

Genesis output:

```text
Master Document
```

or for smaller scope:

```text
Master Document Compact
```

Genesis creates the Vision foundation.

Genesis must not create:

- final architecture
- final modules
- final submodules
- Yin/Yang contracts
- API contracts
- database schemas
- implementation plans
- code

Genesis clarifies the idea. It does not implement it.

---

## 6.2 Phase 2 — Segmentation

Segmentation turns the Master Document into structured topic blocks.

It identifies:

- domains
- product areas
- workflows
- system concerns
- infrastructure concerns
- Core feature areas
- optional ecosystem areas
- optional utility areas
- privacy/security concerns
- dependencies
- boundaries

Outputs:

```text
Project Tree
Topic Blocks
Category Blocks
Potential Module Areas
Potential Boundary Notes
```

Segmentation prevents the AI from deciding the structure during implementation.

---

## 6.3 Phase 3 — Modularization

Modularization turns segmented areas into modules and submodules.

A module is a coherent area of responsibility.

A submodule is a smaller implementable unit inside a module.

Rule:

```text
If one AI work session cannot safely implement or modify it, split it further.
```

A submodule should be:

- small
- clear
- testable
- bounded
- independently implementable
- documentable
- suitable for one focused AI session

---

## 6.4 Phase 4 — Specification

Specification turns modules/submodules into documents that implementation agents can use.

This is where Yin/Yang documents are created.

Yin/Yang documents must not be created before module/submodule boundaries are stable.

Specification output may include:

- Yin Page
- Compact Yin Page
- Yang Core Module
- Yin/Yang Document
- Yin/Yang Compact
- Trace Map
- Schemas
- Handoff Notes
- Acceptance Criteria
- Open Questions

---

## 6.5 Phase 5 — Execution

Execution turns specifications into implementation.

Execution should begin from:

- completed contracts or scoped prompts
- relevant state
- metadata-selected context
- model/platform reference status
- acceptance criteria
- narrow handoff

Execution output should include:

- changed files
- summary
- verification
- tests/checks
- blockers
- documentation updates needed

Execution is not complete until verification closes the loop.

---

# 7. Framework Layer Model

The framework layer model:

```text
Vision Layer
Infrastructure / Backend Layer
System Layer
Core Layer
Ecosystem Layer (optional)
Utilities Layer (optional)
```

Core principle:

```text
Infrastructure and System are reusable.
Core is replaceable.
```

---

## 7.1 Vision Layer

The Vision Layer contains:

- product concept
- purpose
- target audience
- value proposition
- strategic direction
- roadmap direction
- branding direction
- pricing direction
- ecosystem direction
- rejected ideas
- deferred ideas
- open strategic questions

It is primarily created during Genesis.

It guides later architecture.

---

## 7.2 Infrastructure / Backend Layer

Infrastructure / Backend answers:

- where does it run?
- how is it deployed?
- Docker, Kubernetes, serverless, local, or another model?
- which runtime?
- which database?
- which queue/event system?
- which APIs?
- which SDK foundations?
- how are secrets managed?
- how are environments separated?
- how are backups handled?
- how is CI/CD handled?

This layer is technical foundation.

It should be reusable where possible.

---

## 7.3 System Layer

System contains reusable platform capabilities.

Examples:

- authentication
- identity/access
- user accounts
- permissions
- search/indexing
- datastore access
- communication
- notifications
- observability
- audit logging
- settings infrastructure
- import/export foundation
- privacy/data protection
- security baseline
- integration foundation

System should be defined before Core.

Core modules should not reinvent System capabilities.

---

## 7.4 Core Layer

Core contains product-specific business logic.

Examples:

- booking workflow
- content publishing workflow
- analytics workflow
- automation workflow
- collaboration workflow
- reporting workflow
- customer support workflow
- AI workspace workflow

Core is what changes per product.

The same Infrastructure/System foundation can support different Cores.

---

## 7.5 Ecosystem Layer Optional

Use Ecosystem when multiple independent but connected products/apps/platforms belong under one umbrella.

It may share:

- identity
- infrastructure
- system capabilities
- account model
- billing model
- documentation standards
- strategic direction

Not every project needs Ecosystem.

---

## 7.6 Utilities Layer Optional

Utilities are tools that support the workflow or ecosystem rather than serving as the main product Core.

Examples:

- prompt compiler
- document block processor
- localization utility
- research/knowledge utility
- UI composition helper
- reference package manager

Utilities may be part of the ecosystem while remaining architecturally separate from the main product Core.

---

# 8. Module and Submodule Model

A module is a coherent area of responsibility.

A submodule is a smaller independent unit inside a module.

Example:

```text
Module: Content Workflow
Submodules:
- publish item
- schedule item
- review item
- archive item
```

Submodules are the preferred implementation unit.

They allow:

- smaller prompts
- smaller contracts
- focused implementation
- focused tests
- less hallucination
- better use of smaller models
- easier review

---

# 9. Modular Execution Architecture

The framework favors explicit boundaries between modules/submodules.

Possible boundary mechanisms:

- API gateways
- service gateways
- event buses
- queues
- job systems
- internal SDKs
- adapter layers
- module contracts
- workflow engines

No specific technology is mandatory.

The principle:

```text
Modules communicate through explicit boundaries.
They do not depend on hidden shared behavior.
```

Benefits:

- failure isolation
- update safety
- testability
- rollback safety
- observability
- replaceability
- smaller AI context
- safer implementation

---

# 10. Yin/Yang Contract System

Yin/Yang separates human intent from technical execution.

```text
Yin  = human intent, product meaning, domain context, workflows, scope boundaries
Yang = technical execution contract, schemas, decisions, actions, invariants, tests
```

Yin preserves meaning.

Yang constrains execution.

---


## Yin/Yang Prompt Generator

Operational prompt:

```text
yin_yang_prompt_generator.md
```

The Yin/Yang Prompt Generator creates a specialized Agent-2 prompt.

It does not directly create the final Yin/Yang document.

```text
Agent 1 = Yin/Yang Prompt Generator
Agent 2 = Yin/Yang Specification Agent
```

Agent 2 must use the required template content.

A repository link is only a pointer and does not count as attached template content.

The template counts as available only if attached, pasted, or directly readable by the execution environment.

The generator also supports Existing Document Conversion Mode.

In that mode, the existing document is source context, not a template.

Missing product decisions become Open Questions.

Missing technical execution details become Contract Gaps.

There is no standalone Yang Compact.

The combination below is invalid:

```text
generation_target: yang
scope_size: compact
```


## 10.1 Yin Page

A Yin Page is human-facing.

It may be written in a configured human language.

Technical identifiers remain English.

Yin includes:

- short description
- target audience
- concept/objective
- problem/motivation
- core value
- domain/business rules
- workflows
- UI/interaction notes
- data concepts
- roles/permissions/security context
- integrations/dependencies
- out-of-scope boundaries
- open questions
- quality checklist

Yin must not become a technical execution contract.

---

## 10.2 Compact Yin

Compact Yin is for smaller work that still needs intent context.

It includes:

- purpose
- target audience
- core value
- expected behavior
- domain rules
- UI/interaction notes
- data concepts
- dependencies
- out-of-scope
- Yang handoff notes
- open questions
- quality checklist

It is not Yang.

It is not an implementation contract.

---

## 10.3 Yang Core Module

A Yang Core Module is the AI-facing technical execution contract.

Yang is always English.

Yang defines:

- Functional Core / Imperative Shell boundary
- configuration schema
- state snapshot schema
- input event/command schema
- functional result schema
- decision pipeline
- decision matrix
- action registry
- action sets
- parameter schemas
- invariants
- idempotency
- errors and edge cases
- observability/audit
- tests
- trace map
- open contract gaps
- implementation handoff notes

Yang must be precise enough that an implementation agent does not invent missing execution behavior.

---

## 10.4 Functional Core / Imperative Shell

Yang uses the Functional Core / Imperative Shell model.

The Functional Core:

- receives injected state
- receives input command/event
- reads configuration
- makes deterministic decisions
- returns result/action objects
- does not perform side effects

The Imperative Shell:

- reads databases
- writes databases
- calls APIs
- sends messages
- executes actions
- injects time/randomness/environment values
- handles side effects

Rule:

```text
The Core decides. The Shell executes.
```

The Core must not:

- call external APIs
- access databases
- read environment variables directly
- call current time directly
- mutate global state
- send messages
- perform side effects

---

## 10.5 Yin/Yang Document Types

Current document types:

| Type | Purpose |
|---|---|
| Yin Page | Human intent and domain context |
| Compact Yin Page | Smaller human intent page |
| Yang Core Module | Full technical execution contract |
| Yin/Yang Document | Full Yin + full Yang in one file |
| Yin/Yang Compact | Small intent + execution-rules document |
| Direct Scoped Prompt | Tiny isolated work without document contract |

There is no separate Compact Yang.

If Yang is needed, it must be complete enough to prevent execution ambiguity.

---

## 10.6 Full / Compact / Direct Decision

Use Full Yin/Yang when:

- business logic is non-trivial
- state transitions matter
- API behavior matters
- persistence matters
- permissions matter
- privacy/security matter
- audit/logging matters
- multiple edge cases exist
- the module is long-lived
- implementation agents need a contract

Use Yin/Yang Compact when:

- task is small
- execution rules matter
- full Yang would be too heavy
- scope is bounded
- risk is low/moderate

Use Direct Prompt when:

- change is trivial
- no architecture or contract is affected
- no state behavior changes
- no privacy/security logic changes
- no persistence/API behavior changes
- no model/platform-specific rendering is required

---

## 10.7 Core Layer vs. Yang Core Module

Do not confuse these terms.

| Term | Meaning |
|---|---|
| Core Layer | Product-specific business logic layer |
| Yang Core Module | Technical Functional Core contract |

A System module can have a Yang Core Module.

A Core module can have a Yang Core Module.

Infrastructure can have a Yang contract when execution rules must be precise.

The word `Core` in Yang refers to Functional Core, not necessarily the product Core Layer.

---

## 10.8 Metadata for Yin/Yang

Yin/Yang documents should participate in the Metadata Graph.

Recommended metadata:

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
tags:
  - settings
  - input
  - deterministic-core
---
```

Metadata supports deterministic retrieval, source tracing, and handoff generation.

---

# 11. Deterministic Metadata Graph

The Deterministic Metadata Graph makes documents findable by explicit structure instead of semantic guessing.

It uses:

- stable IDs
- metadata/frontmatter
- tags
- layers
- document types
- module IDs
- submodule IDs
- parent/child links
- paired Yin/Yang links
- source block IDs
- status/version fields
- predictable Markdown structure

Principle:

```text
Use deterministic metadata first. Use semantic search as a helper.
```

---

## 11.1 Metadata Minimum

Minimum recommended fields:

```yaml
---
id:
title:
document_type:
layer:
status:
version:
created:
updated:
tags:
related:
---
```

For implementation-relevant documents, add:

```yaml
module_id:
submodule_id:
parent:
children:
paired_yin:
paired_yang:
schemas:
trace_map:
source_block_id:
generated_from:
depends_on:
used_by:
supersedes:
superseded_by:
```

---

## 11.2 Document Status

Recommended statuses:

```text
Draft
Review
Stable
Deprecated
Archived
Superseded
```

Retrieval should prefer `Stable` and `Review`.

Retrieval should exclude `Deprecated`, `Archived`, and `Superseded` by default unless historical context is requested.

---

## 11.3 Relationship Types

Recommended relationship fields:

| Field | Meaning |
|---|---|
| `parent` | Parent node |
| `children` | Child nodes |
| `paired_yin` | Matching Yin document |
| `paired_yang` | Matching Yang document |
| `depends_on` | Upstream dependency |
| `used_by` | Downstream consumer |
| `references` | Referenced documents |
| `generated_from` | Source document/process |
| `source_block_id` | Source block identity |
| `supersedes` | Older document replaced |
| `superseded_by` | Newer document replacing this one |
| `related` | Loose relationship |

Use specific relationship fields before using `related`.

---

## 11.4 Tags

Tags should be:

- concise
- consistent
- high-signal
- useful for retrieval

Bad tags:

```text
misc
stuff
important
general
feature
```

Good tags:

```text
settings
input
ui-state
collapse
auth
search-index
privacy
audit
idempotency
```

Do not use too many tags.

Use `layer`, `document_type`, `module_id`, and `submodule_id` for structural facts.

---

## 11.5 Tool-Agnostic Graph Storage

The graph can live in:

- plain Markdown folders
- Git repositories
- Anytype
- Obsidian
- Notion-style systems
- local folders
- static documentation sites
- custom tooling
- future Allzy tooling

The method requires structured documents and metadata.

The storage tool is replaceable.

Anytype is a strong practical example because it supports flexible types, collections, tags, backlinks, graph views, and exportable structures. It is not required.

---


---

# 12. Metadata, Config, and Retrieval Workflows

The Metadata Graph is operationalized through prompt config blocks, document frontmatter, retrieval builder workflows, metadata enrichment, metadata indexes, Search Logs, and context packages.

## 12.1 Prompt Config Blocks vs. Document Frontmatter

The framework uses two related but different YAML-style structures.

```text
Document frontmatter = metadata about a document
Prompt config block  = execution options for a prompt
```

Document frontmatter makes artifacts findable, linkable, filterable, and indexable.

Prompt config controls how an operational prompt executes.

Rule:

```text
Prompt config controls execution.
Document frontmatter describes artifacts.
```

## 12.2 Document Metadata Enrichment

Operational prompt:

```text
document_metadata_enrichment_prompt.md
```

Document Metadata Enrichment makes existing documents retrieval-ready.

It does:

```text
existing document
→ analyze content
→ add or update metadata/frontmatter
→ preserve document body
→ make the document easier to find, link, classify, and reuse
```

It does not:

- convert a document into Yin/Yang
- generate Yang contracts
- generate a Master Document
- perform Genesis
- perform Triage
- implement code
- fix bugs
- rewrite application logic
- change document meaning
- invent missing project facts

## 12.3 Context Retrieval Builder

Operational prompt:

```text
context_retrieval_builder_prompt.md
```

The Context Retrieval Builder searches existing metadata-tagged documents and builds an output artifact based on user intent.

It uses two phases:

```text
Mode 1 = Intake / Search Planning
Mode 2 = Retrieval / Output Building
```

Supported output modes:

```text
summary
deep_brief
agent_context_package
patch_handoff_context
document_source_pack
review_context
custom
```

It does not implement code, fix bugs, rewrite source documents, create Yin/Yang documents, update `plan.md` / `memory.md`, or replace Workspace Context Initialization.

## 12.4 Retrieval Initialization Check

Before searching, retrieval workflows should check for:

```text
context_retrieval.md
metadata/frontmatter conventions
metadata-tagged documents
metadata_index.md / metadata_index.json
context root
docs root
memory file if requested
skills index if requested
```

If retrieval is not initialized, do not pretend deterministic retrieval is available.

Correct response:

```text
Retrieval is not initialized yet. Run Workspace Context Initialization first, or provide `context_retrieval.md` and metadata conventions.
```

## 12.5 Metadata Index

A metadata index is an optional generated lookup index.

Possible files:

```text
metadata_index.md
metadata_index.json
context_index.md
```

It should be generated from source document metadata where possible.

It should not become a separate manually maintained truth that silently diverges from the source documents.

## 12.6 Search Log

A Search Log records how context was selected.

It is not memory.

Confirmed lasting facts belong in `memory.md`.

Search Logs support auditability, debugging, context-package review, and handoff transparency.

## 12.7 Metadata, Config, and Retrieval Conventions Document

`07_Metadata_Config_and_Retrieval_Conventions.md` defines complete YAML/frontmatter and prompt-config conventions.

Document:

```text
07_Metadata_Config_and_Retrieval_Conventions.md
```

This is a conventions/reference document, not a prompt.


# 13. Retrieval Artifacts

V5 defines a clear separation between memory, retrieval method, selected context, and search logs.

```text
memory.md            = confirmed project state
context_retrieval.md = reusable retrieval method
metadata_index       = optional lookup index
context_package.md   = temporary selected context
Search Log           = retrieval audit trail
```

---

## 12.1 `context_retrieval.md`

`context_retrieval.md` defines how agents/scripts search the documentation graph.

It may include:

- search priority
- metadata fields
- allowed layers
- document types
- tag rules
- parent/child traversal
- paired Yin/Yang traversal
- memory section retrieval
- exclusion rules
- example commands
- Python/ripgrep examples
- context package format
- Search Log format

Recommended search priority:

```text
1. Exact id, module_id, submodule_id, document_type
2. Layer
3. High-signal tags
4. Paired Yin/Yang links
5. Parent/child links where needed
6. Related memory sections
7. Prior handoffs where relevant
8. Semantic search only as helper
```

---

## 12.2 Metadata Index

Optional files:

```text
metadata_index.json
metadata_index.md
context_index.md
```

Use when project size makes scanning all files inefficient.

The index may contain:

- document ID
- path
- title
- document type
- layer
- module ID
- submodule ID
- status
- tags
- parent/child links
- paired Yin/Yang links
- updated date

The index should be generated from document metadata where possible.

---

## 12.3 `context_package.md`

A context package is a temporary context bundle for one task/session.

It includes:

- task
- search goal
- filters used
- documents matched
- links followed
- relevant excerpts
- exclusions
- Search Log
- open questions
- handoff context

It should not become permanent memory.

Confirmed lasting facts go into `memory.md`.

---

## 12.4 Search Log

A Search Log records how context was selected.

It should include:

- user query/task
- metadata filters used
- documents matched
- memory sections matched
- links followed
- files/documents excluded
- archived/deprecated documents skipped
- unresolved retrieval uncertainty

Example:

```text
Search Log:
- Query: Settings/Input collapse height bug
- Filters: module_id=settings, submodule_id=settings.input, tags=collapse/ui-state
- Documents matched: core.settings.input.yin, core.settings.input.yang
- Memory matched: memory.md → Settings / Input
- Links followed: paired_yang, parent module
- Excluded: Settings/Provider, Dashboard, archived drafts
```

---

# 13. State Management

State Management preserves project continuity without preserving noise.

Core artifacts:

```text
plan.md              = current task focus
memory.md            = confirmed project/architecture memory
context_retrieval.md = reusable deterministic retrieval method
context_package.md   = temporary selected context
handoff              = scoped task instruction
```

---

## 13.1 `plan.md`

`plan.md` answers:

```text
What is being worked on right now?
```

It should be:

- short
- current
- category-based
- scoped
- actionable
- checkable

It is not:

- backlog
- roadmap
- changelog
- debug diary
- long-term memory
- raw chat log

Recommended structure:

```markdown
# Plan

_Last updated: YYYY-MM-DD_

## Current Focus

[Current task]

## [Category / Module / Area]

### Task
[One short task]

### Goal
[What done means]

### Status
- [ ] Step 1
- [ ] Step 2

### Scope
In scope:
- ...

Out of scope:
- ...

### Acceptance Criteria
- [ ] ...
```

---

## 13.2 `memory.md`

`memory.md` answers:

```text
What is currently true about this project or area?
```

It should store:

- confirmed project state
- architecture decisions
- current behavior
- useful implementation history
- files/contracts affected
- verification notes
- compact useful troubleshooting notes while unresolved

It should not store:

- raw failed attempts
- full chat history
- speculative reasoning
- obsolete decisions
- uncompressed logs
- the entire retrieval method

Recommended metadata:

```yaml
---
id: "state.memory"
title: "Project Memory"
document_type: "State File"
status: "Active"
updated: "YYYY-MM-DD"
last_compressed: "YYYY-MM-DD"
rounds_since_compression: 0
compression_status: "OK"
tags:
  - state
  - memory
---
```

Recommended section shape:

```markdown
## [Category / Module / Area]

### Current State

[What is true now.]

### Confirmed Changes

#### YYYY-MM-DD — [Short title]

**Status:** Confirmed  
**Reason:** ...  
**Changed:** ...  
**Files affected:** ...  
**Contracts affected:** ...  
**Verification:** ...  

### Useful Troubleshooting Notes

[Only compact notes that still help.]
```

---

## 13.3 Memory Compression

Use the 10/20 rule:

```text
~10 meaningful rounds since compression = compression recommended
~20 meaningful rounds since compression = compression mandatory
```

Compression should:

- preserve current truth
- remove old speculation
- merge duplicates
- remove resolved dead ends
- keep useful unresolved troubleshooting notes
- update metadata
- backup previous memory

Compression must not delete `context_retrieval.md`.

---

## 13.4 State and Retrieval Separation

Do not merge all state and retrieval into one file.

Correct split:

| Artifact | Purpose |
|---|---|
| `plan.md` | current task focus |
| `memory.md` | confirmed current truth |
| `context_retrieval.md` | reusable search method |
| `context_package.md` | selected context for a task |
| `metadata_index` | optional lookup table |
| handoff | scoped instruction |

This prevents memory from becoming a procedural search manual or permanent context dump.

---


---


## State Prompt Boundaries

Use the correct state/context prompt for the correct job.

| Need | Use |
|---|---|
| Create/check the workspace context layer | `workspace_context_initialization_prompt.md` |
| Clean/compress `plan.md`, `memory.md`, or `skills/` | `workspace_state_maintenance_prompt.md` |
| Find and package relevant task context | `context_retrieval_builder_prompt.md` |
| Add retrieval metadata to a document | `document_metadata_enrichment_prompt.md` |
| Create final Yin/Yang specification prompt | `yin_yang_prompt_generator.md` |
| Diagnose a bug and create Agent-2 handoff | Triage prompt family |

Do not use State Management prompts to implement code.

Do not use State Management prompts to create Yin/Yang documents.

Do not use State Management prompts to perform Triage.

Do not use State Management prompts to rewrite framework templates.


# 14. Workspace Context Architecture

Workspace Context Architecture prepares the target implementation workspace for AI-assisted work.

It is not a separate pipeline phase.

It is a support layer for Specification, Execution, Maintenance, Reviews, and cross-agent continuity.

The main operational prompt is:

```text
workspace_context_initialization_prompt.md
```

## 14.1 Target Implementation Workspace

Workspace context artifacts belong to the target implementation workspace.

They are not the same thing as the Framework GitHub repository prompt organization.

The framework repository stores:

- framework docs
- templates
- prompts
- examples
- references

The target implementation workspace stores project-specific context/state/retrieval artifacts such as:

```text
plan.md
memory.md
context_retrieval.md
context_package.md
Search Log
metadata_index
skills/
handoffs
```

## 14.2 Workspace Context Initialization

Workspace Context Initialization sets up, inspects, or repairs the workspace context layer.

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
- replace application runtime state architecture

## 14.3 Initialization Modes

The initialization prompt supports:

| Mode | Meaning |
|---|---|
| Website / Preconfigured Mode | A website or prompt builder fills the config block |
| Manual Config Mode | The user manually edits the config block |
| Assistant Mode | Config is empty/incomplete, so the assistant asks targeted questions |

The config block is fundamental.

If config is filled, execute according to config.

If config is empty, ask targeted setup questions one at a time.

## 14.4 Setup Profiles

Recommended setup profiles:

| Profile | Creates/checks |
|---|---|
| `inspect_only` | Inspect existing context setup only |
| `minimal` | `plan.md` + `memory.md` |
| `standard` | `plan.md` + `memory.md` + `context_retrieval.md` |
| `full` | Standard + context package template + Search Log template + optional metadata index + optional skills |
| `custom` | Explicit config choices |

Use `standard` as the normal baseline.

Use `full` for larger projects, Yin/Yang-heavy work, Triage-heavy workflows, or multi-agent work.

## 14.5 Workspace State Maintenance

Workspace State Maintenance maintains living workspace state.

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

It may health-check optional artifacts when explicitly requested:

```text
context_retrieval.md
metadata_index.md
metadata_index.json
context packages
search logs
```

It does not rewrite these by default.

It does not maintain:

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

`AGENTS.md` and `agenten.md` are outside default scope unless explicitly requested.

`context_retrieval.md` is a stable method file, not a normal cleanup target.

## 14.6 Workspace Skills

The workspace may optionally include:

```text
context/skills/
```

Skills are reusable objective helper rules for AI agents.

They are not Memory 2.0.

They are not search method files.

They are not temporary context packages.

Preferred structure:

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

Recommended lifecycle:

```text
candidate → review → approved → archived
```

Default safety policy:

```yaml
create_skills_structure: false
skills_format: "agentskills.io"
allow_skill_candidates: true
allow_auto_create_approved_skills: false
require_skill_review_before_activation: true
allow_external_skill_lookup: false
allow_skill_scripts: false
create_skills_index: true
create_skills_bundle: true
skills_bundle_is_generated: true
```

External skills may be checked/adapted later, but must not be blindly imported.

Skill scripts are disabled by default.


# 15. Triage and Maintenance

Triage separates diagnosis from implementation through Fast, Standard, and Deep operational prompt variants.

```text
Agent 1 = Triage Intake / Diagnostician / Handoff Compiler
Agent 2 = Executor / Implementation Agent
```

The Triage model is implemented through three operational prompt variants:

| Prompt file | Mode | Use for |
|---|---|---|
| `prompts/Triage/fast/000_universal.md` | Fast | Small, clear, low-risk bugs or visual fixes with obvious scope |
| `prompts/Triage/standard/000_universal.md` | Standard | Default triage for normal bugfixes and maintenance work |
| `prompts/Triage/deep/000_universal.md` | Deep | Risky, unclear, stateful, contract-heavy, multi-layer, or architecture-sensitive issues |

These variants change diagnostic depth and output length. They do not change the Agent 1 / Agent 2 separation.

All variants must preserve:

- Agent 1 no-code rule
- privacy/security checks
- honest model/platform reference handling
- fallback labeling
- scope boundaries
- no false optimization claims
- no unrelated scope bundling
- contract/state gap detection where relevant

Agent 1 processes:

- screenshots
- logs
- stack traces
- rough descriptions
- voice-to-text
- visual context
- suspected area
- desired behavior
- current behavior
- contracts
- state excerpts
- metadata retrieval results

Agent 1 produces:

- scoped Agent-2 handoff
- work type
- scope type
- boundaries
- acceptance criteria
- Search Log where relevant
- metadata/retrieval context
- optional JSON metadata

Agent 1 does not write code.

Agent 2 implements from the handoff.

---

## 15.1 Work Types

Recommended work types:

```text
VISUAL_UI_FIX
INTERACTION_FIX
STATE_FIX
DATA_FLOW_FIX
CONTRACT_FLAW
IMPLEMENTATION_FLAW
COPY_OR_LABEL_FIX
UNKNOWN
```

A contract flaw must not be hidden as a code fix.

---

## 15.2 Scope Types

Recommended scope types:

```text
SINGLE_ISSUE
SAME_AREA_BUNDLE
AUTO_SPLIT_MULTI_SCOPE
USER_REQUESTED_COMBINED_SCOPE
```

Default rule:

```text
One bug. One topic. One narrow area. One handoff.
```

Same-area bundling is allowed when tasks share:

- page
- component
- category
- file area
- workflow
- root cause
- state boundary

Unrelated scopes should be split automatically.

---

## 15.3 Metadata-First Triage

When metadata exists, Agent 1 should use deterministic retrieval before broad file discovery.

Order:

```text
metadata first
document context second
narrow file discovery third
broad repo search last
```

Use:

- `context_retrieval.md`
- metadata/frontmatter
- metadata index
- module ID
- submodule ID
- layer
- document type
- tags
- paired Yin/Yang
- memory section
- prior handoffs
- Search Logs

The handoff should include:

```text
Metadata / Retrieval Context
Search Log
File Discovery Boundaries
```

---

## 15.4 Agent-2 Setup Status

Every serious handoff should include:

```text
Agent-2 AI model: [provided / missing / value]
Agent-2 platform: [provided / missing / value]
AI model reference: [provided and used / missing / mismatch]
Platform reference: [provided and used / missing / mismatch]
Model-optimized: [YES / NO]
Platform-optimized: [YES / NO]
Fallback: [Universal Markdown / NO]
Mode: [Fast / Standard / Deep]
Scope Type: [...]
Metadata context: [provided / missing / not applicable]
Search Log: [included / not used / unavailable]
Blockers: [none / list]
```

Do not claim model/platform optimization without matching reference content.

---

## 15.5 Triage Prompt Variants

### Fast Triage Intake

Use:

```text
prompts/Triage/fast/000_universal.md
```

Fast Triage is for small, obvious, low-risk cases.

Use Fast when the issue is:

- visually clear
- one narrow scope
- unlikely to affect contracts
- unlikely to affect state/persistence
- unlikely to affect privacy/security
- unlikely to require deep metadata retrieval
- suitable for a short Agent-2 handoff

Fast may shorten explanation and output detail.

Fast must not weaken safety rules.

Do not use Fast when the issue is:

- broad
- unclear
- security-sensitive
- privacy-sensitive
- contract-related
- state-related
- data-flow-related
- architecture-relevant
- multi-scope
- likely to affect persistence
- likely to affect permissions
- likely to require model/platform reference handling
- likely to require documentation updates

If Fast is requested but unsafe, use Standard or Deep and briefly explain why.

### Standard Triage Intake

Use:

```text
prompts/Triage/standard/000_universal.md
```

Standard is the default Triage mode.

Use Standard for:

- normal bugs
- normal UI fixes
- normal interaction issues
- bounded state issues
- ordinary implementation flaws
- moderate data-flow issues
- standard Agent-2 handoffs
- metadata retrieval when available
- model/platform fallback handling

When no mode is specified, use Standard unless the issue is clearly safe for Fast or clearly requires Deep.

### Deep Triage Intake

Use:

```text
prompts/Triage/deep/000_universal.md
```

Deep is for unclear, risky, stateful, contract-heavy, multi-layer, or architecture-sensitive cases.

Use Deep when the issue is:

- unclear
- risky
- architecture-sensitive
- state-heavy
- data-flow-heavy
- contract-heavy
- privacy/security-sensitive
- cross-layer
- multi-scope
- likely to require Yin/Yang review
- likely to require `memory.md` review
- likely to require deterministic metadata retrieval
- likely to require model/platform-specific handoff care
- expensive to fix incorrectly

Deep may include more explicit:

- evidence separation
- confirmed facts vs assumptions
- uncertainty handling
- metadata/retrieval analysis
- Search Log
- contract/state implications
- scope splitting
- risk notes
- blocker handling
- acceptance criteria

Deep is still Triage.

Agent 1 still does not write code, produce patches, or modify files.

### Variant Selection Rule

Use the smallest Triage variant that safely preserves diagnosis quality and execution boundaries.

```text
Fast = obvious and low-risk
Standard = standard/default
Deep = unclear, risky, contract/state-heavy, or architecture-sensitive
```

The variant does not remove the split requirement. Unrelated scopes must still be split into separate handoff blocks.

---

# 16. Model/Platform Reference System

The framework separates:

```text
AI model
Platform / execution environment
```

The model affects:

- prompt shape
- reasoning style
- output structure
- instruction density
- uncertainty handling
- formatting

The platform affects:

- file access
- command execution
- patch format
- IDE/CLI behavior
- browser/computer-use availability
- repository access
- output workflow

Examples:

- Claude vs Claude Code
- GPT vs Codex CLI
- Gemini vs Antigravity-style execution environment
- Cursor as platform with selected model
- ChatGPT with tools/files as platform

## 16.1 Reference Packages

A Reference Package may include:

- model prompting references
- platform execution references
- output format rules
- examples
- anti-patterns
- task-mode guidance
- fallback guidance

A reference counts only if its content is present.

A link or file name is not enough.

## 16.2 Current Workflow

Current workflow is manual:

1. User identifies target model.
2. User identifies target platform.
3. User provides model reference if optimization is required.
4. User provides platform reference if optimization is required.
5. Agent checks reference availability.
6. Agent labels output as optimized or fallback.

## 16.3 Future Prism Registry

Future Prism may automate reference selection.

Potential inputs:

- task type
- output type
- target model
- target platform
- execution mode
- prompt shape
- available tools

Until then, manual Reference Packages are the operational path.

---

# 17. Splice Workflow

Splice is a practical block-processing workbench.

It is not the framework itself.

It supports the framework when large documents must be processed safely.

Typical workflow:

1. Create Master Document.
2. Segment into blocks.
3. Modularize blocks.
4. Load universal prompt.
5. Load Yin/Yang template/reference.
6. Process one block at a time.
7. Generate one document per block.
8. Preserve `source_block_id`.
9. Review output.
10. Store accepted docs.
11. Use them for implementation/handoffs.

Splice helps avoid the Batching Trap.

Instead of processing 50–100 blocks in one giant prompt, the project processes blocks safely and traceably.

---

# 18. Privacy and Security Rules

Security and privacy apply across the entire framework.

## 18.1 No Secrets in Context

Never include real secrets in:

- prompts
- docs
- examples
- screenshots
- logs
- handoffs
- context packages
- memory files
- metadata headers

Use placeholders:

```text
$ENV_API_KEY
$ENV_DATABASE_URL
$ENV_SESSION_SECRET
process.env.SERVICE_TOKEN
```

## 18.2 Stop on Secrets

If real secrets appear:

1. stop
2. do not repeat the secret
3. ask for sanitized input
4. continue only after replacement

## 18.3 Privacy as System Concern

Privacy belongs to System architecture.

Define early:

- what data exists
- where it is stored
- retention/deletion
- logging
- redaction
- export
- access
- external AI exposure
- audit
- consent where relevant

---

# 19. Operational Workflows

## 19.1 New Product / Major Feature Workflow

```text
Genesis Full
→ Master Document
→ Segmentation
→ Modularization
→ Layer assignment
→ Module/submodule docs
→ Yin/Yang contracts
→ Metadata headers
→ Context retrieval setup
→ plan.md
→ implementation handoffs
→ execution
→ verification
→ memory.md update
```

Use for large products, platforms, SaaS ideas, major features, or long-lived systems.

## 19.2 Small Tool / Script Workflow

```text
Genesis Compact
→ Master Document Compact
→ small module/task definition
→ Yin/Yang Compact or Direct Scoped Prompt
→ implementation
→ verification
→ memory update if useful
```

Use only when risk and scope are small.

## 19.3 Bugfix Workflow

```text
User observes issue
→ select Fast / Standard / Deep triage mode
→ Agent 1 triage
→ deterministic retrieval if available
→ scope detection
→ split unrelated scopes
→ Agent-2 handoff
→ implementation
→ verification
→ contract/memory update if needed
```

## 19.4 Context Retrieval Workflow

```text
Read context_retrieval.md
→ filter metadata / metadata_index
→ follow explicit links
→ exclude archived/deprecated docs
→ build context_package.md
→ include Search Log
→ provide selected context to agent
```

## 19.5 Cross-Agent Continuity Workflow

```text
Update plan.md
→ extract relevant memory.md
→ include metadata IDs
→ include context package/search log
→ provide scoped handoff
→ execute
→ verify
→ update memory.md
```

Use when switching between ChatGPT, Claude, Codex, Cursor, Gemini, CLI agents, IDE agents, or other tools.

---

# 20. Repository / Folder Structure Guidance

Recommended structure:

```text
allzy-framework/
├── docs/
│   ├── 01_Philosophy.md
│   ├── 02_Architecture.md
│   ├── 03_Yin_Yang_Contracts.md
│   ├── 04_Deterministic_Metadata_Graph.md
│   ├── 05_Triage_and_Maintenance.md
│   ├── 06_State_Management.md
│   ├── 09_Origin_and_Principles.md
│   └── README.md
│
├── templates/
│   ├── prompts/
│   ├── documents/
│   └── context/
│
├── examples/
│
├── references/
│
├── README.md
└── LICENSE.md
```

`references/` may be excluded from public release if it contains private or volatile model/platform reference material.

---

# 21. Required Template/Prompt Alignment

After V5, templates and prompts must be synchronized.

Needed updates:

## 21.1 Document Templates

Yin/Yang templates should include:

- metadata/frontmatter placeholders
- layer
- module ID
- submodule ID
- paired Yin/Yang links
- source block ID
- generated from
- status
- version
- tags
- open questions
- quality checklist

## 21.2 Prompt Templates

Prompts should include:

- current Full/Compact/Direct terminology
- no outdated terminology
- privacy/security check
- phase boundaries
- no premature Yin/Yang in Genesis
- metadata generation where relevant
- context retrieval where relevant
- model/platform reference handling where relevant
- fallback labeling where relevant

## 21.3 Context Templates

Recommended new templates:

```text
templates/context/context_retrieval_template.md
templates/context/context_package_template.md
templates/context/search_log_template.md
templates/context/metadata_index_template.md
```

## 21.4 Operational Prompts Worth Adding

Recommended prompts:

```text
prompts/Triage/fast/000_universal.md
prompts/Triage/standard/000_universal.md
prompts/Triage/deep/000_universal.md
workspace_context_initialization_prompt.md
workspace_state_maintenance_prompt.md
context_retrieval_builder_prompt.md
document_metadata_enrichment_prompt.md
yin_yang_prompt_generator.md
yin_yang_consistency_review_prompt.md
framework_docs_consistency_review_prompt.md
```

These prompts should execute the framework rules without bloating the main docs.

The three Triage prompts are variants of one Triage model:

```text
Fast    = small, clear, low-risk cases
Standard = standard/default triage
Deep    = unclear, risky, stateful, contract-heavy, or architecture-sensitive cases
```

---

# 22. Quality Gates

## 22.1 Genesis Quality Gate

- product purpose clear
- audience clear
- core value clear
- first-release scope separated from future ideas
- out-of-scope explicit
- privacy/security visible
- confirmed decisions separated from assumptions
- open questions listed
- no architecture/code generated prematurely

## 22.2 Architecture Quality Gate

- Vision/Infrastructure/System/Core separated
- reusable System capabilities identified
- Core business logic separated
- optional Ecosystem/Utilities not mixed into Core
- modules coherent
- submodules small enough
- privacy/data protection treated as system concern
- no tool-first architecture

## 22.3 Yin/Yang Quality Gate

- Yin preserves human intent
- Yang defines execution contract
- Core/Shell boundary clear
- schemas present where needed
- action registry present
- invariants/test cases present
- open contract gaps marked
- metadata present
- source traceability present where generated
- no hidden business logic invented

## 22.4 Metadata Quality Gate

- stable IDs
- document types correct
- layer correct
- tags high-signal
- parent/child links correct
- paired Yin/Yang correct
- status current
- archived/deprecated excluded by default
- source block traceability preserved where relevant

## 22.5 Triage Quality Gate

- Agent 1 does not write code
- Agent 2 handoff scoped
- Triage mode selected: Fast / Standard / Deep
- Fast used only for small, clear, low-risk cases
- Standard used as default for normal maintenance
- Deep used for unclear, risky, stateful, contract-heavy, or architecture-sensitive cases
- multi-scope requests split
- metadata retrieval used when available
- Search Log included when retrieval used
- work type classified
- scope type classified
- acceptance criteria testable
- model/platform status honest
- privacy check complete

## 22.6 State Quality Gate

- `plan.md` current and short
- `memory.md` confirmed and compressed
- `context_retrieval.md` separate from memory
- `context_package.md` temporary
- Search Logs not dumped into memory by default
- compression metadata current
- no raw chat history stored as memory
- no secrets stored

---

# 23. Anti-Patterns

Avoid:

- AI guessing
- code-first prompting
- premature Yin/Yang
- giant all-in-one prompts
- broad repository search by default
- context dumping
- memory as raw chatlog
- retrieval method inside memory
- semantic retrieval as source of truth
- false model/platform optimization
- contract-blind patches
- state dumping
- system/core confusion
- utility/product confusion
- privacy as late polish
- tool lock-in
- metadata theater
- tag flooding
- broken links/backlinks
- permanent context packages
- unverified memory updates

---

# 24. Non-Goals

The Allzy Framework does not:

- require one specific AI model
- require one specific coding agent
- require one specific editor
- require one specific graph tool
- require Anytype
- require Splice
- require Prism
- replace legal/security review
- guarantee bug-free code
- remove the need for human judgment
- make every task require heavy documentation
- make RAG mandatory
- make vector search the source of truth
- turn prompts/templates into the master spec

The framework provides a method.

Tools improve the method.

---

# 25. Future Extensions

Planned or possible future extensions:

- Prism Registry for automatic model/platform reference resolution
- richer Prompt Library / Reference Packages
- metadata schema validation
- generated metadata indexes
- context retrieval scripts
- Splice integration for source block traceability
- state compression automation
- documentation consistency audit prompts
- public/private reference separation
- model/platform profile packs
- example packs
- tool-specific adapters

Future extensions must not weaken the core principles:

- no AI guessing
- small scopes
- explicit contracts
- deterministic retrieval
- controlled state
- privacy/security before execution
- honest fallback labeling

---

# 26. Current Working Baseline

The current V5 baseline is:

```text
Full / Compact / Direct terminology only.
Genesis creates Master Documents, not Yin/Yang.
Architecture separates Vision, Infrastructure / Backend, System, Core, optional Ecosystem, optional Utilities.
Specification creates Yin/Yang after modularization.
Yin preserves human intent.
Yang constrains technical execution.
Metadata makes documents retrievable.
context_retrieval.md defines search method.
context_package.md carries temporary selected context.
memory.md stores confirmed project truth.
plan.md stores current task focus.
Triage separates Agent 1 diagnosis from Agent 2 execution and supports Fast / Standard / Deep operational prompt variants.
Model/platform optimization requires references.
Privacy/security are architecture conditions.
Tools support the method but do not replace the method.
```



## 21.7 Workspace Context Quality Gate

- Workspace context artifacts belong to the target implementation workspace
- `plan.md` exists or is intentionally omitted
- `memory.md` exists or is intentionally omitted
- `context_retrieval.md` exists for standard/full setups
- context package and Search Log templates exist for full setup where selected
- metadata index exists only if selected or needed
- `skills/` is optional and not treated as Memory 2.0
- `skills_bundle.md` is generated, not source of truth
- `AGENTS.md` / `agenten.md` are excluded unless explicitly requested
- initialization and maintenance are not confused

## 21.8 Metadata / Retrieval Quality Gate

- Document frontmatter describes artifacts
- Prompt config controls execution
- Document Metadata Enrichment does not convert to Yin/Yang
- Context Retrieval Builder does not rewrite documents
- Retrieval initialization is checked before claiming deterministic retrieval
- Search Log is included when retrieval was used
- Search Log is not treated as memory
- metadata index is generated from source metadata where possible

---

# 27. Website-Ready Summary

The Allzy Framework is a specification-first method for AI-assisted software development.

It exists because AI agents fail when they must infer product intent, architecture, scope, contracts, state, or privacy rules from vague prompts.

The framework moves the important thinking before implementation:

```text
Genesis clarifies intent.
Architecture decomposes the product.
Yin preserves human meaning.
Yang constrains execution.
Metadata makes documents retrievable.
Triage separates diagnosis from implementation through Fast, Standard, and Deep operational prompt variants.
State Management preserves continuity without context noise.
Reference Packages adapt handoffs to models and platforms.
```

The goal is not heavier documentation.

The goal is less guessing.

When an AI agent receives clear intent, a small scope, current state, deterministic context, and a precise handoff, implementation becomes smaller, safer, faster, and easier to verify.