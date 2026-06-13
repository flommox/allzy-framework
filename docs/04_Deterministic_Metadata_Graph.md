---
id: "allzy.framework.docs.04.deterministic-metadata-graph"
title: "04 — Deterministic Metadata Graph"
artifact_type: "Framework Documentation"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - metadata-graph
  - retrieval
---

# 04 — Deterministic Metadata Graph

## Summary

The Deterministic Metadata Graph is the Allzy Framework's method for making project documentation findable, linkable, filterable, and machine-selectable without relying on semantic guessing.

It turns structured Markdown documentation into a navigable project graph by using:

- stable document IDs
- YAML frontmatter or equivalent metadata
- tags
- layers
- modules and submodules
- document types
- parent/child relationships
- links and backlinks
- paired Yin/Yang references
- source block IDs
- status and version fields
- predictable section structure
- reusable retrieval rules

The goal is not to build a generic RAG system.

The goal is deterministic context selection.

The current framework operationalizes this through:

- metadata/frontmatter conventions
- `context_retrieval.md`
- optional metadata indexes
- Search Logs
- temporary context packages
- Document Metadata Enrichment
- Context Retrieval Builder workflows
- optional workspace skills indexes

```text
Do not ask the AI to guess which documents matter.
Make the documents identify themselves.
```

A well-structured Metadata Graph lets a human, script, coding agent, review agent, triage agent, or future tool locate the relevant context by reading explicit metadata and following explicit relationships.

This makes context retrieval faster, cheaper, more auditable, and less dependent on embedding similarity or broad file search.

---

## Source Authority

This document is based on the current Allzy Framework workflow, finalized prompts, finalized templates, finalized examples, current Architecture, Yin/Yang Contracts, Triage, State Management, and practical documentation workflow decisions.

Older documentation and previous master specifications are useful input, but they are not automatically correct. If old wording conflicts with the current architecture, current Yin/Yang contract model, current state-management rules, or practical metadata retrieval workflow, the current source-of-truth files win.

This document is explanatory framework documentation. It is not itself a metadata schema file, index file, prompt config file, index file, or implementation script.

A later dedicated conventions document may define the complete YAML/frontmatter and prompt-config conventions in one place. Until then, this document defines the retrieval model and the required documentation behavior.

---

## What the Deterministic Metadata Graph Is

The Deterministic Metadata Graph is a documentation graph built from explicit metadata and links.

It answers:

- Which document is this?
- Which type of document is it?
- Which layer does it belong to?
- Which module or submodule does it describe?
- Which parent document does it belong to?
- Which child documents belong to it?
- Which Yin document pairs with this Yang document?
- Which schemas are related?
- Which handoff references this contract?
- Which memory entry belongs to this module?
- Which source block generated this document?
- Which documents should be loaded together for a task?
- Which documents should be ignored?

The graph is deterministic because relationships are declared.

A tool should not have to infer that two documents are related only because they use similar words. It should be able to read the metadata and know.

---

## What the Deterministic Metadata Graph Is Not

The Deterministic Metadata Graph is not:

- generic RAG
- a vector database
- a replacement for documentation
- a replacement for Yin/Yang contracts
- a replacement for `memory.md`
- a replacement for `plan.md`
- a mandatory external database
- a mandatory Anytype setup
- a mandatory Obsidian vault
- a mandatory Notion workspace
- a mandatory graph database
- a fully automated knowledge system by default

It can be implemented with plain Markdown files.

It can be supported by documentation tools.

It can later be integrated into tooling such as Prism, Splice, or other Allzy tooling.

The minimum viable version is:

```text
structured Markdown
+ stable IDs
+ metadata/frontmatter
+ explicit links
+ consistent retrieval rules
```

---

# 1. Why Deterministic Metadata Matters

AI systems can search and summarize documents, but they can still select the wrong context when relationships are implicit.

Semantic search may retrieve a document because it sounds related. It may miss a document that is structurally required but uses different wording.

The Allzy Framework uses metadata to reduce that risk.

## Without Metadata

A task starts with:

```text
Find everything relevant to Settings/Input collapse behavior.
```

The agent must guess:

- which files mention Settings
- which files mention Input
- whether "collapse" means UI collapse, data collapse, or prompt collapse
- whether a document is old or current
- whether a Yin page exists
- whether a Yang contract exists
- whether related memory exists
- whether a generated handoff exists
- whether a schema is required

This creates unnecessary search, token use, and error risk.

## With Metadata

A task starts with:

```text
module_id: settings
submodule_id: settings.input
tags: collapse, ui-state
layer: Core
document_type: Yin Page / Yang Core Module
```

The agent can deterministically filter:

- all documents for `settings.input`
- the paired Yin and Yang
- related state memory
- related handoffs
- related schemas
- non-archived current documents
- one-hop parent module context

The context is selected by explicit relationships, not by guesswork.

---

# 2. Deterministic Retrieval vs. Generic RAG

Generic RAG and semantic search can be useful. They are not forbidden.

However, they should not be the source of truth for project-document relationships.

| Deterministic Metadata Graph | Generic RAG / Semantic Retrieval |
|---|---|
| Uses explicit IDs, tags, links, and metadata | Uses semantic similarity and ranking |
| Relationships are declared | Relationships are inferred |
| Easy to audit | Harder to explain why a result was chosen |
| Good for structured project context | Good for broad discovery |
| Works with simple scripts and text search | Usually needs embeddings or retrieval infrastructure |
| Can follow exact parent/child/pair links | May miss structurally required docs |
| Reduces context guesswork | May return related but irrelevant docs |
| Works well with predictable Markdown sections | Works across messy unstructured corpora |

The recommended rule:

```text
Use deterministic metadata first.
Use semantic search as a helper, not as the authority.
```

Semantic search can help discover unknown documents. Deterministic metadata should decide what belongs in the task context once the project structure is known.

---

# 3. Structured Markdown + Metadata

Metadata works best when documents also have predictable structure.

A YAML header alone is useful. A consistent document structure makes it much more powerful.

Yin/Yang documents are a strong example because they follow repeatable shapes:

- Yin has predictable intent, workflow, data concept, scope, and open question sections.
- Yang has predictable schema, decision, action, invariant, test, audit, and trace sections.
- Both can declare module, submodule, layer, status, paired documents, and tags.

