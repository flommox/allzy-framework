---
id: "allzy.framework.prompts.retrieval.metadata-index-generation.universal"
title: "Metadata Index Generation Prompt — Universal"
artifact_type: "Prompt"
prompt_family: "Retrieval"
prompt_variant: "Metadata Index Generation"
adaptation_target: "Universal"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - retrieval
  - metadata-index-generation
  - universal
---

# `metadata_index_generation_prompt.md`

## Purpose

Use this prompt to generate, regenerate, or inspect a metadata index for an AI-assisted project workspace.

A metadata index helps agents find documents without broad guessing or reading the entire project.

It answers:

```text id="m7np9x"
Which documents exist, where are they, and how should agents find them deterministically?
```

This prompt builds an index from document metadata, frontmatter, paths, IDs, document types, layers, tags, and links.

It does not create `plan.md`.

It does not create `memory.md`.

It does not create `context_retrieval.md`.

It does not generate a context package.

It does not create or maintain skills.

It does not manually clean a generated index like a living state file.

It only creates, regenerates, or inspects a metadata index.

---

## When to Use This Prompt

Use this prompt when:

- generating `metadata_index.md`
- generating `metadata_index.json`
- regenerating an index from source documents
- checking whether an existing metadata index is stale
- extracting metadata from Markdown frontmatter
- indexing document IDs, module IDs, submodule IDs, document types, layers, tags, and links
- building lookup support for `context_retrieval.md`
- preparing a deterministic context selection workflow
- creating an index for Yin/Yang, Triage, implementation, review, reference, or state documents
- reducing broad repository scans by future agents

---

## When Not to Use This Prompt

Do not use this prompt to:

- create or update `plan.md`
- create or update `memory.md`
- create or update `context_retrieval.md`
- define retrieval rules
- generate context packages
- create or maintain skills
- write application code
- implement features
- fix bugs
- perform Triage
- generate a Master Document
- create Yin/Yang documents
- rewrite architecture
- manually edit generated index content without sources
- store permanent project truth
- store raw chat history
- store secrets

If the user asks for one of these tasks, explain that this prompt only generates, regenerates, or inspects metadata indexes.

---

## Config Block

This config block is always present.

If the config is filled, use it as **Preconfigured Mode**.

If the config is empty or incomplete, use **Assistant Mode** and ask only the next necessary question.

If the user manually edits the config before running the prompt, treat it exactly like website-generated config.

```yaml id="0itk44"
---
metadata_index_generation_config:
  mode: "" # assistant | preconfigured

  operation: "" # generate_index | regenerate_from_sources | inspect_staleness
  target_artifact: "metadata_index"
  output_format: "" # markdown | json | both
  output_path_markdown: "" # e.g. context/metadata_index.md
  output_path_json: "" # e.g. context/metadata_index.json

  allow_file_creation: null # true | false
  allow_file_updates: null # true | false
  allow_overwrite: false

  source_documents_provided: null # true | false
  source_paths_provided: null # true | false
  existing_index_provided: null # true | false
  context_retrieval_rules_provided: null # true | false

  source_roots:
    docs_root: "" # e.g. docs/
    context_root: "" # e.g. context/
    templates_root: "" # optional
    prompts_root: "" # optional
    modules_root: "" # optional
    source_filter: "" # e.g. *.md

  index_policy:
    include_document_id: true
    include_path: true
    include_title: true
    include_document_type: true
    include_layer: true
    include_status: true
    include_version: true
    include_created_date: true
    include_updated_date: true
    include_tags: true
    include_module_id: true
    include_submodule_id: true
    include_parent_child_links: true
    include_paired_yin_yang_links: true
    include_related_links: true
    include_generated_from: true
    include_supersedes_links: true
    include_short_summary: true
    include_missing_metadata_warnings: true
    exclude_archived_by_default: false
    exclude_deprecated_by_default: false
    exclude_secrets: true

  staleness_policy:
    compare_index_to_sources: true
    flag_missing_source_files: true
    flag_new_unindexed_files: true
    flag_changed_metadata: true
    flag_duplicate_ids: true
    flag_missing_required_fields: true
    flag_broken_links: true

  output_style: "copy_ready" # copy_ready | report_only | file_ready
  target_environment: "" # cursor | claude-code | codex-cli | chatgpt | gemini | other | unknown
---
```

---

## Operating Logic

This prompt supports three operations:

```text id="q6k1rp"
generate_index
regenerate_from_sources
inspect_staleness
```

### `generate_index`

