---
id: "allzy.framework.prompts.retrieval.document-metadata-enrichment.universal"
title: "Document Metadata Enrichment Prompt — Universal"
artifact_type: "Prompt"
prompt_family: "Retrieval"
prompt_variant: "Document Metadata Enrichment"
adaptation_target: "Universal"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - retrieval
  - document-metadata-enrichment
  - universal
---

# Document Metadata Enrichment Prompt

## Purpose

Use this prompt to enrich existing documents with a standardized YAML frontmatter metadata block so they can participate in deterministic retrieval, indexing, linking, filtering, review, context packaging, and later AI-assisted workflows.

This prompt works with arbitrary documents.

The document does not need to be an Allzy Yin/Yang document.

This prompt does not convert the document into Yin/Yang.

This prompt does not rewrite the document content unless explicitly requested.

Its primary job is:

```text
existing document
→ analyze content
→ add or update metadata/frontmatter
→ preserve document body
→ make the document easier to find, link, classify, and reuse
```

---

## When to Use This Prompt

Use this prompt when you have existing documents such as:

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

Use this prompt before using deterministic context retrieval on documents that do not yet have useful metadata.

---

## When Not to Use This Prompt

Do not use this prompt to:

- convert a document into Yin/Yang
- generate Yang contracts
- generate a Master Document
- perform Genesis
- perform Triage
- implement code
- fix bugs
- rewrite application logic
- summarize the document as the only output unless requested
- change the document’s meaning
- invent missing project facts

If the user wants a Yin/Yang conversion, use a dedicated document-to-Yin/Yang conversion prompt instead.

---

## Config Block

This config block is always present.

If filled, use it as **Preconfigured Mode**.

If empty or incomplete, use **Assistant Mode** and ask only for missing required information.

If manually edited by the user, treat it exactly like website-generated config.

```yaml
---
document_metadata_enrichment_config:
  mode: "" # assistant | preconfigured

  processing_mode: "" # single_document | batch
  input_type: "" # markdown | text | mixed | unknown
  target_document_path: ""
  target_document_name: ""

  metadata_schema: "allzy_universal"
  metadata_version: "1.0.0"
  preserve_document_body: true
  add_frontmatter_if_missing: true
  update_existing_frontmatter: true
  keep_unknown_fields: true
  normalize_existing_fields: true

  enrichment_depth: "" # basic | standard | detailed
  infer_ids_and_tags: true
  infer_document_type: true
  infer_layer: true
  infer_status: true
  infer_relationships: true
  infer_module_ids: true
  infer_yin_yang_links: true

  created_updated_policy: "set_updated_only" # preserve_if_existing | infer_if_available | set_updated_only | ask
  current_date: "" # YYYY-MM-DD, optional; if empty, use execution date if known or placeholder

  output_delivery:
    output_mode: "full_document" # full_document | frontmatter_only | patch_instructions | report_only
    requested_filename: ""
    filename_strategy: "" # preserve_original | derive_from_title | derive_from_id | provided

  safety:
    reject_secrets: true
    mark_uncertainty: true
    do_not_invent_missing_facts: true
---
```

---

## Input Block

Provide the document or documents below.

```markdown
## Document Input

[PASTE OR ATTACH DOCUMENT CONTENT HERE]

## Existing File Path / Name

[OPTIONAL]

## Known Context

[OPTIONAL: project, module, folder, intended use, source, related docs, known tags, known IDs]

## Desired Output

[OPTIONAL: full_document / frontmatter_only / patch_instructions / report_only]
```

---

## Core Rule

The document body is the source.

Metadata must describe the document.

Metadata must not invent new product facts.

If a field cannot be inferred safely, leave it empty or mark it as uncertain.

Prefer useful empty fields over missing structural fields.

---

## Required Metadata Block

Use this full metadata shape unless the user explicitly provides a stricter schema.

Keep fields even if some values are empty.

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

## Field Guidance

### `id`

Create a stable, lowercase, dot- or kebab-style ID.

Examples:

```text
docs.discord-moderation-overview
framework.context-retrieval-method
prompt.yin-yang-generator
example.user-login
```

If no stable ID can be inferred, use:

```text
[missing-id]
```

and add `id` to `uncertain_fields`.

### `title`

Use the document’s actual title if present.

If no title exists, infer a concise descriptive title.

### `description`

One to two sentences describing what the document is.

### `document_type`

Use a specific type.

Recommended universal values:

```text
Reference
Guide
Specification
Prompt
Template
Example
Research Note
Project Note
Architecture Note
Decision Record
Workflow
Checklist
Source Document
Context File
State File
Index
Review
Handoff
Unknown
```

