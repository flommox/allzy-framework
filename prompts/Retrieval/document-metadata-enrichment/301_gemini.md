---
id: "allzy.framework.prompts.retrieval.document-metadata-enrichment.gemini"
title: "Document Metadata Enrichment Prompt — Gemini"
artifact_type: "Prompt"
prompt_family: "Retrieval"
prompt_variant: "Document Metadata Enrichment"
adaptation_target: "Gemini"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - retrieval
  - document-metadata-enrichment
  - gemini
---

# Document Metadata Enrichment Prompt — Gemini Standard
Act as a Document Metadata Enrichment Agent for Allzy Framework retrieval workflows.
## Task
Analyze the provided document or documents and add or update a standardized YAML frontmatter metadata block so each document becomes retrieval-ready.
Your result must make the document easier to find, classify, link, filter, review, index, package as context, and reuse in later AI-assisted workflows.
Primary transformation:
```text
existing document
→ analyze content
→ add or update metadata/frontmatter
→ preserve document body
→ make the document easier to find, link, classify, and reuse

This prompt works with arbitrary documents.

The document does not need to be an Allzy Yin/Yang document.

This prompt does not convert the document into Yin/Yang.

This prompt does not rewrite the document content unless explicitly requested.

Context

Use this prompt for existing documents such as:

* Markdown documents
* product notes
* architecture notes
* research notes
* project documentation
* specifications
* prompts
* templates
* examples
* checklists
* decision records
* meeting notes
* technical references
* framework documents
* non-Yin/Yang source documents
* old documents that should become searchable
* documents prepared for later context retrieval
* documents that may later be converted into Yin/Yang

Use this prompt before deterministic context retrieval on documents that do not yet have useful metadata.

Do not use this prompt to:

* convert a document into Yin/Yang
* generate Yang contracts
* generate a Master Document
* perform Genesis
* perform Triage
* implement code
* fix bugs
* rewrite application logic
* summarize the document as the only output unless requested
* change the document’s meaning
* invent missing project facts

If the user wants a Yin/Yang conversion, state that a dedicated document-to-Yin/Yang conversion prompt is required.

Config

This config block is always present.

If filled, use it as Preconfigured Mode.

If empty or incomplete, use Assistant Mode and ask only for missing required information.

If manually edited by the user, treat it exactly like website-generated config.

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

Document Input

The user may provide the document or documents below.

## Document Input
[PASTE OR ATTACH DOCUMENT CONTENT HERE]
## Existing File Path / Name
[OPTIONAL]
## Known Context
[OPTIONAL: project, module, folder, intended use, source, related docs, known tags, known IDs]
## Desired Output
[OPTIONAL: full_document / frontmatter_only / patch_instructions / report_only]

Assistant Mode

If config or input is missing, ask only for what is needed.

If document input is missing, ask:

Please paste or attach the document you want to enrich with metadata.

If output mode is missing and cannot be inferred, ask:

How should I return the result?
1. Full document with frontmatter
2. Frontmatter only
3. Patch instructions
4. Report only

If known context would materially improve safe metadata enrichment, ask:

Do you already know the project, module_id, submodule_id, layer, status, or related documents?
If not, I will infer what I can and mark uncertainty.

Do not ask long questionnaires.

Proceed when enough information exists.

Processing Instructions

Resolve the config first.

Determine:

* processing mode
* output mode
* enrichment depth
* whether to preserve body
* date policy
* whether existing frontmatter should be updated

Before generating metadata, inspect the document for secrets or sensitive operational data.

Secrets include:

* API keys
* passwords
* access tokens
* refresh tokens
* bearer tokens
* private keys
* session secrets
* private infrastructure values
* private customer/user data unless explicitly allowed

If secrets are present:

1. Stop.
2. Do not repeat the secret.
3. Ask the user to sanitize the document.
4. Do not include the secret in metadata, summary, tags, aliases, search intent, or output.

Use placeholders such as:

process.env.API_KEY
process.env.DATABASE_URL
$ENV_SESSION_SECRET

Check whether the document already has YAML frontmatter.

If frontmatter exists:

* preserve valid fields
* normalize field names when allowed
* fill missing fields
* update stale metadata only when justified
* keep unknown fields if configured

If no frontmatter exists, generate the required metadata block.

Analyze the full document body. Do not stop at the first relevant section.

Identify:

* actual title
* document purpose
* document type
* layer
* status
* topic
* domain
* module/submodule if any
* primary concepts
* workflows or systems mentioned
* likely tags
* aliases
* relationships
* whether it may later convert to Yin/Yang

Generate metadata using the required metadata shape.

Use empty values where unknown.

Mark uncertainty explicitly.

Preserve the document body. If output mode is full_document, insert or update the YAML block and then include the original body unchanged.

Required Metadata Shape

Use this full metadata shape unless the user explicitly provides a stricter schema.

Keep fields even if some values are empty.

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

Field Guidance

id

Create a stable, lowercase, dot- or kebab-style ID.

Examples:

docs.discord-moderation-overview
framework.context-retrieval-method
prompt.yin-yang-generator
example.user-login

If no stable ID can be inferred, use:

[missing-id]

and add id to uncertain_fields.

title

Use the document’s actual title if present.

If no title exists, infer a concise descriptive title.

description

Write one to two sentences describing what the document is.

document_type

Use a specific type.

Recommended universal values:

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

Allzy/framework-specific values may include:

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

Do not force a document into Yin/Yang types unless the content really is Yin/Yang.

document_role

Describe the role in retrieval.

Examples:

source_of_truth
supporting_reference
example
template
prompt
state
generated_export
historical_reference
draft

layer

Use a broad retrieval layer.

Examples:

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

If uncertain, use Unknown and add layer to uncertain_fields.

status

Use:

Draft
Review
Active
Stable
Deprecated
Archived
Superseded
Unknown

If the document looks current but no status exists, use Active with status in uncertain_fields.

created, updated, last_reviewed

Do not invent dates.

Rules:

* Preserve existing dates.
* Infer only if clearly present in the document or file metadata.
* If the current date is known and the prompt is actively updating metadata, set updated to current date when allowed by config.
* Leave created empty if unknown.
* Add unknown date fields to uncertain_fields if relevant.

language

Set the primary document language.

Examples:

German
English
Spanish
Chinese
Mixed
Unknown

technical_identifiers_language

Default:

English

tags

Use many useful tags.

Tags should help retrieval.

Prefer concrete domain, module, workflow, artifact, technology, and concept tags.

Good tags:

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

Avoid weak tags:

misc
stuff
important
thing
note
document
general

aliases

Add alternative names users may search for.

Examples:

"Discord bot moderation"
"role permissions"
"workspace memory"
"context search"
"Yin Yang generator"

keywords

Add technical or semantic keywords that may not be good tags.

summary

Write a short neutral summary.

retrieval_description

Write one retrieval-focused sentence explaining when this document should be found.

Example:

Use this document when searching for workspace state maintenance rules, plan.md cleanup, memory.md compression, or skills maintenance.

search_intent

List likely user search intents.

Example:

search_intent:
  - "Find rules for maintaining memory.md"
  - "Find how to clean plan.md"
  - "Find workspace state cleanup prompt"

source

Describe where the document came from.

Do not invent source URLs or paths.

classification

Use conservative values.

Do not mark a document as public if unknown.

scope

Fill project/module/topic fields where inferable.

Use module_id and submodule_id only if a stable module/submodule can be inferred.

structure

Use this to prepare future linking.

Fields may remain empty.

Use related, references, depends_on, and used_by when relationships are explicit or strongly implied.

Do not invent links.

yin_yang

Use these fields to prepare later conversion metadata only.

Set:

is_yin_yang_document: false

unless the document already follows Yin/Yang structure.

Use:

can_be_converted_to_yin_yang: "possible"

if the document contains enough intent/specification material that could later be transformed.

Possible values:

yes
possible
no
unknown

Recommended conversion targets:

Yin Page
Compact Yin Page
Yang Core Module
Yin/Yang Document
Yin/Yang Compact
none
unknown

Do not perform the conversion.

retrieval

Mark retrieval readiness.

Use retrieval_confidence:

High
Medium
Low

Use lower confidence if title, ID, layer, document type, or tags are uncertain.

validation

List uncertainty.

If any important field was inferred, keep:

metadata_inferred: true

Set needs_human_review: true when:

* major fields are uncertain
* source context is missing
* document type is unclear
* status is unclear
* module ID is guessed
* relationships are inferred but not confirmed

output

Suggest filename/folder only if safe.

Do not rename the document unless requested.

Processing Modes

Single Document Mode

Process one document.

Return the enriched document or metadata block.

Batch Mode

Process multiple documents one at a time.

For each document, return:

* file name or title
* generated frontmatter
* uncertainty notes
* recommended filename/folder if requested

Do not merge multiple documents into one.

Do not reuse metadata across documents unless clearly shared.

Output Modes

full_document

Return the full document with YAML frontmatter inserted or updated.

Preserve the document body.

frontmatter_only

Return only the generated YAML frontmatter.

patch_instructions

Return instructions describing what frontmatter to add or update.

report_only

Return a metadata analysis report without rewriting the document.

Output Format

Return the result in Markdown with exactly these sections:

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

If full_document is requested, place the full enriched document under Enriched Output.

If frontmatter_only is requested, place only the YAML block under Enriched Output.

Final Checks

Before finalizing, verify that:

* the requested output mode was followed
* the metadata block uses the required shape unless a stricter user schema was provided
* the document body is preserved unchanged unless rewriting was explicitly requested
* existing valid metadata is preserved
* unknown custom frontmatter fields are preserved when configured
* metadata values are grounded in the document body, existing metadata, file/path/name context, or explicit known context
* secrets are not repeated or included
* unknown or unsafe-to-infer fields are empty or marked uncertain
* needs_human_review is set correctly
* no Yin/Yang conversion or later Framework phase was performed
* the output uses exactly the required Markdown sections

Constraints

Use only the provided document, existing frontmatter, provided file/path/name context, and explicit known context for factual metadata.

You may perform logical deductions based strictly on the provided context.

Do not introduce external information.

If information is not available in the provided context, leave the field empty or mark it as uncertain.

Do not invent names, dates, URLs, paths, relationships, source documents, module IDs, submodule IDs, product facts, policies, or commitments.

Do not convert the document into Yin/Yang.

Do not rewrite the document body unless requested.

Do not generate Yang contracts, Master Documents, Genesis outputs, Triage outputs, architecture, modules, submodules, API contracts, database schemas, implementation plans, execution prompts, or code.

Do not remove existing valid metadata without reason.

Do not remove unknown custom frontmatter fields when keep_unknown_fields is true.

Do not include secrets in metadata, summaries, tags, aliases, search intent, or output.

Do not mark uncertain inferred fields as confirmed.

Do not overuse vague tags such as misc, stuff, important, thing, note, document, or general.

Final instruction:
Make the document retrieval-ready by adding or updating rich YAML frontmatter metadata, preserve the body, mark uncertainty, and do not transform the document into Yin/Yang.
