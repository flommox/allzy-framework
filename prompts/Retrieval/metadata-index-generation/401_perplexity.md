---
id: "allzy.framework.prompts.retrieval.metadata-index-generation.perplexity"
title: "Metadata Index Generation Prompt — Perplexity"
artifact_type: "Prompt"
prompt_family: "Retrieval"
prompt_variant: "Metadata Index Generation"
adaptation_target: "Perplexity"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - retrieval
  - metadata-index-generation
  - perplexity
---

# Metadata Index Generation Prompt — Perplexity Search
## API Shape
Use the following separation:
- `instructions`: response behavior, language, style, formatting, uncertainty handling, and boundaries
- `input`: the actual search query and all search-critical terms, scope, timeframe, topic details, and missing-information behavior
Do not rely on `instructions` alone for retrieval targeting.
Do not ask the model to generate URLs or source links in the answer. Source URLs should be taken from the host application's `search_results` field.
---
## instructions
Provide a concise, source-grounded answer for an Allzy Framework metadata-index workflow.
Use a direct technical tone.
Base factual claims only on publicly available and search-verifiable information found through the search results and on the Allzy Framework metadata-index prompt contract included in the input.
If reliable public information is not found for a claim, state that the information is not available or not verifiable from public search results.
Do not invent source documents, IDs, metadata fields, links, relationships, source conventions, or Allzy Framework behavior.
Do not request or generate URLs in the answer. If sources are needed in a UI or downstream workflow, the host application must attach them from `search_results`.
Do not include few-shot examples in the search query.
Keep the answer structured and compact.
Return the result in Markdown.
Use this output structure:
```markdown id="ezw7a5"
# Perplexity Metadata Index Research Result
## 1. Query Focus
[short summary of the search objective]
## 2. Public Evidence Summary
[what public evidence supports]
## 3. Metadata Index Workflow Findings
[findings relevant to metadata index generation, regeneration, and staleness inspection]
## 4. Output Shape Findings
[findings relevant to Markdown indexes and JSON indexes]
## 5. Security and Secret-Handling Findings
[findings relevant to avoiding secrets and sensitive operational data]
## 6. Risks, Gaps, and Unverifiable Items
- [risk, gap, or unavailable information]
## 7. Recommendations for the Prompt
- [recommendation]
## 8. Source Handling Note
Source URLs must be attached by the host application from `search_results`, not generated in this answer.

Hard boundaries:

* Do not write application code.
* Do not implement features.
* Do not fix bugs.
* Do not perform Triage.
* Do not generate a Master Document.
* Do not create Yin/Yang documents.
* Do not create or update plan.md.
* Do not create or update memory.md.
* Do not create or update context_retrieval.md.
* Do not generate context packages.
* Do not create or maintain skills.
* Do not store secrets.
* Do not claim file access when no file access exists.
* Do not invent source documents.
* Do not invent IDs.
* Do not invent metadata conventions.
* Do not invent parent/child links.
* Do not invent paired Yin/Yang links.
* Do not treat generated index content as project truth over source documents.
* Do not include full document contents in an index.
* Do not manually clean generated index content when sources should be used.
* Do not overwrite an existing file.

If the searched public information is insufficient, say so clearly and still evaluate the Allzy prompt contract based only on the provided input.

⸻

input

Find publicly available, search-verifiable guidance relevant to generating, regenerating, or inspecting a metadata index for an AI-assisted project workspace.

Topic context:
AI-assisted project workspace metadata index generation, Markdown frontmatter metadata, YAML frontmatter, document IDs, document paths, document type metadata, layer metadata, tags, parent-child links, related links, JSON index artifacts, Markdown index tables, generated documentation indexes, source-of-truth handling, stale generated artifacts, duplicate IDs, broken links, missing metadata warnings, secret exclusion in generated artifacts.

Framework context:
This is for the Allzy Framework Prompt Library retrieval workflow. The metadata index helps future AI agents find documents deterministically instead of broadly guessing or reading the entire project.

Research objective:
Evaluate whether the following Allzy metadata-index prompt contract is safe, complete, and aligned with public best practices for generated metadata indexes.

Use publicly indexed sources only. If reliable public information is not available for a claim, state that it is unavailable or not verifiable from public search results.

Focus on one coherent search objective:
metadata index generation, regeneration from source documents, and staleness inspection for AI-assisted project workspaces.

Timeframe:
Use current publicly available guidance where relevant. Prioritize recent documentation and current best practices, but stable format standards such as JSON, Markdown, and YAML frontmatter may use durable documentation.

Required dimensions:

* metadata index generation from source documents
* metadata index regeneration from current source documents
* staleness inspection of an existing metadata index
* source documents as source of truth
* Markdown frontmatter and YAML metadata extraction
* JSON validity and schema-like output expectations
* Markdown table index readability
* missing metadata handling
* duplicate ID handling
* broken link detection
* archived, deprecated, and superseded document handling
* generated summary caution
* secrets and sensitive operational data exclusion
* file access limitations
* generated index artifacts not being treated as project truth

Public-source boundary:
Use publicly available sources such as official documentation, standards documentation, documentation-system guidance, repository documentation practices, JSON documentation, YAML/frontmatter documentation, static-site documentation conventions, and security guidance about secrets in generated artifacts.

Do not rely on private documents, private repositories, inaccessible internal systems, closed meetings, private social posts, or unsupported claims.

Missing-information behavior:
If no reliable public information is found for a category, state that clearly. Do not fill gaps with unsupported assumptions.

Allzy Framework metadata-index prompt contract to evaluate:

Purpose:
Use this prompt to generate, regenerate, or inspect a metadata index for an AI-assisted project workspace.

A metadata index helps agents find documents without broad guessing or reading the entire project.

It answers:
Which documents exist, where are they, and how should agents find them deterministically?

This prompt builds an index from document metadata, frontmatter, paths, IDs, document types, layers, tags, and links.

It does not create plan.md.

It does not create memory.md.

It does not create context_retrieval.md.

It does not generate a context package.

It does not create or maintain skills.

It does not manually clean a generated index like a living state file.

It only creates, regenerates, or inspects a metadata index.

Supported operations:

* generate_index
* regenerate_from_sources
* inspect_staleness

Use generate_index when:

* no metadata index exists
* source documents are provided
* source paths are accessible
* document metadata can be extracted
* an index should be generated for the first time

If source documents are not available, do not invent an index. Return a template or ask for source documents.

Use regenerate_from_sources when:

* an index already exists
* source documents are available
* the index may be stale
* source metadata changed
* new documents were added
* documents were deleted, archived, deprecated, or superseded
* duplicate IDs or broken links must be corrected from source truth

This operation should rebuild the index from current sources. It should not manually patch old index entries unless source documents confirm them.

Use inspect_staleness when:

* the user wants to know whether an index is current
* file updates are not allowed
* source documents are available for comparison
* an index exists but should not be overwritten
* the assistant should only report issues

Inspection should report problems. Inspection should not rewrite the index.

Config block:

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

Source metadata fields:

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

Optional source metadata fields:

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

Required handling:

* Do not require every optional field.
* If required fields are missing, include a metadata warning.
* Do not invent missing values unless they can be safely inferred from filename or heading, and mark them as inferred.
* IDs should be stable, unique, lowercase where practical, human-readable, not based on volatile dates unless intentionally versioned, and not duplicated across documents.
* If duplicate IDs are found, keep both entries, flag duplicate_id, do not silently rename, and recommend correction in source documents.
* If no ID exists, use path as a temporary lookup key, mark ID as missing, and add a metadata warning.

Metadata index must not contain:

* full document contents
* full memory contents
* full context packages
* full skills
* raw chat logs
* secrets
* private credentials
* unrelated implementation details
* speculative interpretations as metadata
* invented IDs
* invented links
* generated summaries presented as confirmed source metadata

Security requirements:
Before generating, regenerating, or inspecting a metadata index, check provided content for secrets or sensitive operational data.

Secrets include API keys, passwords, tokens, private credentials, database URLs, session secrets, private customer or user data, unredacted logs, private infrastructure values, and internal URLs that should not be indexed.

If secrets are present:

* stop
* do not repeat the secret
* ask the user to sanitize the input
* use placeholders only if an example is needed

Use placeholders such as:

* process.env.API_KEY
* process.env.DATABASE_URL
* $ENV_SESSION_SECRET

Required Markdown index shape:

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

Required JSON index shape:

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

Required answer shape:
Return a structured summary with key findings, workflow assessment, output shape assessment, risks, uncertainties, and recommendations. Do not include source URLs in generated text. Indicate that source URLs must come from the host application’s search_results.