Allzy/framework-specific values may include:

```text
Master Document
Master Document Compact
Project Tree
Topic Block
Module Document
Submodule Document
Yin Page
Compact Yin Page
Yang Core Module
Yin/Yang Document
Yin/Yang Compact
Context Retrieval
Context Package
Search Log
Agent Skill
```

Do not force a document into Yin/Yang types unless the content really is Yin/Yang.

### `document_role`

Describe the role in retrieval.

Examples:

```text
source_of_truth
supporting_reference
example
template
prompt
state
generated_export
historical_reference
draft
```

### `layer`

Use a broad retrieval layer.

Examples:

```text
Vision
Infrastructure
Backend
System
Core
Ecosystem
Utilities
Framework
State
Reference
Example
Prompt
Template
Unknown
```

If uncertain, use `Unknown` and add `layer` to `uncertain_fields`.

### `status`

Use:

```text
Draft
Review
Active
Stable
Deprecated
Archived
Superseded
Unknown
```

If the document looks current but no status exists, use `Active` with `status` in `uncertain_fields`.

### `created`, `updated`, `last_reviewed`

Do not invent dates.

Rules:

- Preserve existing dates.
- Infer only if clearly present in the document or file metadata.
- If the current date is known and the prompt is actively updating metadata, set `updated` to current date when allowed by config.
- Leave `created` empty if unknown.
- Add unknown date fields to `uncertain_fields` if relevant.

### `language`

Set the primary document language.

Examples:

```text
German
English
Spanish
Chinese
Mixed
Unknown
```

### `technical_identifiers_language`

Default:

```text
English
```

### `tags`

Use many useful tags.

Tags should help retrieval.

Prefer concrete domain, module, workflow, artifact, technology, and concept tags.

Good tags:

```text
discord
moderation
permissions
roles
workspace-context
memory
plan
retrieval
metadata
frontmatter
prompt-generator
yin-yang
functional-core
imperative-shell
settings
backup
ui-state
security
privacy
billing
documentation
```

Avoid weak tags:

```text
misc
stuff
important
thing
note
document
general
```

### `aliases`

Add alternative names users may search for.

Examples:

```text
"Discord bot moderation"
"role permissions"
"workspace memory"
"context search"
"Yin Yang generator"
```

### `keywords`

Add technical or semantic keywords that may not be good tags.

### `summary`

Short neutral summary.

### `retrieval_description`

One retrieval-focused sentence explaining when this document should be found.

Example:

```text
Use this document when searching for workspace state maintenance rules, plan.md cleanup, memory.md compression, or skills maintenance.
```

### `search_intent`

List likely user search intents.

Example:

```yaml
search_intent:
  - "Find rules for maintaining memory.md"
  - "Find how to clean plan.md"
  - "Find workspace state cleanup prompt"
```

### `source`

Describe where the document came from.

Do not invent source URLs or paths.

### `classification`

Use conservative values.

Do not mark a document as public if unknown.

### `scope`

Fill project/module/topic fields where inferable.

Use `module_id` and `submodule_id` only if a stable module/submodule can be inferred.

### `structure`

Use this to prepare future linking.

Fields may remain empty.

Use `related`, `references`, `depends_on`, and `used_by` when relationships are explicit or strongly implied.

Do not invent links.

### `yin_yang`

Use these fields to prepare later conversion.

Set:

```yaml
is_yin_yang_document: false
```

unless the document already follows Yin/Yang structure.

Use:

```yaml
can_be_converted_to_yin_yang: "possible"
```

if the document contains enough intent/specification material that could later be transformed.

Possible values:

```text
yes
possible
no
unknown
```

Recommended conversion targets:

```text
Yin Page
Compact Yin Page
Yang Core Module
Yin/Yang Document
Yin/Yang Compact
none
unknown
```

### `retrieval`

Mark retrieval readiness.

Use `retrieval_confidence`:

```text
High
Medium
Low
```

Use lower confidence if title, ID, layer, document type, or tags are uncertain.

### `validation`

List uncertainty.

If any important field was inferred, keep:

```yaml
metadata_inferred: true
```

Set `needs_human_review: true` when:

- major fields are uncertain
- source context is missing
- document type is unclear
- status is unclear
- module ID is guessed
- relationships are inferred but not confirmed

### `output`

Suggest filename/folder only if safe.

Do not rename the document unless requested.

---

## Processing Modes

### Single Document Mode

Process one document.

Return the enriched document or metadata block.

### Batch Mode

Process multiple documents one at a time.

