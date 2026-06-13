---
id: "allzy.framework.prompts.retrieval.metadata-index-generation.gemini-deep-research"
title: "Metadata Index Generation Prompt — Gemini Deep Research"
artifact_type: "Prompt"
prompt_family: "Retrieval"
prompt_variant: "Metadata Index Generation"
adaptation_target: "Gemini Deep Research"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - retrieval
  - metadata-index-generation
  - gemini
  - deep-research
---

# Metadata Index Generation Prompt — Gemini Deep Research
Use Gemini Deep Research.
Act as a senior technical research analyst specializing in AI-assisted documentation systems, deterministic retrieval workflows, metadata indexing, and project workspace governance.
## Research Objective
Conduct a source-based research report that evaluates how to generate, regenerate, or inspect a metadata index for an AI-assisted Allzy Framework project workspace.
The research must support a safe, deterministic metadata-index workflow that helps agents answer:
```text
Which documents exist, where are they, and how should agents find them deterministically?

The research must focus on metadata index generation, regeneration, and staleness inspection from explicit document metadata, frontmatter, paths, IDs, document types, layers, tags, links, and file evidence.

Decision Context

This report will support the Allzy Framework Prompt Library and Retrieval workflow.

The goal is to validate and strengthen the prompt logic for metadata_index.md and metadata_index.json generation without expanding the task into unrelated Allzy Framework phases.

The report should help determine whether the metadata-index prompt:

* preserves source documents as the source of truth
* avoids invented metadata
* flags missing metadata, duplicate IDs, broken links, and stale entries
* keeps metadata_index separate from plan.md, memory.md, context_retrieval.md, context packages, and skills
* produces safe copy-ready Markdown and/or valid JSON outputs

Scope

* Geography: not applicable unless external documentation sources require regional context
* Timeframe: prioritize current documentation and best practices, especially recent guidance where available
* Domain: AI-assisted project workspaces, documentation metadata, deterministic retrieval, Markdown frontmatter, JSON indexes, file manifests, repository documentation workflows
* Target audience: Allzy Framework maintainers and AI agents using the Allzy Framework Prompt Library
* Deliverable type: source-based research report
* Include:
    * metadata index generation
    * metadata index regeneration from source documents
    * metadata index staleness inspection
    * source-of-truth handling
    * frontmatter and document metadata extraction
    * ID uniqueness and duplicate-ID handling
    * missing metadata warnings
    * broken link detection
    * archived/deprecated/superseded document handling
    * JSON validity expectations
    * Markdown index table structure
    * security and secret exclusion
    * file access limitations
    * deterministic lookup support for future retrieval workflows
* Exclude:
    * writing application code
    * implementing features
    * fixing bugs
    * performing Triage
    * generating a Master Document
    * creating Yin/Yang documents
    * creating or updating plan.md
    * creating or updating memory.md
    * creating or updating context_retrieval.md
    * defining full retrieval rules
    * generating context packages
    * creating or maintaining skills
    * rewriting architecture
    * storing permanent project truth
    * storing raw chat history
    * storing secrets
    * inventing Allzy-specific conventions not supported by the provided prompt or sources

Source Expectations

Prioritize:

* official documentation for Markdown frontmatter and YAML metadata where relevant
* JSON format and validation references
* documentation-system or static-site metadata conventions where relevant
* repository documentation practices
* software documentation indexing or metadata best-practice sources
* security guidance on avoiding secrets in generated artifacts
* source-control and generated-artifact best practices where relevant
* provided Allzy Framework prompt context as the semantic source of truth

Avoid:

* unsupported claims
* outdated or low-quality SEO listicles
* anonymous forum posts unless they are only used as weak contextual signals
* sources that do not provide evidence for their claims
* claims that would expand the Allzy Framework workflow beyond the provided metadata-index task

Research Tasks

1. Identify best-practice principles for generating a metadata index from source documents, frontmatter, paths, IDs, document types, layers, tags, and links.
2. Evaluate how the metadata index should preserve the source documents as the source of truth.
3. Determine how missing metadata should be represented without inventing IDs, links, tags, titles, or relationships.
4. Compare practices for Markdown table indexes and JSON index artifacts.
5. Identify validation rules for:
    * missing IDs
    * duplicate IDs
    * missing titles
    * missing document types
    * missing layers
    * malformed tags
    * broken parent/child links
    * broken paired Yin/Yang links
    * broken related links
    * archived, deprecated, or superseded documents
    * invalid JSON
    * unsafe or secret-containing content
6. Research how generated artifacts should handle staleness when source files change, are deleted, become archived/deprecated, or are superseded.
7. Identify safe handling rules for secrets and sensitive operational data in generated indexes.
8. Evaluate when the assistant should ask for missing source documents, a source folder path, a file list, or an existing metadata index instead of generating output.
9. Identify risks in over-indexing, under-indexing, generated summaries, inferred metadata, and treating a generated index as project truth.
10. Produce recommendations for strengthening the metadata-index prompt while preserving its strict scope and hard boundaries.

Required Metadata Index Operations to Analyze

The report must analyze these operations exactly:

generate_index
regenerate_from_sources
inspect_staleness

generate_index

Analyze when this operation is appropriate:

* no metadata index exists
* source documents are provided
* source paths are accessible
* document metadata can be extracted
* an index should be generated for the first time

If source documents are not available, the prompt must not invent an index.

It should return a template or ask for source documents.

regenerate_from_sources

Analyze when this operation is appropriate:

* an index already exists
* source documents are available
* the index may be stale
* source metadata changed
* new documents were added
* documents were deleted, archived, deprecated, or superseded
* duplicate IDs or broken links must be corrected from source truth

This operation should rebuild the index from current sources.

It should not manually patch old index entries unless source documents confirm them.

inspect_staleness

Analyze when this operation is appropriate:

* the user wants to know whether an index is current
* file updates are not allowed
* source documents are available for comparison
* an index exists but should not be overwritten
* the assistant should only report issues

Inspection should report problems.

Inspection should not rewrite the index.

Required Config Context to Preserve

The research must treat this config shape as the Allzy Framework prompt contract:

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

Required Source Metadata to Analyze

Analyze this source metadata schema as the expected Allzy Framework metadata input:

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

Optional fields:

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

The report must preserve these principles:

* Do not require every optional field.
* If required fields are missing, include a metadata warning.
* Do not invent missing values unless they can be safely inferred from filename or heading.
* Mark inferred values explicitly.

Required Output Shapes to Evaluate

Evaluate whether these output shapes are appropriate, complete, and safe.

Markdown Index Output Shape

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

JSON Index Output Shape

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

Required Report Structure

Produce the final report with this structure:

1. Executive Summary
2. Research Scope
3. Source Approach / Methodology
4. Key Findings
5. Metadata Index Workflow Assessment
6. Output Shape Assessment
7. Validation and Staleness Rules
8. Security, Privacy, and Secret-Handling Assessment
9. Risks, Gaps, and Uncertainties
10. Recommendations
11. Sources

Verification and Uncertainty Rules

Compare findings across sources where possible.

Mark unverifiable claims as uncertain.

Separate sourced facts from interpretation.

Identify contradictions between sources.

Do not fill information gaps with unsupported assumptions.

If a requested data point is not available, state that it is unavailable.

Use researched and source-supported information for factual claims.

Logical synthesis is allowed only when it is clearly grounded in the researched sources.

Hard Boundaries

Do not:

* write application code
* implement features
* fix bugs
* perform Triage
* generate a Master Document
* create Yin/Yang documents
* create or update plan.md
* create or update memory.md
* create or update context_retrieval.md
* generate context packages
* create or maintain skills
* store secrets
* claim file access when no file access exists
* invent source documents
* invent IDs
* invent metadata conventions
* invent parent/child links
* invent paired Yin/Yang links
* treat generated index as project truth over source documents
* include full document contents in the index
* manually clean a generated index when sources should be used
* overwrite an existing file unless explicitly allowed

Final Instruction

Base the report on researched and source-supported information plus the provided Allzy Framework metadata-index prompt contract. Do not fill gaps with unsupported assumptions. If information cannot be verified, mark it as unavailable or uncertain. Separate factual findings from interpretation and recommendations. Do not expand the task beyond metadata index generation, regeneration, or staleness inspection.
