---
id: "allzy.framework.templates.context.metadata-frontmatter"
title: "Metadata Frontmatter Template"
artifact_type: "Template"
template_family: "context.metadata-frontmatter"
status: "Draft"
version: "0.2.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - template
  - metadata
  - frontmatter
  - retrieval
---

# Metadata Frontmatter Template

Use this template as the standard frontmatter block for documents that should participate in deterministic retrieval, indexing, linking, filtering, review, or future AI-assisted workflows.

## Template Body

Copy the YAML block below. Fill only known values. Leave unknown values empty.

```yaml
---
id: ""
title: ""
description: ""
document_type: ""
document_role: ""
layer: ""
status: "Draft"
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
  metadata_inferred: false
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

## Usage

1. Copy the YAML block.
2. Fill only known values.
3. Leave unknown values empty.
4. Mark inferred or uncertain values in `validation`.
5. Do not invent dates, IDs, file paths, source documents, or relationships.

## Rules

- Document frontmatter describes an artifact.
- Prompt config controls execution.
- Tags do not replace structural fields such as `layer`, `document_type`, `module_id`, or `submodule_id`.
- Search Logs are not memory.
- Context packages are temporary task context.
- Metadata indexes are generated lookup helpers, not source of truth.
