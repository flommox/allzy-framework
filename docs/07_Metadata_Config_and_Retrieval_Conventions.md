---
id: "allzy.framework.docs.07.metadata-config-retrieval-conventions"
title: "07 — Metadata, Config, and Retrieval Conventions"
artifact_type: "Framework Documentation"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - metadata
  - config
  - retrieval
---

# 07 — Metadata, Config, and Retrieval Conventions

## Status

This document defines the metadata, config, frontmatter, retrieval, Search Log, context package, metadata index, and related conventions used by the Allzy Framework.

It is a conventions/reference document.

It is not a prompt.

It is not a template.

It is not an implementation script.

It explains how framework documents, operational prompts, workspace context files, metadata-enriched documents, retrieval workflows, and AI handoffs should describe, configure, search, select, and package context.

---

# 1. Purpose

The Allzy Framework uses structured documentation to reduce AI guessing.

Metadata and config conventions are the infrastructure that make this possible.

They allow humans, scripts, documentation systems, and AI agents to answer questions such as:

- What is this document?
- Which layer does it belong to?
- Which module or submodule does it describe?
- Is it current?
- Is it a template, prompt, example, source document, Yin page, or Yang contract?
- Which documents are related?
- Which Yin and Yang documents are paired?
- Which block generated this document?
- Which documents should be retrieved for a task?
- Which documents should be excluded?
- Which prompt mode should run?
- Which config values were selected by the user?
- Which output artifact should be created?
- Which context was used and why?

The goal is:

```text
Make context explicit, searchable, linkable, auditable, and reusable.
```

The goal is not:

```text
Add metadata for decoration.
```

Metadata must help retrieval, indexing, linking, validation, review, or AI execution.

---

# 2. Core Principle

The central rule:

```text
Document frontmatter describes artifacts.
Prompt config controls execution.
```

This distinction must be preserved throughout the framework.

## 2.1 Document Frontmatter

Document frontmatter is metadata at the top of a document.

It describes the document.

It helps systems and agents classify, retrieve, link, validate, and reuse the document.

Document frontmatter answers:

- What is this artifact?
- What is its role?
- What layer does it belong to?
- What topic/module/submodule does it cover?
- What status does it have?
- What should retrieve it?
- What should not retrieve it?
- What is it related to?
- What generated it?
- What source block or source document does it come from?
- Is it paired with another document?

## 2.2 Prompt Config Block

A prompt config block is a YAML-style configuration area inside an operational prompt.

It controls how the prompt should run.

Prompt config answers:

- Which mode should the prompt use?
- Which profile is selected?
- Which output should be created?
- Which files may be created or updated?
- Which references are available?
- Which retrieval depth is requested?
- Which target model or platform is selected?
- Is fallback allowed?
- Should Search Logs be generated?
- Should skills be included?
- Should metadata indexes be used?

## 2.3 Why the Distinction Matters

If prompt config is treated as permanent document truth, the project state becomes polluted with execution choices.

If document frontmatter is treated as execution config, prompts may silently perform the wrong action.

Correct separation:

| Structure | Belongs to | Purpose |
|---|---|---|
| Document frontmatter | Documents, templates, examples, source docs, context files | Describe an artifact |
| Prompt config block | Operational prompts | Control an execution |
| Search Log | Retrieval output / context package | Record what was searched and selected |
| Metadata index | Generated lookup file | Accelerate deterministic retrieval |
| Context package | Temporary task context | Carry selected context for one task |
| `memory.md` | Workspace state | Preserve confirmed current project truth |
| `skills/` | Workspace helper rules | Preserve reusable objective helper rules |

---

# 3. Where These Conventions Apply

These conventions apply to:

- framework docs
- document templates
- prompt templates
- examples
- Yin documents
- Yang documents
- combined Yin/Yang documents
- Master Documents
- Master Document Compact files
- context files
- metadata indexes
- Search Logs
- context packages
- skills
- prompt libraries
- reference packages
- imported documents
- old source documents
- research notes
- architecture notes
- product notes
- documentation pages
- AI handoff artifacts

They do not require one specific storage tool.

They can be used in:

- plain Markdown repositories
- local folders
- GitHub repositories
- Anytype
- Obsidian
- Notion-style systems
- static documentation sites
- custom Allzy tooling
- future Prism / Pösen / Splice workflows