This helps agents answer:

- where is the product intent?
- where is the execution contract?
- where are out-of-scope rules?
- where are open questions?
- where are tests?
- where are actions?
- where are trace links?
- where is the status?

The Metadata Graph should therefore combine:

```text
metadata for discovery
+ structured Markdown for interpretation
```

---


---

# 4. Prompt Config Blocks vs. Document Frontmatter

The framework uses two related but different YAML-style structures.

```text
Document frontmatter = metadata about a document
Prompt config block  = execution options for a prompt
```

They should not be confused.

## Document Frontmatter

Document frontmatter belongs at the top of a document.

It describes the document so humans, scripts, tools, and AI agents can identify and retrieve it.

It answers:

- what is this document?
- what type of document is it?
- which layer does it belong to?
- which module/submodule does it describe?
- which status does it have?
- which tags and aliases help retrieval?
- which documents are related?
- which source generated it?
- which other document pairs with it?

Example purpose:

```text
Make this document findable, linkable, filterable, and indexable.
```

## Prompt Config Block

A prompt config block belongs inside an operational prompt.

It tells the assistant how to run the prompt.

It answers:

- which mode should the prompt use?
- which output should be created?
- which files may be created or updated?
- which setup profile is selected?
- which retrieval depth is selected?
- which references are available?
- which target model/platform is intended?
- which fallback behavior is allowed?

Example purpose:

```text
Make this prompt executable in website/preconfigured, manual-config, or assistant mode.
```

## Relationship Between Both

Prompt config may produce or update documents that contain frontmatter.

For example:

- Workspace Context Initialization uses config to decide whether to create `context_retrieval.md`.
- Document Metadata Enrichment uses config to decide how much frontmatter to add.
- Context Retrieval Builder uses config to decide what output artifact to build.
- Metadata Index Generation uses document frontmatter as input.

Rule:

```text
Prompt config controls execution.
Document frontmatter describes artifacts.
```

Do not store prompt execution choices as permanent document truth unless they are also meaningful document metadata.


# 5. Minimum Viable Metadata

Every framework document should contain enough metadata to be identified and retrieved.

A minimal header:

```yaml
---
id: "settings.input.yin"
title: "Settings Input — Yin Page"
document_type: "Yin Page"
layer: "Core"
status: "Draft"
version: "0.1.0"
created: "2026-06-06"
updated: "2026-06-06"
tags:
  - settings
  - input
  - ui-state
related:
  - "settings.input.yang"
---
```

Minimum recommended fields:

| Field | Purpose |
|---|---|
| `id` | Stable document identity |
| `title` | Human-readable title |
| `document_type` | What kind of document this is |
| `layer` | Vision, Infrastructure / Backend, System, Core, Ecosystem, Utilities, etc. |
| `status` | Draft, Review, Stable, Deprecated, Archived |
| `version` | Document version |
| `created` | Creation date |
| `updated` | Last meaningful update |
| `tags` | Human and machine retrieval tags |
| `related` | General related documents |

Not every project needs every advanced field on day one. But every document should at least identify itself.

---

# 6. Extended Metadata for Framework Documents

Larger projects should use richer metadata.

Example:

```yaml
---
id: "settings.input.yang"
title: "Settings Input — Yang Core Module"
document_type: "Yang Core Module"
layer: "Core"
module_id: "settings"
submodule_id: "settings.input"
parent: "settings"
children: []
paired_yin: "settings.input.yin"
schemas:
  - "settings.input.config.schema"
  - "settings.input.state.schema"
  - "settings.input.event.schema"
  - "settings.input.result.schema"
trace_map: "settings.input.trace"
source_block_id: "block-023"
generated_from: "master-document-v1"
status: "Review"
version: "0.2.0"
created: "2026-06-06"
updated: "2026-06-06"
tags:
  - settings
  - input
  - collapse
  - ui-state
  - deterministic-core
depends_on:
  - "system.identity"
  - "system.datastore"
used_by:
  - "settings.input.handoff.fix-collapse-height"
supersedes: []
superseded_by: null
---
```

Extended fields:

| Field | Purpose |
|---|---|
| `module_id` | Module ownership |
| `submodule_id` | Submodule ownership |
| `parent` | Parent node |
| `children` | Child nodes |
| `paired_yin` | Matching Yin document |
| `paired_yang` | Matching Yang document |
| `schemas` | Related schema documents |
| `trace_map` | Trace relationship document |
| `source_block_id` | Splice or source block identity |
| `generated_from` | Source document or generation input |
| `depends_on` | Dependencies |
| `used_by` | Consumers or downstream docs |
| `supersedes` | Older documents replaced by this one |
| `superseded_by` | Newer document replacing this one |

Use fields only when they are meaningful. Empty metadata is less useful than concise accurate metadata.

---

# 7. Layer Metadata

Documents should declare their framework layer.

Recommended layer values:

```text
Vision
Infrastructure / Backend
System
Core
Ecosystem
Utilities
Privacy / Data Protection
Framework
Local
```

Layer values should match the project architecture.

Examples:

| Layer | Typical documents |
|---|---|
| `Vision` | product concept, roadmap, pricing, strategy, branding |
| `Infrastructure / Backend` | deployment, runtime, backend foundations, queues, databases |
| `System` | auth, search, datastore, communication, observability, UX foundations |
| `Core` | product-specific business logic, customer-facing workflows |
| `Ecosystem` | independent but connected products/apps/platforms |
| `Utilities` | tools such as prompt compilers, block processors, research utilities |
| `Privacy / Data Protection` | privacy, retention, deletion, consent, redaction, compliance notes |
| `Framework` | framework docs, templates, prompts, rules |
| `Local` | local-first workflows, local tools, local docs |

The exact layer vocabulary can be adapted per project, but it must remain consistent.

---


---

# 8. Document Metadata Enrichment

Document Metadata Enrichment is the workflow for making existing documents retrieval-ready.

Operational prompt:

```text
document_metadata_enrichment_prompt.md
```

Its job is:

```text
existing document
→ analyze content
→ add or update metadata/frontmatter
→ preserve document body
→ make the document easier to find, link, classify, and reuse
```

The prompt can be used for:

- Markdown documents
- product notes
- architecture notes
- research notes
- project documentation
- specifications
- prompts
- templates
- examples
- checklists
- decision records
- meeting notes
- technical references
- framework documents
- non-Yin/Yang source documents
- old documents that should become searchable
- documents prepared for later context retrieval
- documents that may later be converted into Yin/Yang

## What Metadata Enrichment Is Not

Document Metadata Enrichment does not:

- convert a document into Yin/Yang
- generate Yang contracts
- generate a Master Document
- perform Genesis
- perform Triage
- implement code
- fix bugs
- rewrite application logic
- change the document's meaning
- invent missing project facts

If a document later needs Yin/Yang conversion, use the Yin/Yang Prompt Generator workflow with Existing Document Conversion Mode and the required template content.

Metadata Enrichment only prepares the document for retrieval, indexing, linking, filtering, and review.

## Enrichment Rules

The document body is the source.

Metadata must describe the document.

Metadata must not invent new product facts.

If a field cannot be inferred safely:

- leave it empty
- mark it as uncertain
- add it to `uncertain_fields`
- add a note to `validation_notes`

Prefer useful empty fields over missing structural fields.

## Recommended Universal Metadata Shape

A full metadata shape may include:

```yaml
---
id: ""
title: ""
description: ""
document_type: ""
document_role: ""
layer: ""
status: "Active"
version: "0.1.0"
metadata_version: "1.0.0"

created: ""
updated: ""
last_reviewed: ""
review_status: ""
review_notes: ""

language: ""
primary_language: ""
secondary_languages: []
technical_identifiers_language: "English"

tags: []
aliases: []
keywords: []

summary: ""
retrieval_description: ""
search_intent: []
use_cases: []

source:
  type: ""
  origin: ""
  path: ""
  filename: ""
  url: ""
  imported_from: ""
  generated_from: ""
  source_block_id: ""
  source_document_id: ""

classification:
  confidentiality: ""
  sensitivity: ""
  audience: []
  lifecycle_stage: ""
  priority: ""
  stability: ""

scope:
  project: ""
  product: ""
  system: ""
  domain: ""
  module_id: ""
  submodule_id: ""
  component_id: ""
  feature_id: ""
  topic: ""
  subtopic: ""

structure:
  parent: ""
  children: []
  related: []
  references: []
  depends_on: []
  used_by: []
  supersedes: ""
  superseded_by: ""
  duplicates: []
  conflicts_with: []

yin_yang:
  is_yin_yang_document: false
  yin_document: ""
  yang_document: ""
  paired_yin: ""
  paired_yang: ""
  can_be_converted_to_yin_yang: ""
  recommended_conversion_target: ""
  conversion_notes: ""

retrieval:
  retrieval_ready: true
  retrieval_confidence: ""
  retrieval_priority: ""
  indexed: false
  index_id: ""
  chunking_hint: ""
  preferred_retrieval_keys: []
  excluded_from_retrieval: false
  exclusion_reason: ""

validation:
  metadata_inferred: true
  uncertain_fields: []
  missing_context: []
  needs_human_review: false
  validation_notes: []

output:
  preferred_filename: ""
  filename_source: ""
  suggested_folder: ""
---
```

Not every document needs every field filled.

The purpose of the richer shape is to support future retrieval, indexing, linking, filtering, and AI-assisted workflows without forcing the model to infer structure later.


# 9. Document Types

A `document_type` field helps tools and agents choose the right reading strategy.

Recommended values:

```text
Master Document
Master Document Compact
Project Tree
Module Page
Submodule Page
Yin Page
Yang Core Module
Yin/Yang Document
Yin/Yang Compact
Trace Map
Schema
ADR
README
Prompt Template
Document Template
Example
Agent Handoff
Triage Handoff
State File
Memory Entry
Retrieval Method
Context Package
Metadata Index
Reference Profile
Platform Reference
Model Reference
```

The document type should be specific enough to guide retrieval.

A `Yin Page` and a `Yang Core Module` should not both be labeled only as `Documentation`.

---

# 10. IDs

Stable IDs are the backbone of the graph.

A good ID is:

- stable
- unique
- lowercase where possible
- machine-readable
- not dependent on the exact file path
- not dependent on display title
- not too long
- not too vague

Example pattern:

```text
[layer].[module].[submodule].[artifact]
```

Examples:

```text
core.settings.input.yin
core.settings.input.yang
system.identity.access.yang
vision.pricing.strategy
framework.triage.maintenance
state.memory
retrieval.context
```

The exact pattern may vary, but the project should choose one and keep it stable.

## ID Rules

- Do not rename IDs casually.
- Do not reuse IDs for different documents.
- If a document is replaced, use `supersedes` and `superseded_by`.
- File names may change; IDs should remain stable.
- Display titles may change; IDs should remain stable.
- IDs should be short enough to use in links and metadata.

---

# 11. Tags

Tags support filtering and human navigation.

Good tags are:

- consistent
- concise
- lower-case where possible
- domain-specific
- useful for retrieval
- not redundant with every field
- not too numerous

Bad tags:

```text
important
misc
stuff
todo
general
document
feature
new
```

Good tags:

```text
settings
input
ui-state
collapse
authentication
search-index
privacy
audit
rate-limit
idempotency
core
system
```

## Tag Rules

- Prefer fewer high-signal tags.
- Do not use 30 tags when 5 are enough.
- Use consistent spelling.
- Avoid duplicate meanings such as `auth`, `authentication`, and `login-system` unless deliberately defined.
- Use layer/document fields instead of repeating them as tags when possible.
- Keep sensitive details out of tags.
- Review tags during document cleanup.

---

# 12. Relationship Types

The graph should use explicit relationship types.

Recommended relationship fields:

| Field | Meaning |
|---|---|
| `parent` | Parent node/document |
| `children` | Child nodes/documents |
| `paired_with` | General paired document |
| `paired_yin` | Matching Yin document |
| `paired_yang` | Matching Yang document |
| `depends_on` | Upstream dependencies |
| `used_by` | Downstream consumers |
| `references` | Documents this document references |
| `referenced_by` | Documents that reference this one |
| `implements` | Contract or feature implemented |
| `documents` | Thing this document documents |
| `generated_from` | Source document or process |
| `source_block_id` | Source block ID from Splice or block workflow |
| `supersedes` | Older document replaced by this one |
| `superseded_by` | Newer document replacing this one |
| `related` | Loose relationship when no stronger type fits |

