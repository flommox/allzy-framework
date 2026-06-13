---
id: "allzy.framework.docs.08.glossary-and-terminology"
title: "08 — Glossary and Terminology"
artifact_type: "Framework Documentation"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - glossary
  - terminology
---

# 08 — Glossary and Terminology

## Status

This document defines core terminology used across the Allzy Framework.

It is a glossary and terminology reference.

It is not a prompt.

It is not a template.

It is not a specification contract by itself.

It exists to prevent ambiguity across framework docs, prompts, templates, examples, READMEs, AI handoffs, and implementation workflows.

---

# 1. Purpose

The Allzy Framework depends on consistent language.

Many framework terms look similar but mean different things:

- Core Layer vs. Functional Core
- Workspace Context Initialization vs. Workspace State Maintenance
- Document Frontmatter vs. Prompt Config Block
- Search Log vs. `memory.md`
- Context Package vs. `context_retrieval.md`
- Skills vs. Memory
- Model vs. Platform
- Genesis Compact vs. Direct
- Yin/Yang Compact vs. Yang Core Module

If these terms drift, prompts and implementation agents start mixing concepts.

This document defines the shared vocabulary.

The goal is:

```text
Use the same term for the same concept everywhere.
```

---

# 2. Terminology Rules

## 2.1 Use Current Scope Terms

The current scope terms are:

```text
Full
Compact
Direct
```

Use these terms consistently.

Do not introduce alternative names for the same scope levels.

## 2.2 Do Not Invent Synonyms for Core Terms

Do not casually rename framework terms.

For example:

| Correct | Avoid |
|---|---|
| Genesis Compact | Compact Genesis |
| Master Document Compact | Compact Master Document |
| Yin/Yang Compact | weight Yin/Yang |
| Yang Core Module | Yang Contract  |
| Workspace Context Initialization | Workspace Setup Wizard |
| Workspace State Maintenance | Memory Cleanup Only |
| Context Retrieval Builder | RAG Builder |
| Document Metadata Enrichment | Metadata Conversion |
| Prompt Config Block | Runtime Frontmatter |

Synonyms may be listed as aliases for retrieval, but they should not become official terminology.

## 2.3 Use Precise Boundaries

If two terms overlap, explain the boundary rather than merging them.

Example:

```text
Search Log records what was retrieved.
memory.md stores confirmed current project truth.
```

They may reference each other, but they are not the same artifact.

---

# 3. Framework-Level Terms

## Allzy Framework

A specification-first method for AI-assisted software development.

It helps humans and AI agents move from raw ideas to structured implementation by using clear phases, explicit artifacts, metadata, context management, and scoped execution.

The framework is not a single prompt.

The framework is not one app.

The framework is not a generic RAG system.

## Specification-First Development

A development approach where intent, scope, rules, contracts, context, and verification criteria are clarified before implementation.

In the Allzy Framework, this usually happens through Genesis, architecture decomposition, Yin/Yang documents, metadata, Triage, and state/context workflows.

## Defined Context

Context that has been intentionally selected, structured, verified, and scoped.

Defined context is different from dumping every available file into an AI context window.

Defined context should answer:

- what is true?
- what is relevant?
- what is out of scope?
- what should be changed?
- what should not be changed?
- how will success be verified?

## AI Guessing

The behavior where an AI model fills missing requirements, architecture decisions, business rules, file paths, or implementation behavior without explicit evidence.

The framework exists largely to reduce AI guessing.

## Context Pollution

A state where too much irrelevant, stale, duplicated, conflicting, or unstructured context reduces AI output quality.

Context pollution often causes:

- wrong assumptions
- broad file discovery
- hallucinated requirements
- repeated failed fixes
- unnecessary token use
- architectural drift

## Deterministic Context Selection

Selecting context using explicit metadata, IDs, tags, document types, layers, relationships, module IDs, submodule IDs, source links, and status fields before relying on semantic similarity.

It is not the same as vector-only RAG.

---

# 4. Pipeline Terms

## Pipeline

The five-phase Allzy Framework process:

```text
Genesis
→ Segmentation
→ Modularization
→ Specification
→ Execution
```

The pipeline describes how an idea becomes implementable work.

## Phase 1 — Genesis

The collaborative human/AI ideation and clarification phase.

Genesis turns raw input into:

```text
Master Document
```

or:

```text
Master Document Compact
```

Genesis does not create final architecture, modules, Yin/Yang documents, implementation plans, or code.

## Phase 2 — Segmentation

The phase that divides a Master Document into topic areas, project areas, blocks, domains, or candidate areas.

Segmentation identifies what exists.

It does not yet define final implementation units.

## Phase 3 — Modularization

The phase that turns segmented areas into modules and submodules.

Modularization defines manageable units of responsibility.

## Phase 4 — Specification

The phase that turns modules/submodules into implementation-ready specifications.

This is where Yin/Yang documents usually appear.

## Phase 5 — Execution

The phase where agents implement, verify, patch, review, or maintain based on scoped prompts, contracts, context packages, and handoffs.

Execution should not be driven by vague prompts.

---

# 5. Scope Scale Terms

## Full

The full framework workflow for larger, higher-risk, long-lived, or architecture-relevant work.

Use Full for:

- products
- platforms
- systems
- SaaS ideas
- major features
- complex modules
- business logic
- persistence
- APIs
- permissions
- compliance/privacy/security concerns
- long-lived architecture

Full does not mean bloated.

It means complete enough to avoid unsafe guessing.

## Compact

A reduced-overhead workflow for smaller, bounded, lower-risk work.

Compact is not weaker.

Compact still requires:

- clear intent
- scope boundaries
- privacy/security discipline
- assumptions separated from facts
- open questions where needed
- acceptance criteria where applicable

Use Compact for:

- small tools
- scripts
- utilities
- narrow workflows
- bounded features
- smaller internal helpers

## Direct

A direct scoped prompt for trivial isolated work.

Use Direct only when the task has no meaningful impact on:

- architecture
- contracts
- state
- persistence
- APIs
- permissions
- privacy/security
- business logic
- cross-module behavior

Examples:

- copy change
- label change
- spacing tweak
- isolated CSS polish
- tiny visual adjustment

Direct is not a replacement for Compact when the task needs intent, scope, or decisions.

---

# 6. Genesis Terms

## Genesis Full

The full Phase 1 Genesis workflow.

It is used for large products, systems, platforms, SaaS ideas, major features, or high-risk work.

It produces:

```text
Master Document
```

## Genesis Compact

The compact Phase 1 Genesis workflow.

It is used for small tools, scripts, utilities, narrow workflows, low-risk tasks, or smaller features that still need clarified intent.

It produces:

```text
Master Document Compact
```

Genesis Compact is not weaker than Genesis Full.

It is smaller in scope and overhead.

## Master Document

The main output of Genesis Full.

It captures the full clarified project/product idea, including intent, audience, workflows, constraints, open questions, scope boundaries, decisions, assumptions, risks, and phase-2 inputs.

## Master Document Compact

The compact output of Genesis Compact.

It captures the minimum useful clarified intent for smaller work.

It is not a Project Tree.

It is not a Yin/Yang document.

It is not implementation code.

## Phase Boundary

A rule that prevents one phase from performing another phase prematurely.

Example:

```text
Genesis clarifies the idea.
Genesis does not create final Yin/Yang documents.
```

---

# 7. Architecture Terms

## Vision Layer

The layer containing product direction, purpose, roadmap direction, branding direction, strategy, and long-term intent.

Vision guides the system but is not itself customer-facing implementation logic.

## Infrastructure / Backend Layer

The layer containing runtime, deployment, hosting, databases, queues, secrets, APIs, CI/CD, backups, and technical foundations.

Infrastructure / Backend is usually reusable across products.

## System Layer

The reusable platform capability layer.

Examples:

- authentication
- identity
- permissions
- search
- datastore access
- audit logging
- notifications
- observability
- privacy/data protection

System capabilities should not be reinvented inside each Core module.

## Core Layer

The product-specific business logic layer.

Core is what the product is actually about.

Core changes from product to product.

The same infrastructure and system foundation may support different Core products.

## Ecosystem Layer

An optional layer for multiple independent but connected products/apps/platforms under one umbrella.

Not every project needs an Ecosystem layer.

## Utilities Layer

An optional layer for tools that support workflows, development, productivity, documentation, prompt generation, localization, research, UI composition, or other utility work.

Utilities may belong to a broader ecosystem while staying architecturally separate from the main product Core.

## Module

A coherent area of responsibility inside a product/system.

Examples:

```text
settings
auth
notifications
billing
search
workspace-context
```

## Submodule

A smaller independently implementable unit inside a module.

Examples:

```text
settings.input
auth.login
notifications.email
metadata.frontmatter
```

## Core Layer vs. Yang Core Module

These are different.

| Term | Meaning |
|---|---|
| Core Layer | Product-specific business logic layer |
| Yang Core Module | Technical Functional Core contract in a Yang document |

A System module can have a Yang Core Module.

A Core module can have a Yang Core Module.

Infrastructure can also have a Yang contract when technical execution rules must be precise.

---

# 8. Yin/Yang Terms

## Yin

The human-facing intent, product, domain, and workflow side of a specification.

Yin explains:

- what this is
- why it exists
- who it is for
- what behavior matters
- which business/domain rules apply
- what is out of scope
- what is still open

Yin may be written in a configured human language.

Technical identifiers should remain English unless explicitly overridden.

## Yang

The AI-facing technical execution contract.

Yang explains:

- schemas
- decision rules
- Functional Core / Imperative Shell boundaries
- action registry
- invariants
- idempotency
- errors
- edge cases
- tests
- traceability
- implementation handoff notes

Yang is normally English.

## Yin Page

A full human-intent document.

It captures product/domain meaning for a module, submodule, or feature area.

## Compact Yin Page

A smaller human-intent document for bounded work.

It does not replace Yang.

It does not define full technical execution.

## Yang Core Module

A full technical execution contract.

It defines deterministic implementation behavior.

There is no standalone Yang Compact.

## Yin/Yang Document

A combined document containing full Yin and full Yang.

## Yin/Yang Compact

A compact combined artifact for smaller work that needs both intent and execution rules but not a full Yang Core Module.

Yin/Yang Compact is not Yang Compact.

## Yang Compact

Invalid as a standalone framework artifact.

Correct rule:

```text
There is no standalone Yang Compact.
```

If someone asks for Yang Compact, choose one of:

- full Yang Core Module
- Yin/Yang Compact
- Compact Yin
- Direct Scoped Prompt

depending on the task.

## Functional Core

The pure decision logic area.

The Functional Core receives state, config, and input events/commands.

It returns decisions and action objects.

It does not perform side effects.

## Imperative Shell

The side-effect execution area.

The Imperative Shell reads/writes databases, calls APIs, sends messages, executes actions, gets current time, reads environment variables, and performs external work.

## Core/Shell Boundary

The boundary between pure logic and side effects.

Framework rule:

```text
The Core decides.
The Shell executes.
```

## Action Registry

The set of allowed actions that the Functional Core may request and the Imperative Shell may execute.

## Action Object

A structured output from the Functional Core describing what should be executed by the Shell.

## Invariant

A rule that must always remain true.

## Idempotency

The property that repeated execution of the same operation does not create unsafe duplicate effects.

## Trace Map

A mapping between intent, rules, decisions, schemas, actions, tests, and implementation notes.

Trace Maps help detect drift between what the product means and what the technical contract says.

---

# 9. Specification and Prompt Generator Terms

## Yin/Yang Prompt Generator

An operational prompt that creates a specialized Agent-2 prompt for generating a final Yin/Yang artifact.

It does not directly create the final Yin/Yang document.

```text
Agent 1 = Yin/Yang Prompt Generator
Agent 2 = Yin/Yang Specification Agent
```

## Yin/Yang Specification Agent

The Agent-2 role that receives the generated prompt and required template content, then creates the final Yin/Yang artifact.

## Existing Document Conversion Mode

A mode of the Yin/Yang Prompt Generator where an existing document is used as source context for a Yin/Yang specification.

The existing document is not the template.

The required Allzy template must still be attached, pasted, or directly accessible.

## Source Context

The source material used to generate or enrich an artifact.

Examples:

- Master Document
- module block
- submodule block
- old Markdown document
- product note
- architecture note
- specification
- research note

## Template Content

The actual template text/file that an agent can read.

A repository link is not template content.

A link only tells the user where to find the template.

## Contract Gap

A missing or unclear technical execution detail that prevents a Yang contract or implementation task from being safely completed.

Contract gaps should be marked, not invented.

## Open Question

A missing product, domain, or human-intent decision that requires human clarification.

Open Questions should not be patched over with implementation guesses.

---

