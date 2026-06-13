---
id: "allzy.framework.templates.context.search-log"
title: "Search Log Template"
artifact_type: "Template"
template_family: "context.search-log"
status: "Draft"
version: "0.2.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - template
  - search-log
  - retrieval
---

## Template Body

Copy the frontmatter block below for a Search Log.

```yaml
---
id: ""
title: "Search Log — "
document_type: "Search Log"
document_role: "Retrieval Audit Trail"
layer: "Workspace Context"
status: "Active"
version: "0.1.0"
metadata_version: "1.0.0"
created: ""
updated: ""
language: "[Yin output language | English]"
technical_identifiers_language: "English"
tags:
  - search-log
  - retrieval
retrieval_description: ""
---
```

# Search Log — [Task / Query]

## Retrieval Goal

[What context was needed and why?]

## Requested Output Mode

[summary / deep_brief / agent_context_package / patch_handoff_context / document_source_pack / review_context / custom]

## Retrieval Initialization Check

| Check | Result |
|---|---|
| `context_retrieval.md` available | YES / NO / UNKNOWN |
| Metadata/frontmatter conventions available | YES / NO / UNKNOWN |
| Metadata-tagged documents available | YES / NO / UNKNOWN |
| Metadata index available | YES / NO / UNKNOWN / not used |
| Docs root available | YES / NO / UNKNOWN |
| Context root available | YES / NO / UNKNOWN |
| `memory.md` requested/available | YES / NO / not requested |
| Skills index requested/available | YES / NO / not requested |

## Search Inputs

- Topic:
- User query:
- Known module_id:
- Known submodule_id:
- Known layer:
- Known document_type:
- Known tags:
- Known aliases:
- Known folders:

## Derived Retrieval Keys

Derived keys are not confirmed truth.

| Key | Value | Confidence |
|---|---|---|
| topic |  |  |
| possible_module_ids |  |  |
| possible_submodule_ids |  |  |
| likely_layers |  |  |
| likely_document_types |  |  |
| derived_tags |  |  |
| aliases |  |  |
| likely_folders |  |  |

## Retrieval Signals Used

- [Signal]

## Searches Performed

| Step | Search / Filter | Result |
|---|---|---|
| 1 | [Search / filter applied] | [Result summary] |

## Sources Selected

| Source | Type | Status | Why selected |
|---|---|---|---|
| [Source] | [Type] | [Current / Draft / Stable / Deprecated] | [Why selected] |

## Sources Excluded

| Source | Reason |
|---|---|
| [Source] | [Reason] |

## Relevant Findings

- [Finding]

## Uncertainty

- [Uncertainty]

## Confidence

[High / Medium / Low / Unknown]

## Open Questions

- [Question]

## Notes for Context Package / Handoff

[Notes.]

## Rules

- Search Log is not memory.
- Search Log is not a context package by itself.
- Confirmed lasting facts belong in `memory.md`.
- Do not include secrets.
- Do not pretend deterministic retrieval was available if initialization was missing.