Use strong relationship fields before using `related`.

`related` should not become a dumping ground.

---

# 13. Metadata for Yin/Yang Documents

Yin/Yang documents are ideal Metadata Graph nodes.

## Yin Page Metadata

```yaml
---
id: "core.settings.input.yin"
title: "Settings Input — Yin Page"
document_type: "Yin Page"
layer: "Core"
module_id: "settings"
submodule_id: "settings.input"
paired_yang: "core.settings.input.yang"
parent: "core.settings"
status: "Review"
version: "0.2.0"
tags:
  - settings
  - input
  - ui-state
  - product-intent
---
```

## Yang Core Module Metadata

```yaml
---
id: "core.settings.input.yang"
title: "Settings Input — Yang Core Module"
document_type: "Yang Core Module"
layer: "Core"
module_id: "settings"
submodule_id: "settings.input"
paired_yin: "core.settings.input.yin"
schemas:
  - "core.settings.input.config.schema"
  - "core.settings.input.state.schema"
  - "core.settings.input.event.schema"
  - "core.settings.input.result.schema"
trace_map: "core.settings.input.trace"
parent: "core.settings"
status: "Review"
version: "0.2.0"
tags:
  - settings
  - input
  - deterministic-core
  - ui-state
---
```

## Why This Matters

A retrieval tool can now answer:

- find Yin for `settings.input`
- find Yang for `settings.input`
- find schemas for the Yang
- find parent module
- find trace map
- find all documents tagged `ui-state`
- exclude archived documents
- include only `Review` or `Stable` documents

No semantic guessing required.

---

# 14. Metadata for Modules and Submodules

Module pages and submodule pages should also carry metadata.

Example module page:

```yaml
---
id: "core.content-workflow"
title: "Content Workflow"
document_type: "Module Page"
layer: "Core"
module_id: "content-workflow"
parent: "core"
children:
  - "core.content-workflow.publish"
  - "core.content-workflow.schedule"
  - "core.content-workflow.review"
status: "Draft"
tags:
  - content
  - workflow
  - publishing
---
```

Example submodule page:

```yaml
---
id: "core.content-workflow.publish"
title: "Publish Content Item"
document_type: "Submodule Page"
layer: "Core"
module_id: "content-workflow"
submodule_id: "content-workflow.publish"
parent: "core.content-workflow"
paired_yin: "core.content-workflow.publish.yin"
paired_yang: "core.content-workflow.publish.yang"
status: "Review"
tags:
  - content
  - publishing
  - workflow
---
```

A module page may be primarily human-facing.

A submodule page should normally lead to implementation documents.

---

# 15. Metadata for Handoffs

Agent handoffs should carry enough metadata to be traceable.

Example:

```yaml
---
id: "handoff.settings.input.fix-collapse-height"
title: "Fix Settings/Input Collapse Height"
document_type: "Agent Handoff"
work_type: "STATE_FIX"
scope_type: "SINGLE_ISSUE"
layer: "Core"
module_id: "settings"
submodule_id: "settings.input"
related_yin: "core.settings.input.yin"
related_yang: "core.settings.input.yang"
related_memory:
  - "memory.settings.input"
status: "Generated"
created: "2026-06-06"
tags:
  - settings
  - input
  - collapse
  - ui-state
---
```

This makes handoffs auditable.

A future agent can see:

- why the handoff exists
- which module it targets
- which contract it relates to
- which memory section matters
- which tags were used
- which work type was classified

---

# 16. Metadata for State Files

`plan.md` and `memory.md` are not normal product contracts, but they can still participate in the graph.

## `plan.md` Metadata

```yaml
---
id: "state.plan"
title: "Current Plan"
document_type: "State File"
status: "Active"
updated: "2026-06-06"
active_area: "settings.input"
tags:
  - state
  - plan
  - active-task
---
```

## `memory.md` Metadata

```yaml
---
id: "state.memory"
title: "Project Memory"
document_type: "State File"
status: "Active"
updated: "2026-06-06"
last_compressed: "2026-06-01"
rounds_since_compression: 8
compression_status: "OK"
tags:
  - state
  - memory
  - project-context
---
```

## Memory Entry References

Inside `memory.md`, category sections can reference metadata IDs:

```markdown
## Settings / Input

Related metadata:
- module_id: settings
- submodule_id: settings.input
- related_yin: core.settings.input.yin
- related_yang: core.settings.input.yang
- tags: settings, input, ui-state, collapse
```

This helps agents map memory back to documents.

---

# 17. Metadata for Splice Blocks

Splice or another block processor can generate documents from source blocks.

The graph should preserve the block origin.

Example:

```yaml
---
id: "core.settings.input.yin"
title: "Settings Input — Yin Page"
document_type: "Yin Page"
source_block_id: "block-023"
source_document: "master-document-v1.md"
generated_from: "splice-session-2026-06-06"
module_id: "settings"
submodule_id: "settings.input"
tags:
  - settings
  - input
---
```

This allows traceability:

```text
Master Document
→ Block 023
→ Yin Page
→ Yang Contract
→ Agent Handoff
→ Implementation
```

If a generated document seems wrong, the source block can be inspected.

If a block is reprocessed, the generated document can declare what it supersedes.

---

# 18. Collections, Types, and Human Graph Navigation

The framework is tool-agnostic, but human navigation matters.

A metadata graph should support both:

```text
machine retrieval
human retrieval
```

Machine retrieval uses metadata fields and scripts.

Human retrieval uses pages, collections, views, tags, links, and backlinks.

## Collections as Thematic Entry Points

Collections can act as top-level thematic entry points.

Examples:

- Framework
- Vision
- Backend
- System
- Core
- Ecosystem
- Utilities / Local
- Privacy / Data Protection

A collection is not merely a folder. It is a human-facing entry point into a thematic area of the graph.

Collections can be pinned or kept accessible for fast navigation.

A user should be able to open a collection and quickly see the relevant pages, modules, or submodules.

## Types as Node Classes

Types define what kind of node a page is.

Examples:

- Vision Page
- System Page
- Backend Page
- Core Module
- Bot Module
- Utility Page
- Privacy Page
- Framework Page
- Document Template
- Prompt Template
- Example

A type helps both humans and tools understand what a page represents.

## Filtered Views