# 10. Metadata and Config Terms

## Metadata

Structured descriptive information about an artifact.

Metadata helps classify, retrieve, link, validate, review, and reuse documents.

## Frontmatter

A YAML-style metadata block at the top of a document.

Frontmatter describes the document.

It does not control prompt execution.

## Document Frontmatter

Same as frontmatter, specifically used for documents.

It answers:

```text
What is this artifact?
```

## Prompt Config Block

A YAML-style config block inside an operational prompt.

It controls prompt execution.

It answers:

```text
How should this prompt run?
```

## Config-First Principle

The rule that operational prompts should execute according to filled config values and only ask questions when required config is missing.

```text
If config is filled, execute according to config.
If config is empty or incomplete, switch to Assistant Mode.
```

## Preconfigured Mode

A workflow mode where a website, prompt builder, or user has already filled the config block.

The assistant should not ask redundant setup questions.

## Manual Config Mode

A workflow mode where the user manually edits the config block.

Manual config should be treated the same as website-generated config.

## Assistant Mode

A workflow mode where required information is missing and the assistant asks targeted setup questions.

Preferred behavior:

```text
Ask one necessary question at a time.
```

## Universal Fallback Mode

A workflow mode where output is still possible but required references, model details, platform details, or configuration values are missing.

Fallback output must be labeled.

Do not claim optimization in fallback mode.

## Optional Clarification Mode

A workflow mode where non-critical information is missing, but the assistant proceeds and lists optional clarifications that would improve specialization.

## Metadata Version

The version of the metadata schema or convention used in the frontmatter.

It is not the same as the document version.

## Document Version

The version of the document content itself.

---

# 11. Metadata Field Terms

## `id`

A stable identifier for a document or artifact.

Should be unique enough inside the project.

## `title`

The human-readable title.

## `document_type`

The type of artifact.

Examples:

```text
Framework Documentation
Prompt
Template
Example
Yin Page
Yang Core Module
State File
Context Package
Search Log
Metadata Index
Skill
```

## `document_role`

The role the document plays in the workflow.

Examples:

```text
Operational Prompt
Conventions Reference
Reusable Template
Filled Example
Source Context
Implementation Contract
```

## `layer`

The framework layer or context area.

Examples:

```text
Vision
Infrastructure / Backend
System
Core
Ecosystem
Utilities
Framework
Workspace Context
Reference
Example
```

## `tags`

Specific retrieval helper labels.

Tags should not replace structural fields.

## `aliases`

Alternative names useful for retrieval.

Aliases may include old working names for search, but aliases do not make old terminology official.

## `keywords`

Additional lower-priority search terms.

## `summary`

A concise summary of the document.

## `retrieval_description`

A retrieval-oriented description explaining when and why this document should be selected.

## `search_intent`

A list of user search intents that should retrieve this document.

## `source_block_id`

The ID of the source block that generated the document.

Useful for Splice workflows.

## `generated_from`

The source artifact or workflow that generated the document.

## `module_id`

The module identifier.

## `submodule_id`

The submodule identifier.

## `paired_yin`

The matching Yin document for a Yang document.

## `paired_yang`

The matching Yang document for a Yin document.

## `retrieval_ready`

Whether the document is ready to participate in deterministic retrieval.

## `excluded_from_retrieval`

Whether the document should be excluded from normal retrieval.

## `uncertain_fields`

Metadata fields that were inferred or cannot be confirmed.

## `missing_context`

Information needed to improve metadata quality.

## `needs_human_review`

Whether a human should review the metadata before relying on it.

---

# 12. Deterministic Metadata Graph Terms

## Deterministic Metadata Graph

A documentation graph built from explicit metadata, IDs, links, tags, document types, layers, module IDs, submodule IDs, relationships, and statuses.

It allows retrieval based on structure rather than only semantic similarity.

## Graph Node

A document or artifact that participates in the metadata graph.

Examples:

- Yin page
- Yang contract
- Master Document
- memory section
- prompt
- template
- context package
- skill

## Relationship

A structured connection between graph nodes.

Examples:

- parent
- children
- related
- references
- depends_on
- used_by
- paired_yin
- paired_yang
- supersedes
- superseded_by

## Metadata Index

A generated lookup index created from document metadata.

Possible files:

```text
metadata_index.md
metadata_index.json
context_index.md
```

A metadata index is not the source of truth.