The method requires consistent metadata.

The storage tool is replaceable.

---

# 4. Minimum Metadata Block

Every important framework artifact should have at least a small metadata block.

Minimum recommended block:

```yaml
---
id: ""
title: ""
document_type: ""
document_role: ""
layer: ""
status: "Draft"
version: "0.1.0"
metadata_version: "1.0.0"
created: ""
updated: ""
language: ""
technical_identifiers_language: "English"
tags: []
aliases: []
summary: ""
retrieval_description: ""
---
```

This minimum is enough to:

- identify the document
- classify the document
- search by title and tags
- filter by layer and document type
- check status
- support basic retrieval

Use the full metadata block when the document is important, long-lived, generated, related to implementation, related to Yin/Yang, or part of deterministic retrieval.

---

# 5. Full Universal Metadata Shape

Use the following shape for metadata-rich documents, imported documents, framework documents, long-lived project docs, context-enabled docs, and documents prepared for deterministic retrieval.

Keep fields even if some values are empty when the document is meant to be processed by AI or indexing tools.

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

---

# 6. Metadata Field Groups

## 6.1 Identity Fields

Identity fields define the document as an artifact.

```yaml
id: ""
title: ""
description: ""
document_type: ""
document_role: ""
```

### `id`

`id` should be stable.

Use lowercase.

Prefer dot-style or kebab-style.

Examples:

```text
framework.metadata-config-retrieval-conventions
docs.settings.input.yin
core.settings.input.yang
prompt.yin-yang-generator
example.user-login
context.memory
workspace.context-retrieval
```

Avoid:

```text
Document 1
new file
important stuff
latest version
final final
```

A good ID is:

- stable
- searchable
- not too long
- not dependent on a local file path
- useful in references
- unique enough inside the project

### `title`

`title` is the human-readable title.

Example:

```yaml
title: "Settings Input — Yang Core Module"
```

The title may change more easily than the ID.

### `description`

`description` gives a short human-readable description.

It should not become a long summary.

### `document_type`

`document_type` classifies the artifact.

Examples:

```text
Framework Documentation
Master Document
Master Document Compact
Yin Page
Compact Yin Page
Yang Core Module
Yin/Yang Document
Yin/Yang Compact
Prompt
Template
Example
Reference
State File
Context Package
Search Log
Metadata Index
Skill
Source Document
Research Note
Architecture Note
Product Note
Decision Record
```

### `document_role`

`document_role` describes what the document does in the workflow.

Examples:

```text
Conventions Reference
Operational Prompt
Reusable Template
Filled Example
Source Context
Implementation Contract
Human Intent Document
Retrieval Method
Workspace Memory
Current Task Plan
Generated Lookup Index
Reusable Agent Helper
```

---

## 6.2 Layer Fields

```yaml
layer: ""
```

Valid framework layers:

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

Use `Framework` for framework docs, prompts, templates, and conventions.

Use `Workspace Context` for files such as:

```text
plan.md
memory.md
context_retrieval.md
context_package.md
Search Log
metadata_index
skills/
```

Use product-specific layers such as `System` or `Core` for implementation documents.

Do not use tags as a replacement for layer.

Incorrect:

```yaml
layer: ""
tags:
  - core
```

Correct:

```yaml
layer: "Core"
tags:
  - settings
  - input
```

---

## 6.3 Status and Version Fields

```yaml
status: "Active"
version: "0.1.0"
metadata_version: "1.0.0"
created: ""
updated: ""
last_reviewed: ""
review_status: ""
review_notes: ""
```

Recommended status values:

```text
Draft
Review
Active
Stable
Deprecated
Archived
Superseded
```

Use `Stable` for accepted framework docs.

Use `Active` for living workspace state.

Use `Draft` for early working documents.

Use `Deprecated`, `Archived`, or `Superseded` to exclude old documents from normal retrieval.

`metadata_version` tracks the metadata schema version, not the document content version.

`version` tracks the document itself.

## 6.4 Date Policy

Do not invent dates.

Preserve existing dates.

Infer dates only if clearly present.

If actively updating metadata and the current date is known, `updated` may be set according to config.

Leave `created` empty if unknown.

---

## 6.5 Language Fields

```yaml
language: ""
primary_language: ""
secondary_languages: []
technical_identifiers_language: "English"
```