Filtered views are a human retrieval layer.

Examples:

- all Core Modules
- all Bot Modules
- Bot Modules tagged `Moderation`
- Bot Modules tagged `Support`
- System pages tagged `Identity`
- Utilities tagged `Prompting`
- Privacy pages with status `Draft`
- Yin/Yang documents with status `Review`

Filtered views turn metadata into usable navigation.

## Backlinks

Backlinks make relationships visible.

A page can remain independent while still showing:

- parent module
- child submodules
- related contracts
- category pages
- collection pages
- source documents
- generated documents

This is useful because framework pages should be standalone enough to read directly, but connected enough to retrieve as part of their graph neighborhood.

---

# 19. Anytype as a Practical Graph Workspace

The Allzy Framework does not require Anytype.

Anytype is one practical example of a graph workspace that fits this workflow well because it supports independent pages, flexible object types, collections, tags, backlinks, graph views, and multiple human-facing views such as lists, tables, and galleries.

In an Anytype-style workflow, a project may create collections such as:

- Framework
- Vision
- Backend
- System
- Core
- Ecosystem
- Utilities
- Privacy / Data Protection

Each collection can contain typed pages.

For example:

- a `Core` collection may contain Core business logic areas
- a `System` collection may contain reusable platform capabilities
- a `Backend` collection may contain infrastructure/runtime/deployment pages
- a `Vision` collection may contain strategy, roadmap, pricing, and branding pages
- a `Utilities` collection may contain tools such as prompt compilers or block processors
- a module collection may show submodules filtered by category or tag

Anytype is useful because it combines:

- graph thinking
- independent pages
- flexible types
- collections
- filtered views
- backlinks
- visual graph navigation
- exportable documentation

However, it is only an example workflow.

The same principles can be applied in:

- plain Markdown folders
- Git repositories
- Obsidian
- Notion-style tools
- local documentation folders
- static site documentation
- custom documentation systems
- future Allzy tooling

The method requires structured documents, metadata, links, and retrieval rules. The storage tool is replaceable.

---

# 20. Privacy, Export-First Workflow, and Controlled Integrations

Documentation graphs may contain sensitive business information.

For sensitive documentation, prefer a controlled workflow.

## Export-First Workflow

A safe AI workflow is:

1. Maintain documentation in the graph tool of choice.
2. Export relevant Markdown or structured files.
3. Place exported files in a local project directory.
4. Run deterministic metadata search locally.
5. Generate a compact context package.
6. Give only that context package to the AI agent.

This reduces direct exposure of the full knowledge graph.

## Self-Hosted or Local Documentation

Some documentation tools can support local or self-hosted workflows depending on project setup and tool capabilities.

This can be useful for privacy, business secrets, and internal documentation control.

The framework does not require one hosting model. It recommends that sensitive documentation be managed with explicit privacy boundaries.

## MCP / API Access

Direct MCP, API, connector, or automation access to a knowledge graph can be useful.

It should be treated as a controlled integration.

Use direct access only when:

- the data is appropriate for that integration
- permissions are clear
- secrets are not exposed
- private personal information is not unnecessarily included
- business-sensitive material is intentionally allowed
- the user understands what the agent can access

For highly sensitive documentation, exported Markdown plus local deterministic filtering is often easier to audit.

---

# 21. Dedicated Retrieval Artifact: `context_retrieval.md`

The project may store the deterministic search method in a dedicated file:

```text
context_retrieval.md
```

This is recommended.

It is better than storing retrieval instructions only inside `memory.md`.

## Purpose

`context_retrieval.md` defines:

- how to search the metadata graph
- which fields to filter
- which relationship types to follow
- which files to exclude
- how to build a context package
- how to log the search
- which commands or scripts can be used
- how agents should behave before broad semantic search

## Why It Should Be Separate from `memory.md`

`memory.md` stores confirmed project state.

`context_retrieval.md` stores retrieval method.

Separating them prevents:

- retrieval logic being deleted during memory compression
- search rules being mixed with project status
- every agent inventing its own search method
- context retrieval becoming inconsistent
- repeated token use explaining search strategy

A triage agent, review agent, coding agent, or future tool can all reuse the same retrieval method.

## Recommended `context_retrieval.md` Structure

```markdown
# context_retrieval.md

## Purpose

Defines deterministic metadata search for this project.

## Search Priority

1. Match exact `id`, `module_id`, `submodule_id`, or `document_type`.
2. Match `layer`.
3. Match high-signal tags.
4. Follow explicit relationships:
   - parent
   - children
   - paired_yin
   - paired_yang
   - schemas
   - trace_map
   - related
   - depends_on
   - used_by
5. Read only matched files and necessary one-hop linked documents.
6. Build a compact context package.

## Excluded by Default

- archived documents
- deprecated documents
- backups
- unrelated layers
- unrelated modules
- generated outputs unless requested
- old drafts when a stable document exists

## Output

Create a temporary context package with:
- task
- search goal
- filters used
- files matched
- links followed
- relevant excerpts
- excluded files
- open questions
- search log
```

---

# 22. Optional Metadata Index

A project may generate a metadata index.

Possible files:

```text
metadata_index.json
metadata_index.md
context_index.md
```

The index can contain:

- document ID
- file path
- title
- document type
- layer
- module ID
- submodule ID
- status
- version
- tags
- parent
- children
- paired Yin/Yang
- related documents
- updated date

## Why Use an Index

Without an index, the agent or script may need to read every file header.

With an index, retrieval can start from one compact file.

This is useful for large projects.

## Example `metadata_index.json`

```json
[
  {
    "id": "core.settings.input.yin",
    "path": "docs/core/settings/input.yin.md",
    "title": "Settings Input — Yin Page",
    "document_type": "Yin Page",
    "layer": "Core",
    "module_id": "settings",
    "submodule_id": "settings.input",
    "status": "Review",
    "tags": ["settings", "input", "ui-state", "collapse"],
    "paired_yang": "core.settings.input.yang"
  },
  {
    "id": "core.settings.input.yang",
    "path": "docs/core/settings/input.yang.md",
    "title": "Settings Input — Yang Core Module",
    "document_type": "Yang Core Module",
    "layer": "Core",
    "module_id": "settings",
    "submodule_id": "settings.input",
    "status": "Review",
    "tags": ["settings", "input", "deterministic-core", "ui-state"],
    "paired_yin": "core.settings.input.yin"
  }
]
```