For each document, return:

- file name or title
- generated frontmatter
- uncertainty notes
- recommended filename/folder if requested

Do not merge multiple documents into one.

Do not reuse metadata across documents unless clearly shared.

---

## Output Modes

### `full_document`

Return the full document with YAML frontmatter inserted or updated.

Preserve the document body.

### `frontmatter_only`

Return only the generated YAML frontmatter.

### `patch_instructions`

Return instructions describing what frontmatter to add or update.

### `report_only`

Return a metadata analysis report without rewriting the document.

---

## Assistant Mode Flow

If config or input is missing, ask only for what is needed.

### Step 1 — Ask for Document

```text
Please paste or attach the document you want to enrich with metadata.
```

### Step 2 — Ask for Output Mode

Only if not provided:

```text
How should I return the result?

1. Full document with frontmatter
2. Frontmatter only
3. Patch instructions
4. Report only
```

### Step 3 — Ask for Known Context

Only if helpful:

```text
Do you already know the project, module_id, submodule_id, layer, status, or related documents?
If not, I will infer what I can and mark uncertainty.
```

Do not ask long questionnaires.

Proceed when enough information exists.

---

## Security and Privacy Check

Before generating metadata, inspect the document for secrets or sensitive operational data.

Secrets include:

- API keys
- passwords
- access tokens
- refresh tokens
- bearer tokens
- private keys
- session secrets
- private infrastructure values
- private customer/user data unless explicitly allowed

If secrets are present:

1. Stop.
2. Do not repeat the secret.
3. Ask the user to sanitize the document.
4. Do not include the secret in metadata, summary, tags, aliases, search intent, or output.

Use placeholders such as:

```text
process.env.API_KEY
process.env.DATABASE_URL
$ENV_SESSION_SECRET
```

---

## Enrichment Protocol

Follow this sequence.

### Step 1 — Resolve Config

Determine:

- processing mode
- output mode
- enrichment depth
- whether to preserve body
- date policy
- whether existing frontmatter should be updated

### Step 2 — Identify Existing Frontmatter

Check whether the document already has YAML frontmatter.

If yes:

- preserve valid fields
- normalize field names when allowed
- fill missing fields
- update stale metadata only when justified
- keep unknown fields if configured

If no:

- generate the required metadata block

### Step 3 — Analyze Document Content

Identify:

- actual title
- document purpose
- document type
- layer
- status
- topic
- domain
- module/submodule if any
- primary concepts
- workflows or systems mentioned
- likely tags
- aliases
- relationships
- whether it may later convert to Yin/Yang

### Step 4 — Generate Metadata

Fill the required metadata block.

Use empty values where unknown.

Mark uncertainty explicitly.

### Step 5 — Preserve Body

Do not rewrite the document body unless explicitly requested.

If the output mode is `full_document`, insert or update the YAML block and then include the original body unchanged.

### Step 6 — Return Result

Return the requested output mode.

Include a short change summary and uncertainty notes.

---

## Required Output Format

Return exactly:

```markdown
# Document Metadata Enrichment Result

## 1. Metadata Summary

- Title:
- ID:
- Document type:
- Layer:
- Status:
- Retrieval confidence:
- Needs human review:

## 2. Enriched Output

[Full document, frontmatter only, patch instructions, or report.]

## 3. Tags and Aliases

### Tags

- [tag]

### Aliases

- [alias]

## 4. Relationships / References

- Related:
- References:
- Depends on:
- Used by:
- Paired Yin:
- Paired Yang:

## 5. Uncertainty / Human Review

- [uncertain field or decision]

## 6. Notes

- [brief note]
```

If `full_document` is requested, place the full enriched document under `Enriched Output`.

If `frontmatter_only` is requested, place only the YAML block under `Enriched Output`.

---

## Hard Boundaries

Do not:

- convert the document into Yin/Yang
- rewrite the document body unless requested
- invent missing product facts
- invent dates
- invent URLs or file paths
- invent relationships
- remove existing valid metadata without reason
- remove unknown custom frontmatter fields when `keep_unknown_fields` is true
- include secrets
- mark uncertain inferred fields as confirmed
- overuse vague tags
- collapse structural fields into tags only
- treat generated metadata as final truth when uncertainty exists

---

## Final Rule

Your job is to make existing documents retrieval-ready.

Add or update a rich standardized YAML frontmatter block.

Prefer more useful metadata fields over too few fields.

Leave unknown values empty and mark uncertainty.

Preserve the document body.

Do not transform the document into Yin/Yang.

Begin by resolving the config block and checking whether document input was provided.