Use this operation when:

- no metadata index exists
- source documents are provided
- source paths are accessible
- document metadata can be extracted
- an index should be generated for the first time

If source documents are not available, do not invent an index.

Return a template or ask for source documents.

---

### `regenerate_from_sources`

Use this operation when:

- an index already exists
- source documents are available
- the index may be stale
- source metadata changed
- new documents were added
- documents were deleted, archived, deprecated, or superseded
- duplicate IDs or broken links must be corrected from source truth

This operation should rebuild the index from current sources.

It should not manually patch old index entries unless source documents confirm them.

---

### `inspect_staleness`

Use this operation when:

- the user wants to know whether an index is current
- file updates are not allowed
- source documents are available for comparison
- an index exists but should not be overwritten
- the assistant should only report issues

Inspection should report problems.

Inspection should not rewrite the index.

---

## Assistant Mode

If the config is empty or incomplete, ask only the next necessary question.

Do not ask all setup questions at once.

### Question 1 — Operation

If `operation` is missing, ask:

```text id="h3x4qy"
What should I do with the metadata index?

1. Generate a new index from source documents
2. Regenerate an existing index from current sources
3. Inspect an existing index for staleness
```

### Question 2 — Output Format

Ask only if output format is missing:

```text id="xsfsk4"
Which index format should I produce?

1. Markdown
2. JSON
3. Both
```

### Question 3 — Source Documents

If generating or regenerating and sources are missing, ask:

```text id="31rxbs"
Please provide the source documents, source folder path, or file list that should be indexed.
```

### Question 4 — Existing Index

If inspecting staleness and the existing index is missing, ask:

```text id="f5jzy2"
Please provide the existing metadata_index.md or metadata_index.json.
```

### Question 5 — File Permission

Ask only if file access exists and permission is unclear:

```text id="ejv51w"
May I create or update the metadata index directly, or should I return copy-ready output only?
```

---

## File Access Rule

If running in an environment with file access, inspect configured source roots and target index files directly.

If running in a normal chat without file access, ask the user to paste or attach the needed documents, file list, or existing index.

Do not pretend to have read files that were not provided or accessible.

If the source set is too large, ask for a file manifest first.

If no source documents are available, do not generate fake index entries.

---

## Security and Privacy Check

Before generating, regenerating, or inspecting a metadata index, check all provided content for secrets or sensitive operational data.

Secrets include:

- API keys
- passwords
- tokens
- private credentials
- database URLs
- session secrets
- private customer or user data
- unredacted logs
- private infrastructure values
- internal URLs that should not be indexed

If secrets are present:

1. Stop.
2. Do not repeat the secret.
3. Ask the user to sanitize the input.
4. Use placeholders only if an example is needed.

Use placeholders such as:

```text id="n5joz0"
process.env.API_KEY
process.env.DATABASE_URL
$ENV_SESSION_SECRET
```

Never store real secrets in metadata indexes.

---

## Metadata Index Role

A metadata index is a generated lookup artifact.

It helps agents find documents using explicit metadata.

It is not:

```text id="n2xleo"
plan.md
memory.md
context_retrieval.md
context package
skills/
raw chat history
source of project truth
```

The source of truth is the source document metadata.

The index should be regenerated from sources when it becomes stale.

Do not hand-edit generated index contents unless explicitly requested and source data is unavailable.

---

## Metadata Index Must Contain

A useful metadata index may contain:

- document ID
- file path
- title
- document type
- layer
- status
- version
- created date
- updated date
- tags
- module ID
- submodule ID
- parent links
- child links
- paired Yin link
- paired Yang link
- related links
- generated-from links
- supersedes / superseded-by links
- short summary
- metadata warnings

---

## Metadata Index Must Not Contain

Do not include:

- full document contents
- full memory contents
- full context packages
- full skills
- raw chat logs
- secrets
- private credentials
- unrelated implementation details
- speculative interpretations as metadata
- invented IDs
- invented links
- generated summaries presented as confirmed source metadata

---

## Required Source Metadata

Use these fields when available:

```yaml id="ds9jhh"
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

Optional fields:

```yaml id="m9hg4y"
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

Do not require every optional field.

If required fields are missing, include a metadata warning.

Do not invent missing values unless they can be safely inferred from filename or heading, and mark them as inferred.

---

## ID Rules

IDs should be:

- stable
- unique
- lowercase where practical
- human-readable
- not based on volatile dates unless intentionally versioned
- not duplicated across documents

If duplicate IDs are found:

```text id="03qobx"
- keep both entries in the inspection report
- flag duplicate_id warning
- do not silently rename
- recommend correction in source documents
```

If no ID exists:

```text id="h24zsg"
- use path as temporary lookup key
- mark id as missing
- add metadata warning
```

---

## Summary Rules

If short summaries are enabled:

- summarize only the document’s apparent purpose
- keep summaries short
- do not replace reading the source
- do not include unsupported claims
- mark summary as generated when appropriate

Example:

```text id="654xnp"
summary: "Defines workspace state maintenance rules for plan.md and memory.md."
summary_source: "generated"
```

---

## Markdown Index Output Shape

Use this structure for `metadata_index.md`.

```markdown id="0rgsqz"
# Metadata Index

_Generated: YYYY-MM-DD_  
_Source roots: [source roots]_  
_Format: Markdown_  

## Index Status

- Documents indexed: [number]
- Missing metadata warnings: [number]
- Duplicate IDs: [number]
- Broken links: [number]
- Archived/deprecated included: [yes/no]

## Documents

| ID | Path | Title | Type | Layer | Status | Tags | Updated | Warnings |
|---|---|---|---|---|---|---|---|---|
| [id or missing] | [path] | [title] | [document_type] | [layer] | [status] | [tags] | [date] | [warnings] |

## Links

| Source ID | Link Type | Target | Status |
|---|---|---|---|
| [source] | parent/child/paired_yin/paired_yang/related/supersedes | [target] | ok/broken/unresolved |

## Missing Metadata

| Path | Missing Fields | Notes |
|---|---|---|
| [path] | [fields] | [notes] |

## Duplicate IDs

| ID | Paths |
|---|---|
| [id] | [paths] |

## Staleness / Regeneration Notes

- [Note or None]
```

---

## JSON Index Output Shape

Use this structure for `metadata_index.json`.

```json id="mfcgwv"
{
  "generated": "YYYY-MM-DD",
  "source_roots": [],
  "format": "json",
  "status": {
    "documents_indexed": 0,
    "missing_metadata_warnings": 0,
    "duplicate_ids": 0,
    "broken_links": 0,
    "archived_deprecated_included": false
  },
  "documents": [
    {
      "id": "",
      "path": "",
      "title": "",
      "document_type": "",
      "layer": "",
      "status": "",
      "version": "",
      "created": "",
      "updated": "",
      "tags": [],
      "module_id": "",
      "submodule_id": "",
      "parent": "",
      "children": [],
      "paired_yin": "",
      "paired_yang": "",
      "related": [],
      "generated_from": "",
      "supersedes": [],
      "superseded_by": [],
      "summary": "",
      "summary_source": "",
      "warnings": []
    }
  ],
  "links": [
    {
      "source_id": "",
      "link_type": "",
      "target": "",
      "status": ""
    }
  ],
  "missing_metadata": [],
  "duplicate_ids": [],
  "staleness_notes": []
}
```

Do not output invalid JSON when JSON is requested.

If values are unknown, use empty strings, empty arrays, or explicit warning fields.

---

## Staleness Inspection Rules

When inspecting an existing index, compare it with available sources.

Check for:

```text id="5xtwdi"
- indexed files that no longer exist
- source files not present in the index
- changed frontmatter
- changed document title
- changed status
- changed tags
- duplicate IDs
- missing required fields
- broken parent/child links
- broken paired Yin/Yang links
- broken related links
- archived/deprecated documents incorrectly marked current
- generated summaries that no longer match the source
```

If sources are unavailable, inspect only internal consistency and clearly state the limitation.

---

## Regeneration Rules

When regenerating:

1. Treat source documents as source of truth.
2. Parse available frontmatter first.
3. Use headings or filenames only as fallback.
4. Preserve only generated index structure, not stale index claims.
5. Flag missing metadata.
6. Flag duplicate IDs.
7. Flag broken links.
8. Include archived or deprecated documents only according to policy.
9. Do not invent missing relationships.
10. Do not overwrite source documents.

If an existing index contains entries not found in sources, flag them as stale or unresolved.

Do not preserve stale entries as current.

---

## Template-Only Rule

If the user requests an index but no source documents are available, do not generate fake entries.

Return a metadata index template and state:

```text id="uq9z3g"
A full metadata index requires source documents or a file manifest.
```

---

## Date Rule

Use the current date for:

```text id="pjmyw1"
generated
```

If the current date is unavailable, use:

```text id="8365zn"
YYYY-MM-DD
```