The metadata index is optional. It should be generated from documents where possible, not manually maintained forever.

---

# 23. Context Packages

A context package is the temporary output of deterministic retrieval.

It contains only what one agent needs for one task.

Possible file:

```text
context_package.md
```

A context package should include:

- task
- search goal
- matched documents
- relevant excerpts
- related documents followed
- search log
- exclusions
- open questions
- warnings
- handoff instructions if needed

It should not become permanent memory by default.

Confirmed results later move into `memory.md` or contracts if needed.

## Example Context Package

```markdown
# Context Package — Settings/Input Collapse Height

## Task

Prepare implementation context for Settings/Input collapse height bug.

## Search Goal

Find current documents related to Settings/Input, collapse state, UI state, and Yang contract behavior.

## Filters Used

- layer: Core
- module_id: settings
- submodule_id: settings.input
- tags: settings, input, collapse, ui-state
- status: Review or Stable

## Files Matched

- docs/core/settings/input.yin.md
- docs/core/settings/input.yang.md
- docs/state/memory.md#settings-input

## Links Followed

- paired_yang from Yin
- paired_yin from Yang
- parent module: settings
- related memory section: Settings/Input

## Relevant Context Summary

[Short summary of retrieved context.]

## Excluded

- Settings/Provider
- Dashboard
- archived drafts
- unrelated visual layout notes

## Search Log

Search performed using metadata fields before semantic search.
```

---

# 24. Search Log

Search logs make retrieval auditable.

A search log should record:

- task
- query or user request
- fields searched
- filters used
- files matched
- links followed
- files excluded
- why exclusions happened
- whether semantic search was used
- unresolved retrieval uncertainty

This prevents invisible context selection.

A later agent can see why the context package contains certain files and not others.

---

# 25. Retrieval Workflow

Recommended retrieval workflow:

1. Start with exact identifiers if available.
2. Search metadata fields before body text.
3. Match `id`, `module_id`, `submodule_id`, `document_type`, `layer`, and `tags`.
4. Filter out archived/deprecated documents unless requested.
5. Follow explicit links:
   - `paired_yin`
   - `paired_yang`
   - `parent`
   - `children`
   - `schemas`
   - `trace_map`
   - `related`
   - `depends_on`
   - `used_by`
6. Read only relevant documents.
7. Read predictable sections inside documents.
8. Create a context package.
9. Include a search log.
10. Use semantic search only if deterministic search is insufficient.

---

# 26. Example Search Commands

Plain text metadata allows simple search.

Examples with `ripgrep`:

```bash
rg "module_id: \"settings\"" docs/
rg "submodule_id: \"settings.input\"" docs/
rg "document_type: \"Yang Core Module\"" docs/
rg "layer: \"Core\"" docs/
rg "collapse" docs/
```

Search for tags:

```bash
rg "- ui-state" docs/
rg "- collapse" docs/
```

Search for paired documents:

```bash
rg "paired_yang: \"core.settings.input.yang\"" docs/
rg "paired_yin: \"core.settings.input.yin\"" docs/
```

Search excluding archives:

```bash
rg "submodule_id: \"settings.input\"" docs/ -g '!**/archive/**'
```

These commands are examples, not required tooling.

---

# 27. Example Python Metadata Search

A project may include a small Python script or prompt instruction for deterministic retrieval.

Example conceptual script:

```python
from pathlib import Path
import re
import yaml

ROOT = Path("docs")

def extract_frontmatter(text: str) -> dict:
    if not text.startswith("---"):
        return {}
    match = re.match(r"---\\n(.*?)\\n---", text, re.DOTALL)
    if not match:
        return {}
    return yaml.safe_load(match.group(1)) or {}

def load_docs(root: Path):
    for path in root.rglob("*.md"):
        text = path.read_text(encoding="utf-8")
        meta = extract_frontmatter(text)
        yield path, meta, text

def matches(meta: dict, filters: dict) -> bool:
    for key, expected in filters.items():
        value = meta.get(key)
        if isinstance(expected, list):
            values = value if isinstance(value, list) else [value]
            if not any(item in values for item in expected):
                return False
        else:
            if value != expected:
                return False
    return True

filters = {
    "layer": "Core",
    "module_id": "settings",
    "submodule_id": "settings.input",
}

for path, meta, text in load_docs(ROOT):
    if meta.get("status") in {"Archived", "Deprecated"}:
        continue
    if matches(meta, filters):
        print(path, meta.get("id"), meta.get("title"))
```

A real script should be adapted to the project's file layout and YAML conventions.

The important point is the retrieval method:

```text
read metadata
filter deterministically
follow explicit links
build context package
```

---

# 28. Optional Metadata Schemas

A project may define schemas for allowed metadata fields, document types, layers, statuses, and tags.

Schemas are useful when:

- the project is large
- many agents generate documents
- many contributors create pages
- automated validation is needed
- metadata drift becomes a problem
- registry/tooling integration is planned

Schemas may define:

- allowed `document_type` values
- allowed `layer` values
- allowed `status` values
- required fields per document type
- tag vocabulary
- ID pattern
- relationship fields
- date format
- version format

However, schemas create maintenance overhead.

For small projects, a simple written convention may be enough.

Recommended rule:

```text
Start with consistent frontmatter.
Add schemas when metadata drift becomes a real problem.
```

---

# 29. Document Status and Lifecycle

Every document should have a status.

Recommended statuses:

```text
Draft
Review
Stable
Deprecated
Archived
Superseded
```

| Status | Meaning |
|---|---|
| `Draft` | Work in progress, not authoritative |
| `Review` | Ready for review, not final |
| `Stable` | Current source for normal use |
| `Deprecated` | Still present but should not be used for new work |
| `Archived` | Historical, excluded by default |
| `Superseded` | Replaced by another document |

Retrieval should prefer `Stable` and `Review` documents.

Retrieval should exclude `Deprecated`, `Archived`, and `Superseded` documents by default unless the user asks for history.

---

# 30. Metadata Maintenance Rules

Metadata must be maintained.

Rules:

- update `updated` after meaningful changes
- update status when document lifecycle changes
- update paired links when Yin/Yang files move
- update parent/child links after modularization changes
- update source block IDs after regeneration
- update `superseded_by` when replacing a document
- remove stale links
- do not keep broken IDs
- do not preserve old metadata just because it existed
- do not use private secrets in metadata