The source documents and their frontmatter are the source of truth.

## Retrieval Signal

Any field or structural clue used to select relevant context.

Examples:

- ID
- document type
- layer
- module ID
- submodule ID
- tags
- aliases
- paired Yin/Yang
- parent/child links
- retrieval description
- file path

## Derived Retrieval Key

A search key inferred from natural-language user input.

Derived keys must be marked as derived, not confirmed.

## Semantic Search

Search based on meaning rather than exact metadata.

Semantic search may be useful, but in the framework it should assist deterministic retrieval rather than replace it.

## RAG

Retrieval-Augmented Generation.

The framework may use retrieval, but it is not defined as a generic vector-only RAG system.

## Deterministic Retrieval

Retrieval using explicit metadata and relationships before semantic similarity.

---

# 13. Context and Retrieval Terms

## `context_retrieval.md`

A stable method file that explains how agents or scripts should retrieve relevant context in a target workspace.

It is not memory.

It is not a context package.

It is not a normal cleanup target.

It should not be compressed like `memory.md`.

## Context Retrieval Builder

An operational prompt/workflow that selects and packages relevant context for a specific output.

It can produce:

```text
summary
deep_brief
agent_context_package
patch_handoff_context
document_source_pack
review_context
custom
```

It does not implement code.

It does not fix bugs.

It does not rewrite documents.

It does not create Yin/Yang documents.

## Search Log

An audit trail showing what was searched, selected, excluded, and why.

Search Log is not memory.

## Context Package

Temporary selected context for one task.

A context package may include a Search Log, relevant excerpts, selected sources, exclusions, open questions, and handoff notes.

It is not permanent memory.

## Agent Context Package

A context package prepared for an AI agent.

## Patch Handoff Context

A context package focused on a patch/fix task.

## Document Source Pack

A context package focused on documentation or writing work.

## Review Context

A context package prepared for review or audit.

## Deep Brief

A detailed briefing assembled from selected context.

## Summary

A short output summarizing selected context.

## Retrieval Initialization Check

The check that determines whether deterministic retrieval is available before claiming it can be used.

Look for:

- `context_retrieval.md`
- metadata/frontmatter conventions
- metadata-tagged documents
- metadata index
- docs root
- context root
- memory file if requested
- skills index if requested

If not available, do not pretend retrieval is initialized.

---

# 14. Workspace State Terms

## Workspace Context Architecture

The support layer that prepares a target implementation workspace for AI-assisted work.

It includes plan, memory, retrieval method, context packages, Search Logs, metadata indexes, optional skills, and handoffs.

It is not a separate framework pipeline phase.

## Target Implementation Workspace

The project/repository/folder/environment where implementation or documentation work happens.

It is different from the Framework repository.

## Workspace Context Initialization

The setup, inspection, or repair workflow for the workspace context layer.

Operational prompt:

```text
workspace_context_initialization_prompt.md
```

It creates/checks artifacts such as:

- `plan.md`
- `memory.md`
- `context_retrieval.md`
- context package template
- Search Log template
- metadata index template
- optional `skills/`

It does not write application code.

## Workspace State Maintenance

The cleanup, compression, update, or review workflow for living workspace state.

Operational prompt:

```text
workspace_state_maintenance_prompt.md
```

It maintains:

- `plan.md`
- `memory.md`
- `skills/`
- `skills_index.md`
- `skills_bundle.md`

It does not perform Triage.

It does not initialize the workspace.

It does not rewrite application code.

## `plan.md`

The current task focus.

It should contain:

- current tasks
- active scope boundaries
- acceptance criteria
- immediate next steps
- blockers

It is not a backlog.

It is not a changelog.

It is not memory.

## `memory.md`

Confirmed current project / architecture memory.

It should contain current truths, accepted decisions, useful implementation history, important file/contract relationships, and relevant unresolved troubleshooting notes.

It is not raw chat history.

It is not the Search Log.

It is not the context package.

## `skills/`

Optional reusable objective helper rules for AI agents.

Skills are not Memory 2.0.

Skills should not store project state.

## `SKILL.md`

The source-of-truth file for an individual skill.

## `skills_index.md`

A generated or maintained index of available skills.

## `skills_bundle.md`

A generated helper bundle of skills.

It is not the source of truth.

## Living Workspace State

Current, active, useful project/session context that helps future AI agents continue work safely.

