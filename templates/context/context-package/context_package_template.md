---
id: "allzy.framework.templates.context.context-package"
title: "Context Package Template"
artifact_type: "Template"
template_family: "context.context-package"
status: "Draft"
version: "0.2.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - template
  - context-package
---

## Template Body

Copy the frontmatter block below for a Context Package.

```yaml
---
id: ""
title: "Context Package — "
document_type: "Context Package"
document_role: "Temporary Task Context"
layer: "Workspace Context"
status: "Active"
version: "0.1.0"
metadata_version: "1.0.0"
created: ""
updated: ""
language: "[Yin output language | English]"
technical_identifiers_language: "English"
tags:
  - context-package
retrieval_description: ""
source:
  generated_from: ""
  source_document_id: ""
  search_log: ""
validation:
  metadata_inferred: false
  uncertain_fields: []
  missing_context: []
  needs_human_review: false
---
```

# Context Package — [Task / Topic]

## Purpose

[Explain why this context package exists and which task it supports.]

## Target Audience

[Human / Agent 2 / reviewer / documentation agent / custom.]

## Intended Use

[Explain how the receiver should use this package.]

## Task

[Describe the specific task.]

## Scope Boundaries

### In Scope

- [Item]

### Out of Scope

- [Item]

## Selected Sources

| Source | Type | Status | Why included |
|---|---|---|---|
| [Source] | [Type] | [Current / Draft / Stable / Deprecated] | [Reason] |

## Relevant Context Summary

[Summarize selected context. Keep this compact and task-specific.]

## Direct Excerpts

Use direct excerpts only when necessary.

### Source: [Name]

```text
[Excerpt]
```

## Memory Excerpts

Include only relevant `memory.md` excerpts when needed.

```text
[Relevant memory excerpt]
```

## Skills Used

List any selected skills from `skills_index.md` or `context/skills/`.

| Skill | Why relevant |
|---|---|
| [Skill] | [Why relevant] |

## Search Log

Paste or link the Search Log for this context package.

## Exclusions

| Excluded source | Reason |
|---|---|
| [Excluded source] | [Reason] |

## Assumptions

- [Assumption]

## Open Questions

- [Question]

## Confidence

[High / Medium / Low / Unknown]

## Handoff Notes

[Instructions for the next agent/human.]

## Rules

- This package is temporary task context.
- This package is not `memory.md`.
- This package is not `context_retrieval.md`.
- This package must not include secrets.
- Confirmed lasting facts should be moved to `memory.md` through the state workflow.