Metadata is not useful if it becomes stale.

---

# 31. Integration with Triage and Maintenance

Triage can use the graph to prepare Agent-2 handoffs.

Example:

```text
User reports Settings/Input collapse bug.
Agent 1 searches:
- module_id: settings
- submodule_id: settings.input
- tags: collapse, ui-state
- document_type: Yin Page, Yang Core Module
```

Agent 1 retrieves:

- relevant Yin
- relevant Yang
- relevant memory entry
- related handoff history
- status of documents

Then Agent 1 produces a scoped Agent-2 handoff.

This prevents Agent 2 from inspecting unrelated Settings categories or broad repository areas.

---

# 32. Integration with State Management

State Management and the Metadata Graph reinforce each other.

`memory.md` can reference metadata IDs.

`plan.md` can name the active module/submodule.

Handoffs can declare their target metadata.

Context packages can log which IDs were retrieved.

Example `plan.md` excerpt:

```markdown
## Current Focus

Fix Settings/Input collapse height issue.

Metadata:
- module_id: settings
- submodule_id: settings.input
- tags: settings, input, collapse, ui-state
```

Example `memory.md` section:

```markdown
## Settings / Input

Related metadata:
- module_id: settings
- submodule_id: settings.input
- related_yin: core.settings.input.yin
- related_yang: core.settings.input.yang
```

This lets state files participate in deterministic retrieval without becoming the graph itself.

---

# 33. Integration with Prompt Library and Future Prism Registry

The Metadata Graph can support Prompt Library and future Prism Registry workflows.

Possible uses:

- locate model references
- locate platform references
- locate prompt templates
- locate document templates
- locate examples
- locate task-mode profiles
- locate renderer rules
- locate project-specific constraints

Example metadata:

```yaml
---
id: "reference.model.claude"
title: "Claude Prompting Reference"
document_type: "Model Reference"
layer: "Framework"
status: "Stable"
tags:
  - model-reference
  - claude
  - prompting
---
```

Future Prism workflows may use metadata to resolve:

- target model
- target platform
- task mode
- output type
- prompt shape
- reference profile
- rendering rules

Until that exists, metadata can still help users manually locate the correct reference files.

---

# 34. Integration with Documentation Tools

The framework is tool-agnostic.

A valid implementation can use:

- plain Markdown folders
- Git repositories
- Anytype
- Obsidian
- Notion-style systems
- local folders
- static documentation sites
- custom tools
- future Allzy tooling

The required properties are:

- structured documents
- stable identifiers
- metadata fields
- linkable relationships
- predictable retrieval
- exportable context

The tool is replaceable.

The graph principles remain.

---


## Operational Prompt Boundaries

Use the correct prompt for the correct metadata/retrieval task.

| Need | Use |
|---|---|
| Create/check workspace context structure | `workspace_context_initialization_prompt.md` |
| Maintain living state files | `workspace_state_maintenance_prompt.md` |
| Add/update metadata/frontmatter on existing documents | `document_metadata_enrichment_prompt.md` |
| Retrieve and package relevant context | `context_retrieval_builder_prompt.md` |
| Generate a Yin/Yang specification prompt | `yin_yang_prompt_generator.md` |
| Diagnose a bug and prepare Agent-2 handoff | Triage prompt family |

Do not use Document Metadata Enrichment to convert documents into Yin/Yang.

Do not use Context Retrieval Builder to rewrite documents.

Do not use Workspace State Maintenance to rewrite metadata conventions.

Do not use broad semantic retrieval when deterministic metadata is available and sufficient.


# 35. Anti-Patterns

## Metadata Theater

Documents contain metadata headers, but the fields are inaccurate, stale, or meaningless.

Symptoms:

- every document has the same tags
- `related` contains many random links
- status is never updated
- IDs change casually
- paired Yin/Yang links are broken
- archived docs are still retrieved

Fix:

- use fewer fields
- keep them accurate
- validate periodically
- remove stale metadata

## Tag Flooding

A document has too many tags.

Symptoms:

- tags no longer filter meaningfully
- every search returns too much
- high-signal tags are buried
- tag vocabulary becomes inconsistent

Fix:

- use fewer, more precise tags
- rely on `layer`, `document_type`, `module_id`, and `submodule_id` fields instead of tags for everything

## Semantic Guessing First

The agent starts with broad semantic search even when metadata exists.

Symptoms:

- wrong files selected
- important paired docs missed
- old docs retrieved
- unrelated but similar text included

Fix:

- search metadata first
- use semantic search only as helper

## Broken Relationship Graph

Metadata exists, but links are not maintained.

Symptoms:

- `paired_yang` points to old document
- `parent` is missing
- `children` outdated
- source block ID lost
- superseded docs still active

Fix:

- maintain relationships during document updates
- run periodic metadata review

## Tool Lock-In

The project assumes the graph only works in one app.

Symptoms:

- export breaks structure
- AI cannot use the graph outside the tool
- references depend on UI-only behavior

Fix:

- preserve plain-text metadata
- support Markdown export
- keep IDs and links tool-independent

## Permanent Context Package

A temporary context package becomes a long-term catch-all file.

Symptoms:

- context_package.md grows forever
- old search logs remain active
- stale excerpts are reused
- memory and retrieval blur

Fix:

- treat context packages as temporary task artifacts
- move confirmed facts to memory
- discard or archive the package

## MCP Overexposure

A tool connector gives an AI agent broader access than needed.

Symptoms:

- agent can access private notes unrelated to task
- sensitive business knowledge is exposed
- audit boundary unclear
- too much graph data enters context

Fix:

- prefer export-first for sensitive work
- limit connector access
- give only selected context packages where possible

---

# 36. Quality Checklist

## Document Metadata Checklist

- [ ] Document has stable `id`.
- [ ] Document has clear `title`.
- [ ] `document_type` is specific.
- [ ] `layer` is accurate.
- [ ] `status` is current.
- [ ] `version` is present where useful.
- [ ] `updated` date is current.
- [ ] Tags are concise and useful.
- [ ] Parent/child links are accurate.
- [ ] Paired Yin/Yang links are accurate where applicable.
- [ ] Related schemas are linked where applicable.
- [ ] Source block ID is preserved where applicable.
- [ ] Deprecated/archived documents are marked correctly.
- [ ] No secrets appear in metadata.