Framework rule:

```text
Technical identifiers should remain English unless explicitly overridden.
```

Human-facing documents may use configured languages.

Examples:

- Yin may be German, English, Spanish, or another configured language.
- Yang is normally English.
- Technical identifiers remain English.
- Prompt configs use English identifiers.

---

## 6.6 Tags, Aliases, and Keywords

```yaml
tags: []
aliases: []
keywords: []
```

### Tags

Tags should be specific and useful.

Good tags:

```text
settings
input
collapse
ui-state
auth
login
privacy
audit
retrieval
frontmatter
workspace-context
functional-core
triage
metadata-index
```

Bad tags:

```text
misc
stuff
important
thing
general
random
doc
file
```

Do not use tags as a replacement for structure.

If something is a layer, use `layer`.

If something is a module, use `module_id`.

If something is a document type, use `document_type`.

Tags are retrieval helpers, not the only metadata system.

### Aliases

Aliases help retrieve the document when people use different names.

Examples:

```yaml
aliases:
  - "Yin Yang Generator"
  - "Yin/Yang Prompt Generator"
  - "Specification Prompt Generator"
```

Use aliases for:

- common spelling variations
- alternative names
- old working names when still useful for search
- user-facing names vs. technical names

Do not use aliases to preserve incorrect terminology as official naming.

### Keywords

Keywords are lower-priority search helpers.

Use them for words likely to appear in user queries.

---

# 7. Source Fields

Source fields explain where the document came from.

```yaml
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
```

Use these fields when documents are generated from:

- Genesis output
- Splice blocks
- module blocks
- submodule blocks
- source documents
- imported notes
- old Markdown files
- examples
- templates
- research material

## 7.1 `source_block_id`

Use `source_block_id` when a document was generated from a specific block.

Example:

```yaml
source_block_id: "block-023"
```

This is especially useful for Splice workflows.

## 7.2 `generated_from`

Use `generated_from` to reference the source or workflow that created the document.

Example:

```yaml
generated_from: "master-document-v1.md"
```

or:

```yaml
generated_from: "splice-block-023"
```

## 7.3 Source Rules

Do not invent source IDs.

Do not invent file paths.

If the source is unknown, leave the field empty or mark it in:

```yaml
validation:
  uncertain_fields:
    - "source.generated_from"
```

---

# 8. Classification Fields

Classification fields describe sensitivity, audience, lifecycle, and stability.

```yaml
classification:
  confidentiality: ""
  sensitivity: ""
  audience: []
  lifecycle_stage: ""
  priority: ""
  stability: ""
```

Recommended confidentiality values:

```text
public
internal
private
restricted
secret
```

Recommended sensitivity values:

```text
none
low
medium
high
unknown
```

Use sensitivity and confidentiality for retrieval and sharing decisions.

High-sensitivity documents should not be casually included in AI context packages.

Secrets should never be included.

---

# 9. Scope Fields

Scope fields connect a document to a project, product, domain, module, or feature.

```yaml
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
```

Use these instead of encoding everything in tags.

Examples:

```yaml
scope:
  project: "keepit"
  product: "private-planner"
  system: "workspace-context"
  domain: "state-management"
  module_id: "settings"
  submodule_id: "settings.input"
  component_id: "input-collapse-panel"
  feature_id: "fixed-panel-height"
  topic: "Input collapse behavior"
  subtopic: "Height stability"
```

## 9.1 `module_id`

`module_id` should identify a coherent module.

Examples:

```text
settings
auth
notifications
billing
search
workspace-context
metadata
triage
```

## 9.2 `submodule_id`

`submodule_id` should identify a smaller implementable unit.

Examples:

```text
settings.input
auth.login
notifications.email
workspace-context.memory
metadata.frontmatter
triage.fast
```

## 9.3 Scope Rules

Use scope fields when deterministic retrieval needs to select documents for one area.

Do not rely only on folder paths.

Do not rely only on semantic search.

---

# 10. Structure and Relationship Fields

Relationship fields define graph structure.

```yaml
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
```

## 10.1 Parent / Children

Use `parent` and `children` for hierarchy.

Examples:

```yaml
parent: "core.settings"
children:
  - "core.settings.input"
  - "core.settings.provider"
```

## 10.2 Related

Use `related` for loose relationships.