Examples:

- current plan
- confirmed memory
- approved skills

## State Compression

The process of reducing `memory.md` or state files by removing stale, duplicated, or resolved information while preserving current truth.

## Cleanup Metadata

Metadata tracking maintenance/compression state.

Examples:

```yaml
last_maintenance: "YYYY-MM-DD"
last_compressed: "YYYY-MM-DD"
rounds_since_compression: 0
cleanup_status: "OK"
compression_status: "OK"
```

---

# 15. Triage Terms

## Triage

The maintenance workflow that turns messy human bug/context input into scoped Agent-2 handoffs.

Triage is diagnosis and handoff preparation.

Triage is not implementation.

## Agent 1

The diagnostic/handoff agent.

In Triage:

```text
Agent 1 = Triage Intake / Diagnostician / Handoff Compiler
```

Agent 1 does not write code.

## Agent 2

The execution/implementation agent.

Agent 2 receives the handoff and performs the implementation.

## Agent-2 Handoff

A scoped instruction package for Agent 2.

It should include:

- task
- context
- scope boundaries
- likely affected area
- constraints
- acceptance criteria
- output format
- fallback status
- model/platform status
- retrieval status where relevant

## Fast Triage

Fast operational Triage mode.

Use for small, clear, low-risk issues.

Prompt:

```text
prompts/Triage/fast/000_universal.md
```

## Standard Triage

Default operational Triage mode.

Use for normal maintenance tasks.

Prompt:

```text
prompts/Triage/standard/000_universal.md
```

## Deep Triage

Deep operational Triage mode.

Use for unclear, risky, state-heavy, contract-heavy, metadata-heavy, multi-layer, or architecture-sensitive issues.

Prompt:

```text
prompts/Triage/deep/000_universal.md
```

## Same-Area Bundle

A small group of related fixes that share the same page, component, workflow, root cause, or state boundary.

Allowed when it reduces overhead without mixing unrelated context.

## Multi-Scope Request

A request containing unrelated issues, modules, pages, categories, or root causes.

Should be split into multiple handoff blocks by default.

## Scope Type

A classification of how broad the task is.

Examples:

```text
SINGLE_ISSUE
SAME_AREA_BUNDLE
AUTO_SPLIT_MULTI_SCOPE
USER_REQUESTED_COMBINED_SCOPE
```

## Work Type

A classification of what kind of maintenance task is being handled.

Examples:

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

## Contract Flaw

A mismatch or missing rule in the specification/contract.

A contract flaw should not be hidden as a code-only patch.

## Implementation Flaw

A bug in code that violates an existing confirmed contract or expected behavior.

---

# 16. Model and Platform Terms

## AI Model

The model producing the output.

Examples:

- Claude
- GPT
- Gemini
- Codex-style model
- Perplexity
- another named model

The model affects:

- reasoning style
- prompt shape
- output structure
- instruction density
- uncertainty handling
- formatting

## Platform / Execution Environment

The tool or environment where the model runs or where work is executed.

Examples:

- Cursor
- Claude Code
- Codex CLI
- Codex app
- ChatGPT with tools/files
- Gemini / Antigravity-style environment
- IDE assistant
- CLI

The platform affects:

- file access
- patch format
- command execution
- tool use
- browser/computer-use availability
- repository access
- output workflow

## Model Reference

A reference document describing how to prompt or use a target model.

Model-optimized output requires actual model reference content.

## Platform Reference

A reference document describing the target execution platform.

Platform-optimized output requires actual platform reference content.

## Model-Optimized

Output adapted to a specific model based on provided model reference content.

Do not claim model optimization without reference content.

## Platform-Optimized

Output adapted to a specific platform/execution environment based on provided platform reference content.

Do not claim platform optimization without reference content.

## Universal Markdown Fallback

A model-neutral, platform-neutral Markdown output used when references are missing.

Fallback must be labeled.

---

# 17. Prompt Family Terms

## Operational Prompt

A prompt used to perform a framework workflow.

Examples:

- Genesis prompts
- Triage prompts
- Workspace Context Initialization prompt
- Workspace State Maintenance prompt
- Context Retrieval Builder prompt
- Document Metadata Enrichment prompt
- Yin/Yang Prompt Generator

## Prompt Family

A related group of operational prompts.

Current families:

- Genesis
- Triage
- Workspace / Context
- Retrieval / Metadata
- Specification

## Prompt Variant

A variant of a prompt for a specific scope, mode, model, platform, or depth.

Examples:

- Genesis Full
- Genesis Compact
- Triage Fast
- Triage Standard
- Triage Deep

## Adaptive Prompt Variant

A prompt variant adapted for a target model, platform, or environment.

Adaptive does not automatically mean optimized.

Optimization requires reference content.

## Single-Artifact Prompt

A focused prompt for one artifact.

Examples planned or optional:

- `plan_md_prompt.md`
- `memory_md_prompt.md`
- `context_retrieval_prompt.md`
- `context_package_generation_prompt.md`
- `metadata_index_generation_prompt.md`
- `skills_maintenance_prompt.md`

These are optional convenience prompts unless they exist as finalized source files.

---

# 18. Template, Example, and Reference Terms

## Template

A reusable structural document with placeholders or empty sections.

Templates are meant to be filled.

## Prompt Template

A reusable prompt file.

## Document Template

A reusable document structure.

Examples:

- Yin template
- Yang template
- Yin/Yang template
- context package template
- metadata frontmatter template

## Example

A filled reference artifact.

Examples demonstrate what a completed artifact may look like.

Examples are not templates.

## Reference

Supporting material used to adapt or ground output.

Examples:

- model reference
- platform reference
- prompting reference
- API reference
- external product reference

Reference content must be available to count as used.

A file name or link alone is not enough.

## Repository Link

A pointer to where something can be found.

A repository link is not the same as attached content.

---

# 19. File and Artifact Terms

## Framework Repository

The repository containing Allzy Framework docs, templates, prompts, examples, references, and README files.

## Target Workspace

The actual project workspace where framework workflows are applied.

## `docs/`

The documentation folder.

Contains explanatory framework docs or project docs depending on context.

## `templates/`

Reusable template files.

## `prompts/`

Operational prompt files, organized into top-level prompt families (Genesis, Triage, Workspace, Retrieval, Specification, Review).

## `templates/context/`

Reusable context, metadata, Search Log, context package, or metadata index templates.

## `examples/`

Filled examples.

## `Referenzen/`

Optional, supporting, internal reference material. Not part of the primary active publication surface.

## `context/`

In a target workspace, the folder for project-specific context artifacts.

## Handoff

A scoped instruction artifact passed from one agent/human/context to another.

## `AGENTS.md`

`AGENTS.md` is an external or workspace-specific agent instruction file.

It may contain instructions for coding agents, local tooling, repository-specific behavior, or execution environments.

It is not a core Allzy Framework state artifact.

It is not part of Workspace Context Initialization by default.

It is not part of Workspace State Maintenance by default.

It may be reviewed or updated only when the user explicitly includes it in scope.

Framework rule:

```text
Do not silently rewrite AGENTS.md as part of normal workspace context setup or state maintenance.
```


---


## `context_package_template.md`

A reusable template for creating task-specific context packages.

It is not the context package itself.

It is not memory.

It defines the structure that a future context package should follow.

## `search_log_template.md`

A reusable template for Search Logs.

It is not permanent memory.

It is not a complete history file.

It defines how retrieval activity should be recorded for one task, package, review, or handoff.

## `metadata_frontmatter_template.md`

A reusable template for standard document frontmatter.

It provides the metadata shape for documents that should participate in deterministic retrieval, indexing, linking, filtering, review, or future AI workflows.

It is not Document Metadata Enrichment itself.

## `prompt_config_block_template.md`

A reusable template for prompt configuration blocks.

It defines how a prompt can be preconfigured by a website, prompt builder, or human before execution.

It is not document frontmatter.

## `metadata_index_generation_prompt.md`

An optional focused prompt for generating a metadata index from document frontmatter.

It may create:

```text
metadata_index.md
metadata_index.json
```

The generated index is a lookup helper.

It is not the source of truth.

Source documents and their frontmatter remain the source of truth.

## `skills_maintenance_prompt.md`

An optional focused prompt for maintaining the workspace skills system.

It may review skill candidates, update `skills_index.md`, regenerate `skills_bundle.md`, or check skill lifecycle status.

It is not general Workspace State Maintenance.

It is not memory cleanup.

It should not auto-approve skills unless explicitly configured.


# 20. Naming Rules