## Retrieval Checklist

- [ ] Search starts with exact IDs or metadata fields.
- [ ] Tags are used after stronger fields.
- [ ] Deprecated/archived documents are excluded by default.
- [ ] Paired Yin/Yang links are followed.
- [ ] Parent/child links are followed only as needed.
- [ ] Related documents are not blindly included.
- [ ] Context package is compact.
- [ ] Search log is recorded.
- [ ] Semantic search is used only as helper when needed.

## Tooling Checklist

- [ ] Documentation can be exported or read as structured text.
- [ ] Metadata survives export.
- [ ] Links or IDs remain usable outside the tool.
- [ ] Sensitive data is not exposed through broad connectors.
- [ ] Search scripts or retrieval instructions are available.
- [ ] `context_retrieval.md` exists for large projects.
- [ ] Optional metadata index is generated if project size requires it.


---


# 37. Context Retrieval Builder

The Context Retrieval Builder is the operational workflow for selecting and packaging relevant project context.

Operational prompt:

```text
context_retrieval_builder_prompt.md
```

It searches existing metadata-tagged documents and builds an output artifact based on user intent.

It does not:

- implement code
- fix bugs
- rewrite source documents
- create Yin/Yang documents
- update `plan.md` or `memory.md`
- clean state files
- replace Workspace Context Initialization
- replace Document Metadata Enrichment

## Two-Phase Workflow

The builder performs two phases:

```text
Mode 1 = Intake / Search Planning
Mode 2 = Retrieval / Output Building
```

Mode 1 clarifies:

- what should be searched
- why it is needed
- what output should be produced
- how deep retrieval should go
- who the output is for

Mode 2 uses deterministic retrieval rules, metadata, tags, IDs, document structure, memory excerpts, skills indexes, and related files to build the requested output.

## Output Modes

The builder may produce different output artifacts:

```text
summary
deep_brief
agent_context_package
patch_handoff_context
document_source_pack
review_context
custom
```

This matters because context retrieval is not only for Agent-2 implementation.

It may also support:

- documentation writing
- prompt creation
- reviews
- audits
- research
- planning
- source gathering
- human understanding
- handoff preparation

## Retrieval Initialization Check

Before searching, the builder must check whether deterministic retrieval is available.

It should look for:

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

If retrieval is not initialized, the builder must not pretend deterministic retrieval is available.

If deterministic retrieval is required but missing, the correct response is:

```text
Retrieval is not initialized yet. Run Workspace Context Initialization first, or provide `context_retrieval.md` and metadata conventions.
```

Temporary bootstrap retrieval may be allowed only when explicitly enabled, and it must be labeled as temporary.

## Retrieval Signals

The builder may use:

- `id`
- `title`
- `document_type`
- `layer`
- `module_id`
- `submodule_id`
- `status`
- `tags`
- `aliases`
- `related`
- `references`
- `parent`
- `children`
- `paired_yin`
- `paired_yang`
- `source_block_id`
- `generated_from`
- `retrieval_description`
- file path
- folder structure
- memory sections
- skills index
- Search Logs where relevant

## Derived Retrieval Keys

If the user describes a topic in natural language, the builder may derive possible retrieval keys:

```text
topic
possible_module_ids
possible_submodule_ids
likely_layers
likely_document_types
derived_tags
aliases
known/likely folders
confidence
```

Derived keys are not confirmed truth.

They must be labeled as derived.

## Builder Output Requirements

A good retrieval output should include:

- selected sources
- why they were selected
- what was excluded
- source status
- confidence level
- open questions
- retrieval uncertainty
- Search Log when enabled

The Search Log is not memory.

Confirmed lasting facts may be moved into `memory.md` only through the correct state workflow.


## Metadata Index Generation

A metadata index may be generated from frontmatter.

Operational prompt name:

```text
metadata_index_generation_prompt.md
```

This focused prompt may be created later as a single-artifact prompt.

Until then, metadata indexing can be handled by Workspace Context Initialization, Context Retrieval Builder setup, or custom scripts.

The index should be derived from document metadata where possible.

It should not become a separate manually maintained truth that silently diverges from source documents.

Recommended index fields:

- document ID
- path
- title
- document type
- layer
- module ID
- submodule ID
- status
- tags
- aliases
- parent/child links
- paired Yin/Yang links
- related/referenced documents
- updated date
- retrieval description


---

# Metadata, Config, and Retrieval Conventions Document

A later dedicated documentation file should define the complete metadata/config conventions.

Recommended name:

```text
07_Metadata_Config_and_Retrieval_Conventions.md
```

Its role should be to explain:

- why config blocks exist
- difference between prompt config and document frontmatter
- standard metadata fields
- tags
- IDs
- aliases
- related/references
- module IDs and submodule IDs
- status
- `retrieval_description`
- Search Logs
- metadata indexes
- context packages
- how metadata supports deterministic retrieval
- how Document Metadata Enrichment uses the schema
- how Context Retrieval Builder uses the schema
- how Workspace Context Initialization creates starter structures

This document should be a conventions/reference document, not a prompt.

It should later support reusable templates such as:

```text
metadata_frontmatter_template.md
prompt_config_block_template.md
context_package_template.md
search_log_template.md
metadata_index_template.md
```



---

## Website-Ready Summary

The Deterministic Metadata Graph is the Allzy Framework's method for making documentation reliably retrievable by humans, scripts, and AI agents.

Instead of relying only on semantic search or vector similarity, documents declare what they are through stable IDs, metadata, tags, layers, document types, links, backlinks, and predictable structures.

This makes it possible to find the right Yin page, Yang contract, module, submodule, schema, memory section, or handoff without guessing.

The graph can live in plain Markdown, Git folders, Anytype, Obsidian, Notion-style systems, or future Allzy tooling. Anytype is one practical example because it supports typed pages, collections, tags, backlinks, graph views, and exportable structures, but the framework itself is tool-agnostic.

The core rule is:

```text
Use deterministic metadata first.
Use semantic search as a helper.
Do not make the AI guess the project graph.
```

The result is faster context preparation, lower token usage, clearer traceability, and safer AI-assisted implementation.


---