Prefer specific fields before using `related`.

## 10.3 References

Use `references` when the document directly cites or depends on another document as source material.

## 10.4 Depends On / Used By

Use `depends_on` for upstream dependencies.

Use `used_by` for downstream consumers.

## 10.5 Supersedes / Superseded By

Use these for document replacement.

If a document is superseded, its status should usually be:

```yaml
status: "Superseded"
```

and it should not be retrieved by default.

## 10.6 Conflicts With

Use `conflicts_with` when documents disagree.

Do not silently resolve conflicts if they require human judgment.

---

# 11. Yin/Yang Compatibility Metadata

Yin/Yang metadata links human intent and technical execution contracts.

```yaml
yin_yang:
  is_yin_yang_document: false
  yin_document: ""
  yang_document: ""
  paired_yin: ""
  paired_yang: ""
  can_be_converted_to_yin_yang: ""
  recommended_conversion_target: ""
  conversion_notes: ""
```

## 11.1 Existing Yin/Yang Documents

For a Yin document:

```yaml
yin_yang:
  is_yin_yang_document: true
  yang_document: "core.settings.input.yang"
  paired_yang: "core.settings.input.yang"
```

For a Yang document:

```yaml
yin_yang:
  is_yin_yang_document: true
  yin_document: "core.settings.input.yin"
  paired_yin: "core.settings.input.yin"
```

For a combined Yin/Yang document:

```yaml
yin_yang:
  is_yin_yang_document: true
  paired_yin: ""
  paired_yang: ""
```

## 11.2 Documents That May Be Converted Later

For a source document:

```yaml
yin_yang:
  is_yin_yang_document: false
  can_be_converted_to_yin_yang: "yes"
  recommended_conversion_target: "yin_yang"
  conversion_notes: "Source contains both product intent and partial execution rules."
```

## 11.3 Critical Boundary

Document Metadata Enrichment is not Yin/Yang conversion.

It may mark that a document can later be converted.

It must not generate the Yin/Yang document.

Yin/Yang conversion requires:

- source context
- target artifact selection
- required template content
- target model/platform handling
- Open Questions
- Contract Gaps
- human review

Use the Yin/Yang Prompt Generator workflow for that.

---

# 12. Retrieval Fields

Retrieval fields define how a document participates in deterministic retrieval.

```yaml
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
```

## 12.1 `retrieval_ready`

Use:

```yaml
retrieval_ready: true
```

when the document has enough metadata to be included in deterministic retrieval.

Use:

```yaml
retrieval_ready: false
```

when the document is incomplete, unsafe, obsolete, or not intended for retrieval.

## 12.2 `retrieval_confidence`

Recommended values:

```text
high
medium
low
unknown
```

Use `low` or `unknown` when metadata was inferred from weak context.

## 12.3 `retrieval_priority`

Recommended values:

```text
primary
normal
supporting
low
exclude
```

Use `primary` for authoritative source-of-truth documents.

Use `supporting` for examples or background.

Use `exclude` for documents that should not appear in normal retrieval.

## 12.4 `chunking_hint`

Use `chunking_hint` for long documents.

Examples:

```yaml
chunking_hint: "section_based"
```

or:

```yaml
chunking_hint: "frontmatter_plus_headings"
```

## 12.5 `preferred_retrieval_keys`

Use this for explicit keys.

Example:

```yaml
preferred_retrieval_keys:
  - "settings.input"
  - "input-collapse"
  - "fixed-panel-height"
```

## 12.6 `excluded_from_retrieval`

Use:

```yaml
excluded_from_retrieval: true
```

when the document should not be retrieved by default.

Always include an explanation:

```yaml
exclusion_reason: "Superseded by core.settings.input.yang v1.2.0"
```

---

# 13. Validation Fields

Validation fields make uncertainty visible.

```yaml
validation:
  metadata_inferred: true
  uncertain_fields: []
  missing_context: []
  needs_human_review: false
  validation_notes: []
```

Use these fields when metadata was inferred.

Example:

```yaml
validation:
  metadata_inferred: true
  uncertain_fields:
    - "scope.module_id"
    - "structure.parent"
  missing_context:
    - "No parent module document provided."
  needs_human_review: true
  validation_notes:
    - "Module ID inferred from heading and folder path."
```

Rule:

```text
Mark uncertainty instead of inventing certainty.
```

---

# 14. Output Fields

Output fields support filename and folder decisions.

```yaml
output:
  preferred_filename: ""
  filename_source: ""
  suggested_folder: ""
```

Example:

```yaml
output:
  preferred_filename: "settings_input_yang.md"
  filename_source: "derived_from_module_id"
  suggested_folder: "docs/contracts/settings/"
```

Do not silently rename source files without clear rules.

---

# 15. Prompt Config Block Conventions

Prompt config blocks control operational prompts.

They should be:

- explicit
- predictable
- YAML-style
- near the top of the prompt
- easy for a website or prompt builder to fill
- editable by humans
- safe when partially empty

## 15.1 Config-First Principle

Every major operational prompt should use a config-first model.

Rule:

```text
If config is filled, execute according to config.
If config is empty or incomplete, switch to Assistant Mode.
```

Manual config and website-generated config must be treated the same.

Do not ask redundant questions when config values are already provided.

## 15.2 Standard Prompt Modes

Operational prompts may support these modes:

| Mode | Meaning |
|---|---|
| Preconfigured Mode | Config is filled by website, prompt builder, or user |
| Manual Config Mode | User manually edits config block |
| Assistant Mode | Required config is missing, assistant asks targeted questions |
| Universal Fallback Mode | Missing references/options, task can proceed as labeled fallback |
| Optional Clarification Mode | Non-critical details missing, prompt proceeds and lists optional improvements |

## 15.3 Assistant Mode

Assistant Mode should ask targeted questions.

It should not dump long questionnaires unless the workflow truly requires them.

Preferred behavior:

```text
Ask one necessary question.
Wait.
Continue.
```

## 15.4 Universal Fallback Mode

Use Universal Fallback Mode when:

- target model is missing
- target platform is missing
- model reference is missing
- platform reference is missing
- template/reference context is incomplete
- optimized output is impossible but safe generic output can proceed

Fallback output must be labeled.

Do not claim model/platform optimization without reference content.

## 15.5 Optional Clarification Mode

Use Optional Clarification Mode when the task can proceed but would improve with more information.

Example block:

```markdown
## Clarifications That Would Improve Specialization

- Which target platform will Agent 2 use?
- Is there a model-specific prompting reference?
- Should the output be optimized for a specific coding agent?
```

Do not block for non-critical details.

---

# 16. Workspace Context Config Conventions

Workspace Context Initialization uses config to create or inspect workspace context artifacts.

Core config concepts:

```yaml
workspace_context_config:
  mode: "" # assistant | preconfigured | inspect_only
  setup_profile: "" # inspect_only | minimal | standard | full | custom

  context_root: "" # e.g. context/ or .ai/context/
  allow_file_creation: null
  allow_file_updates: null
  allow_placeholder_repair: null

  create_plan_md: null
  create_memory_md: null
  create_context_retrieval_md: null
  create_context_package_template: null
  create_search_log_template: null
  create_metadata_index_template: null
  metadata_index_format: "" # none | markdown | json | both

  create_skills_structure: null
  skills_format: "agentskills.io"
  allow_skill_candidates: true
  allow_auto_create_approved_skills: false
  require_skill_review_before_activation: true
  allow_external_skill_lookup: false
  allow_skill_scripts: false
```

## 16.1 Setup Profiles

| Profile | Creates/checks |
|---|---|
| `inspect_only` | Inspect existing setup only |
| `minimal` | `plan.md` + `memory.md` |
| `standard` | `plan.md` + `memory.md` + `context_retrieval.md` |
| `full` | Standard + context package template + Search Log template + optional metadata index + optional skills |
| `custom` | Explicit config choices |

Use `standard` as baseline.

Use `full` for larger projects, Yin/Yang workflows, Triage-heavy projects, and multi-agent work.

## 16.2 Target Workspace Boundary

Workspace config applies to the target implementation workspace.

It does not configure the Framework repository itself.

Do not confuse:

```text
framework repo
```

with:

```text
target implementation workspace
```

---

# 17. Search Log Convention

A Search Log records how context was selected.

It is an audit trail.

It is not memory.

It should include:

- task or query
- retrieval goal
- selected output mode
- search depth
- config used
- metadata filters used
- search keys used
- documents matched
- memory sections matched
- skills index entries used
- links followed
- documents excluded
- reasons for exclusion
- uncertainty
- confidence
- open questions