## 20.1 Use Exact Prompt Names

Use:

```text
workspace_context_initialization_prompt.md
workspace_state_maintenance_prompt.md
context_retrieval_builder_prompt.md
document_metadata_enrichment_prompt.md
yin_yang_prompt_generator.md
```

Do not use approximate names in documentation.

## 20.2 Distinguish Similar Prompt Names

```text
context_retrieval_builder_prompt.md
```

means:

```text
universal retrieval/output builder
```

Potential future:

```text
context_retrieval_prompt.md
```

would mean:

```text
single-artifact prompt for creating/checking context_retrieval.md
```

Do not confuse them.

## 20.4 Do Not Rename Framework Concepts Casually

Incorrect:

```text
Metadata Wizard
```

Correct:

```text
Document Metadata Enrichment
```

Incorrect:

```text
Context Cleaner
```

Correct:

```text
Workspace State Maintenance
```

---

# 21. Common Confusions

## 21.1 `memory.md` vs. Search Log

| Artifact | Purpose |
|---|---|
| `memory.md` | confirmed current project truth |
| Search Log | record of what was searched/selected for a task |

Search Log is not memory.

## 21.2 `memory.md` vs. `skills/`

| Artifact | Purpose |
|---|---|
| `memory.md` | project-specific current truth |
| `skills/` | reusable helper rules for agents |

Skills are not Memory 2.0.

## 21.3 `context_retrieval.md` vs. Context Package

| Artifact | Purpose |
|---|---|
| `context_retrieval.md` | reusable search method |
| Context Package | temporary selected context for one task |

## 21.4 Document Metadata Enrichment vs. Yin/Yang Conversion

| Workflow | Purpose |
|---|---|
| Document Metadata Enrichment | add/update frontmatter |
| Existing Document Conversion Mode | generate prompt for converting source document into Yin/Yang artifact |

## 21.5 Workspace Initialization vs. State Maintenance

| Workflow | Purpose |
|---|---|
| Workspace Context Initialization | create/check context layer |
| Workspace State Maintenance | clean/compress living state |

## 21.6 Agent 1 vs. Agent 2

| Agent | Role |
|---|---|
| Agent 1 | diagnose, generate prompt, compile handoff |
| Agent 2 | execute, implement, produce final artifact |

## 21.7 Model vs. Platform

| Term | Meaning |
|---|---|
| Model | AI model producing output |
| Platform | execution environment/tool where the model runs or work happens |

Cursor is a platform.

Claude Code is a platform.

Claude is a model family.

## 21.8 Core Layer vs. Functional Core

| Term | Meaning |
|---|---|
| Core Layer | product-specific business logic layer |
| Functional Core | pure logic part of a Yang contract |

---

# 22. Quality Checklist

Before publishing or accepting terminology:

- [ ] Current terms are used consistently.
- [ ] `Full`, `Compact`, and `Direct` are used consistently.
- [ ] `Core Layer` is not confused with `Functional Core`.
- [ ] `Yang Core Module` is not called `Yang Compact`.
- [ ] `Workspace Context Initialization` is not treated as implementation.
- [ ] `Workspace State Maintenance` is not treated as Triage.
- [ ] `skills/` is not described as Memory 2.0.
- [ ] `skills_bundle.md` is not source of truth.
- [ ] `context_retrieval.md` is not treated as a context package.
- [ ] Search Log is not treated as memory.
- [ ] Document Metadata Enrichment is not described as Yin/Yang conversion.
- [ ] Context Retrieval Builder is not described as only Agent-2 packaging.
- [ ] model and platform are separated.
- [ ] repository links are not treated as attached content.
- [ ] prompt names match actual file names.
- [ ] optional future prompts are not described as finalized source files.
- [ ] aliases do not become official terminology.

---

# 23. Summary

The Allzy Framework relies on precise terminology because AI agents follow the language they receive.

Terminology is part of context control.

Use:

```text
Full / Compact / Direct
```

Use:

```text
Document Frontmatter
Prompt Config Block
Search Log
Context Package
Metadata Index
Workspace Context Initialization
Workspace State Maintenance
Context Retrieval Builder
Document Metadata Enrichment
Yin/Yang Prompt Generator
```

Do not merge similar terms.

Do not invent softer names.

When a term is unclear, define it before using it in prompts, templates, handoffs, or implementation instructions.