Do not invent historical dates.

---

## Processing Protocol

### Step 1 — Resolve Config

Read the config block.

Determine:

- mode
- operation
- output format
- output paths
- source roots
- source document availability
- existing index availability
- index policy
- staleness policy
- file creation permission
- file update permission
- output style

If config is incomplete, enter Assistant Mode.

---

### Step 2 — Validate Output Format

If `output_format` is missing, ask for it.

If JSON is requested, produce valid JSON.

If both are requested, produce both Markdown and JSON outputs.

---

### Step 3 — Determine Source Availability

For `generate_index`, require:

- source documents, or
- source paths with file access, or
- file manifest

For `regenerate_from_sources`, require:

- existing index if comparison is desired, and
- current source documents or source paths

For `inspect_staleness`, require:

- existing index
- source documents if full staleness check is expected

If required input is missing, ask only for that input.

---

### Step 4 — Check Scope

Verify that the request is about metadata index generation, regeneration, or inspection.

If the request is about another artifact, redirect:

```text id="n2wbsu"
This prompt only handles metadata indexes. Use the appropriate artifact prompt for plan.md, memory.md, context_retrieval.md, context packages, or skills.
```

---

### Step 5 — Security Check

Inspect source content and index content for secrets.

Stop if unsafe.

Do not repeat secrets.

---

### Step 6 — Extract Metadata

For each source document:

1. Read frontmatter if present.
2. Extract title from frontmatter or first heading.
3. Extract path.
4. Extract document type.
5. Extract layer.
6. Extract status.
7. Extract tags.
8. Extract IDs and links.
9. Generate short summary only if enabled.
10. Record missing fields and warnings.

Do not infer beyond source evidence.

---

### Step 7 — Validate Metadata

Check:

- missing IDs
- duplicate IDs
- missing titles
- missing document types
- missing layers
- malformed tags
- broken links
- superseded documents
- archived or deprecated status
- invalid JSON output
- unsafe content

---

### Step 8 — Produce Output

Depending on operation:

```text id="5xsow3"
generate_index
→ return metadata index from source documents

regenerate_from_sources
→ return regenerated metadata index from current source documents

inspect_staleness
→ return staleness inspection report
```

If sources are unavailable, return a template and explain what is missing.

---

### Step 9 — Explain Index Quality

Briefly list:

- documents indexed
- warnings found
- duplicate IDs
- broken links
- stale entries
- missing sources
- recommended source fixes

---

## Required Output Format

Return exactly:

```markdown id="1fndod"
# Metadata Index Generation Result

## 1. Operation Used

[generate_index / regenerate_from_sources / inspect_staleness]

## 2. Target Output

[metadata_index.md / metadata_index.json / both / report only]

## 3. Input Used

[source documents / source paths / file manifest / existing index / missing input]

## 4. Metadata Index

```markdown
[metadata_index.md output, if requested]
```

```json
[metadata_index.json output, if requested]
```

## 5. Index Summary

- Documents indexed:
- Missing metadata:
- Duplicate IDs:
- Broken links:
- Stale entries:
- Needs review:

## 6. Warnings / Blockers

- [Warning, blocker, or None]

## 7. Recommended Next Step

[Next action]
``` id="wrw9l5"

If `inspect_staleness` is used, replace `## 4. Metadata Index` with:

```markdown
## 4. Staleness Inspection Report

[inspection findings]
```

If no source documents are available, replace `## 4. Metadata Index` with:

```markdown
## 4. Metadata Index Template

[template output]
```

---

## Hard Boundaries

Do not:

- write application code
- implement features
- fix bugs
- perform Triage
- generate a Master Document
- create Yin/Yang documents
- create or update `plan.md`
- create or update `memory.md`
- create or update `context_retrieval.md`
- generate context packages
- create or maintain skills
- store secrets
- claim file access when no file access exists
- invent source documents
- invent IDs
- invent metadata conventions
- invent parent/child links
- invent paired Yin/Yang links
- treat generated index as project truth over source documents
- include full document contents in the index
- manually clean a generated index when sources should be used
- overwrite an existing file unless explicitly allowed

---

## Final Rule

Your job is to generate, regenerate, or inspect a metadata index.

Use source documents as source of truth.

Index explicit metadata first.

Flag missing metadata.

Flag duplicate IDs.

Flag broken links.

Do not invent entries.

Do not treat the index as memory, plan, retrieval method, context package, or skills.

If required source input is missing, ask only for the next necessary input.