Example:

```markdown
## Search Log

### Retrieval Goal

Prepare context for a Settings/Input collapse-height bugfix handoff.

### Search Inputs

- Topic: Settings Input collapse height
- Known module_id: settings
- Known submodule_id: settings.input
- Known tags: collapse, ui-state

### Retrieval Signals Used

- `module_id=settings`
- `submodule_id=settings.input`
- `tags=collapse`
- `paired_yang`
- `memory.md > Settings / Input`

### Sources Selected

| Source | Reason | Status |
|---|---|---|
| `core.settings.input.yin` | Product/intent context | Stable |
| `core.settings.input.yang` | Technical contract | Stable |
| `memory.md > Settings / Input` | Recent confirmed behavior | Active |

### Sources Excluded

| Source | Reason |
|---|---|
| `settings.provider.*` | Different settings category |
| `dashboard.*` | Different UI area |

### Confidence

High.

### Open Questions

- None blocking.
```

## 17.1 Search Log Rules

Search Log must not become permanent memory.

Confirmed lasting facts should move to `memory.md` through the state workflow.

Search Log can be included in:

- context package
- Triage handoff
- review report
- documentation source pack
- retrieval builder output

---

# 18. Context Package Convention

A context package is temporary selected context for one task.

It may be created by:

- Context Retrieval Builder
- Triage
- manual preparation
- a future context package generation prompt

It is not a permanent state file.

It is not `memory.md`.

It is not a replacement for `context_retrieval.md`.

It should include:

- task
- goal
- selected sources
- relevant excerpts
- summary of selected context
- Search Log
- source status
- exclusions
- uncertainty
- open questions
- handoff notes
- intended audience

Example structure:

```markdown
# Context Package — [Task]

## Purpose

[Why this package exists.]

## Target Audience

[Human / Agent 2 / reviewer / documentation agent.]

## Task

[Task description.]

## Selected Sources

| Source | Type | Why included | Status |
|---|---|---|---|

## Relevant Context Summary

[Compact summary.]

## Direct Excerpts

[Only if needed.]

## Search Log

[How sources were found.]

## Exclusions

[What was intentionally excluded and why.]

## Open Questions

[Remaining uncertainties.]

## Handoff Notes

[How the next agent should use this package.]
```

## 18.1 Context Package Rules

Use the smallest safe context package.

Prefer summaries over long excerpts when possible.

Include direct excerpts only when needed.

Do not include secrets.

Do not include full unrelated documents.

Do not treat the context package as memory.

---

# 19. Metadata Index Convention

A metadata index is a generated lookup index.

Possible files:

```text
metadata_index.md
metadata_index.json
context_index.md
```

It should be derived from document frontmatter where possible.

It should not become a manually maintained truth that diverges from source documents.

## 19.1 Recommended Index Fields

```yaml
id: ""
path: ""
title: ""
document_type: ""
document_role: ""
layer: ""
status: ""
version: ""
updated: ""
tags: []
aliases: []
module_id: ""
submodule_id: ""
parent: ""
children: []
paired_yin: ""
paired_yang: ""
related: []
references: []
retrieval_description: ""
retrieval_ready: true
retrieval_priority: ""
```

## 19.2 Markdown Index Example

```markdown
# Metadata Index

| ID | Path | Type | Layer | Status | Tags |
|---|---|---|---|---|---|
| `core.settings.input.yang` | `docs/contracts/settings/input_yang.md` | Yang Core Module | Core | Stable | settings, input |
```

## 19.3 JSON Index Example

```json
[
  {
    "id": "core.settings.input.yang",
    "path": "docs/contracts/settings/input_yang.md",
    "document_type": "Yang Core Module",
    "layer": "Core",
    "status": "Stable",
    "tags": ["settings", "input"],
    "paired_yin": "core.settings.input.yin"
  }
]
```

---

# 20. Skills Metadata and Index Convention

Workspace skills are optional reusable helper rules for AI agents.

They belong in:

```text
context/skills/
```

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

## 20.1 Source of Truth

Each individual `SKILL.md` is the source of truth.

```text
context/skills/**/SKILL.md
```

`skills_bundle.md` is generated.

It is only a helper for:

- maintenance
- export
- optimization
- compact loading

It must not become the source of truth.

## 20.2 What Skills May Store

Skills may store:

- reusable objective helper rules
- local procedures
- recurring fix patterns
- verification checklists
- mistake-prevention rules
- stable workflow lessons
- small reusable task procedures

## 20.3 What Skills Must Not Store

Skills must not store:

- project status
- raw chat history
- temporary handoffs
- full memory
- plan items
- search method
- context packages
- secrets
- speculative notes

Search/retrieval logic belongs in:

```text
context_retrieval.md
```

not in `skills/`.

## 20.4 Skill Lifecycle

Recommended lifecycle:

```text
candidate → review → approved → archived
```

Approved skills should require human review.

Skill scripts are disabled by default.

External skill lookup is disabled by default.

---

# 21. Document Metadata Enrichment Workflow

Document Metadata Enrichment makes existing documents retrieval-ready.

Use it when a document lacks useful metadata.

Operational prompt:

```text
document_metadata_enrichment_prompt.md
```

## 21.1 Inputs

It can work with:

- Markdown documents
- text documents
- product notes
- architecture notes
- specifications
- prompts
- templates
- examples
- decision records
- research notes
- framework docs
- old source material
- arbitrary documents prepared for retrieval

## 21.2 Output

It outputs:

- full document with frontmatter
- frontmatter only
- patch instructions
- report only

depending on config.

## 21.3 Boundaries

It does not:

- convert the document into Yin/Yang
- generate Yang contracts
- generate Master Documents
- perform Genesis
- perform Triage
- implement code
- fix bugs
- change document meaning
- invent missing project facts

## 21.4 Enrichment Quality Criteria

A good enrichment result:

- preserves document body
- adds useful metadata
- marks uncertainty
- does not invent facts
- adds retrieval description
- adds tags/aliases carefully
- classifies document type
- marks status
- includes source fields where known
- includes validation notes when needed

---

# 22. Context Retrieval Builder Workflow

The Context Retrieval Builder selects and packages relevant context.

Operational prompt:

```text
context_retrieval_builder_prompt.md
```

## 22.1 Two Phases

```text
Mode 1 = Intake / Search Planning
Mode 2 = Retrieval / Output Building
```

Mode 1 defines the search.

Mode 2 builds the output.

## 22.2 Output Modes

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

## 22.3 Retrieval Signals

Use explicit signals first:

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

Use semantic search only as helper.

## 22.4 Initialization Check

Before searching, check whether deterministic retrieval is available.

Look for:

- `context_retrieval.md`
- metadata/frontmatter conventions
- metadata-tagged documents
- metadata index if available
- context root
- docs root
- memory file if requested
- skills index if requested

If missing, do not pretend retrieval is initialized.

Correct response:

```text
Retrieval is not initialized yet. Run Workspace Context Initialization first, or provide `context_retrieval.md` and metadata conventions.
```

---

# 23. How Major Prompts Use These Conventions

## 23.1 Workspace Context Initialization

Uses prompt config to decide which artifacts to create/check.

May create:

- `plan.md`
- `memory.md`
- `context_retrieval.md`
- context package template
- Search Log template
- metadata index template
- optional `skills/`

## 23.2 Workspace State Maintenance

Maintains living state:

- `plan.md`
- `memory.md`
- `skills/`
- `skills_index.md`
- `skills_bundle.md`

Does not clean stable method/template files by default.

## 23.3 Context Retrieval Builder

Uses metadata and retrieval conventions to select context and build an output artifact.

## 23.4 Document Metadata Enrichment

Uses metadata conventions to add or update frontmatter.

## 23.5 Yin/Yang Prompt Generator

Uses:

- source metadata
- module/submodule IDs
- source block IDs
- template availability rules
- target artifact config
- model/platform config
- conversion config

Important boundary:

```text
A repository link is not attached template content.
```

## 23.6 Triage

Uses:

- metadata retrieval when available
- Search Logs
- context packages
- memory excerpts
- paired Yin/Yang documents
- model/platform setup status
- fallback labeling

---

# 24. Naming and File Conventions

## 24.1 Frontmatter Templates

Recommended future templates:

```text
templates/context/metadata_frontmatter_template.md
templates/context/prompt_config_block_template.md
templates/context/context_package_template.md
templates/context/search_log_template.md
templates/context/metadata_index_template.md
```

