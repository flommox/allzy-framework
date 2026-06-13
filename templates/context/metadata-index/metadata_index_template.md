---
id: "allzy.framework.templates.context.metadata-index"
title: "Metadata Index Template"
artifact_type: "Template"
template_family: "context.metadata-index"
status: "Draft"
version: "0.2.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - template
  - metadata-index
  - retrieval
---

## Template Body

Copy the frontmatter block below for a generated Metadata Index.

```yaml
---
id: ""
title: "Metadata Index"
document_type: "Metadata Index"
document_role: "Generated Lookup Index"
layer: "Workspace Context"
status: "Generated"
version: "0.1.0"
metadata_version: "1.0.0"
created: ""
updated: ""
tags:
  - metadata-index
  - retrieval
retrieval_description: "[When should this Metadata Index be retrieved? Describe the retrieval scenario.]"
source:
  generated_from: "document frontmatter"
validation:
  metadata_inferred: false
  uncertain_fields: []
  missing_context: []
  needs_human_review: false
---
```

# Metadata Index

## Status

This file is a generated lookup helper.

It is not the source of truth.

Source documents and their frontmatter remain the source of truth.

## Index Metadata

```yaml
index_version: "0.1.0"
generated_at: ""
generated_by: ""
source_roots: []
documents_indexed: 0
documents_excluded: 0
```

## Indexed Documents

| ID | Path | Title | Type | Layer | Status | Module | Submodule | Tags | Retrieval Priority |
|---|---|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |  |  |

## Paired Yin/Yang Documents

| Yin | Yang | Module | Submodule | Status |
|---|---|---|---|---|
|  |  |  |  |  |

## Excluded Documents

| Path / ID | Reason |
|---|---|
|  |  |

## Missing / Incomplete Metadata

| Path / ID | Missing fields | Notes |
|---|---|---|
|  |  |  |

## JSON Shape

If generating JSON instead of Markdown, use this shape:

```json
[
  {
    "id": "",
    "path": "",
    "title": "",
    "document_type": "",
    "document_role": "",
    "layer": "",
    "status": "",
    "version": "",
    "updated": "",
    "tags": [],
    "aliases": [],
    "module_id": "",
    "submodule_id": "",
    "parent": "",
    "children": [],
    "paired_yin": "",
    "paired_yang": "",
    "related": [],
    "references": [],
    "retrieval_description": "",
    "retrieval_ready": true,
    "retrieval_priority": ""
  }
]
```

## Rules

- Generate this index from document frontmatter.
- Do not manually invent index truth.
- Do not let this file silently diverge from source documents.
- Rebuild the index when source frontmatter changes.