## 24.2 Prompt Names

Current operational prompt names:

```text
workspace_context_initialization_prompt.md
workspace_state_maintenance_prompt.md
context_retrieval_builder_prompt.md
document_metadata_enrichment_prompt.md
yin_yang_prompt_generator.md
```

Optional future single-artifact prompts:

```text
plan_md_prompt.md
memory_md_prompt.md
context_retrieval_prompt.md
context_package_generation_prompt.md
metadata_index_generation_prompt.md
skills_maintenance_prompt.md
```

Clarification:

```text
context_retrieval_builder_prompt.md = existing universal retrieval/output builder
context_retrieval_prompt.md         = optional future single-artifact prompt for creating/checking context_retrieval.md
```

Do not confuse them.

---

# 25. Anti-Patterns

Avoid:

- treating tags as the entire metadata system
- using vague tags such as `misc`, `stuff`, or `important`
- storing prompt execution choices as permanent document truth
- treating document frontmatter as prompt runtime config
- treating Search Logs as memory
- treating context packages as memory
- treating `skills/` as Memory 2.0
- treating `skills_bundle.md` as source of truth
- storing search/retrieval logic in skills instead of `context_retrieval.md`
- creating metadata indexes manually and letting them drift
- pretending deterministic retrieval exists when it is not initialized
- using semantic search as primary retrieval when explicit metadata exists
- treating repository links as attached template content
- using Document Metadata Enrichment as Yin/Yang conversion
- using Context Retrieval Builder to rewrite source documents
- using Workspace State Maintenance to perform Triage
- using Workspace Context Initialization to implement code
- inventing missing metadata certainty
- inventing source paths, IDs, or dates
- including secrets in metadata, Search Logs, or context packages

---

# 26. Quality Checklist

Before accepting metadata/frontmatter:

- [ ] `id` is stable and useful.
- [ ] `title` is human-readable.
- [ ] `document_type` is correct.
- [ ] `document_role` is clear.
- [ ] `layer` is correct.
- [ ] `status` is current.
- [ ] `version` and `metadata_version` are present.
- [ ] language fields are present where relevant.
- [ ] tags are specific.
- [ ] aliases are useful but not misleading.
- [ ] `summary` is concise.
- [ ] `retrieval_description` helps future retrieval.
- [ ] source fields are filled only when known.
- [ ] scope fields use module/submodule IDs where applicable.
- [ ] relationships are specific.
- [ ] Yin/Yang pairing is correct where relevant.
- [ ] retrieval fields are accurate.
- [ ] uncertainty is marked.
- [ ] missing context is listed.
- [ ] no source paths or dates are invented.
- [ ] no secrets are included.

Before accepting a prompt config block:

- [ ] config keys are explicit.
- [ ] user-selected values are not asked again.
- [ ] missing required values trigger Assistant Mode.
- [ ] optional missing values trigger Optional Clarification Mode.
- [ ] fallback mode is clearly labeled.
- [ ] model/platform optimization is not claimed without references.
- [ ] output mode is clear.
- [ ] file creation/update permissions are explicit where needed.

Before accepting retrieval output:

- [ ] retrieval initialization was checked.
- [ ] metadata signals were used first.
- [ ] derived keys are marked as derived.
- [ ] selected sources are listed.
- [ ] exclusions are listed.
- [ ] Search Log is included when enabled.
- [ ] Search Log is not stored as memory.
- [ ] context package is task-specific.
- [ ] secrets are excluded.
- [ ] confidence and open questions are stated.

---

# 27. Summary

Metadata and config are not decoration.

They are the mechanism that allows the Allzy Framework to keep AI work scoped, searchable, auditable, and reusable.

Use document frontmatter to describe artifacts.

Use prompt config blocks to control prompt execution.

Use Search Logs to explain retrieval.

Use context packages to carry temporary task context.

Use metadata indexes as generated lookup helpers.

Use skills for reusable objective helper rules, not memory.

Use Document Metadata Enrichment to prepare documents for retrieval.

Use Context Retrieval Builder to select and package context.

Use Workspace Context Initialization to create the workspace context layer.

Use Workspace State Maintenance to keep living state compressed and useful.

The core rule remains:

```text
Make the relevant context explicit before asking an AI agent to act.
```
