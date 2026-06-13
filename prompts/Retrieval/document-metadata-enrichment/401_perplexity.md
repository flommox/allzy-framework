---
id: "allzy.framework.prompts.retrieval.document-metadata-enrichment.perplexity"
title: "Document Metadata Enrichment Prompt — Perplexity"
artifact_type: "Prompt"
prompt_family: "Retrieval"
prompt_variant: "Document Metadata Enrichment"
adaptation_target: "Perplexity"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - retrieval
  - document-metadata-enrichment
  - perplexity
---

# Document Metadata Enrichment Search Prompt — Perplexity
## Purpose
Use this prompt with Perplexity / Sonar-style web-search models when the task requires publicly indexed research about document metadata enrichment, YAML frontmatter conventions, retrieval-oriented metadata, indexing, linking, filtering, review workflows, context packaging, and AI-assisted documentation workflows.
Do not use this prompt to directly enrich a private user document.
Do not use this prompt to convert documents into Yin/Yang.
Do not use this prompt to generate Yang contracts, Master Documents, Genesis outputs, Triage outputs, implementation plans, code, API contracts, or database schemas.
Perplexity search models use `instructions` for response behavior and `input` for the actual web-search query. All search-critical terms, scope, timeframe, and topic details must appear in `input`.
Do not ask Perplexity to generate URLs or source links. Source URLs must come from the host application’s `search_results`, not from generated answer text.
---
## instructions
Provide concise, source-grounded research synthesis for technical documentation and retrieval-system design.
Use only information that can be verified from publicly available search results.
If reliable public information is not found for a requested point, state that clearly instead of speculating.
Separate sourced facts from interpretation and Allzy-specific recommendations.
Do not generate URLs, source links, or fake citations in the answer text.
Do not claim that a metadata field or convention is an industry standard unless search results support that claim.
Do not introduce unsupported product facts about Allzy.
Do not convert documents into Yin/Yang.
Do not generate Yang contracts, Master Documents, Genesis outputs, Triage outputs, implementation plans, code, API contracts, or database schemas.
Keep the response structured and practical.
Return Markdown with the requested sections.
---
## input
Research publicly available information about best practices for YAML frontmatter metadata and document metadata enrichment in Markdown documentation, technical documentation systems, static-site generators, knowledge bases, retrieval/indexing workflows, AI context packaging, and document search workflows.
Focus on how existing documents can be enriched with standardized metadata/frontmatter while preserving the original document body.
Research context:
This research supports the Allzy Framework Document Metadata Enrichment workflow:
```text
existing document
→ analyze content
→ add or update metadata/frontmatter
→ preserve document body
→ make the document easier to find, link, classify, filter, review, index, package as context, and reuse

Research scope:

* Domain: Markdown documentation, YAML frontmatter, technical documentation, knowledge-base organization, deterministic retrieval, indexing, document discovery, AI context management, documentation metadata
* Geography: global / English-language technical documentation ecosystem
* Timeframe: prioritize current documentation and recent sources where relevant
* Public-source boundary: use publicly indexed information only
* Include: official documentation, static-site generator documentation, documentation tooling references, search/indexing documentation, AI/RAG/context-management documentation where relevant, and reputable technical sources
* Exclude: unsupported SEO listicles, anonymous forum posts as primary evidence, outdated sources when current documentation exists, private documents, inaccessible paywalled details, and unsupported marketing claims

Research tasks:

1. Identify publicly documented best practices for YAML frontmatter in Markdown and documentation workflows.
2. Identify metadata fields commonly used for document discovery, retrieval, classification, filtering, linking, and review.
3. Evaluate practical support for these metadata categories:
    * stable IDs
    * titles
    * descriptions
    * document types
    * document roles
    * status and lifecycle fields
    * versions
    * created, updated, and reviewed dates
    * language metadata
    * tags
    * aliases
    * keywords
    * summaries
    * retrieval descriptions
    * search intent
    * source/provenance fields
    * confidentiality and sensitivity fields
    * audience fields
    * project/product/system/module/topic scope fields
    * parent/child/related/reference/dependency fields
    * supersession and conflict fields
    * retrieval readiness
    * indexing status
    * chunking hints
    * preferred retrieval keys
    * retrieval exclusion logic
    * inferred metadata flags
    * uncertain fields
    * missing context
    * human review flags
4. Research safe handling of existing frontmatter:
    * preserving valid fields
    * keeping unknown custom fields
    * normalizing only when justified
    * avoiding deletion of user-specific metadata
5. Research body preservation during metadata enrichment:
    * adding/updating frontmatter without rewriting document content
    * risks of changing meaning while enriching metadata
6. Research security and privacy risks:
    * secrets in source documents
    * private keys
    * tokens
    * passwords
    * sensitive customer/user data
    * confidential source paths
    * metadata summaries leaking sensitive content
    * accidental indexing of private information
7. Identify which metadata fields are broadly supported by public documentation practice, which are retrieval-specific, and which should be treated as project-specific or Allzy-specific.
8. Identify risks of over-tagging, vague tags, invented relationships, invented dates, guessed module IDs, and unsupported classification.
9. Compare findings against this Allzy metadata shape:

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

Required answer shape:
Return a concise structured Markdown report with these sections:

1. Executive Summary
2. Public Source Boundary
3. Key Findings
4. YAML Frontmatter Practice Overview
5. Retrieval-Oriented Metadata Findings
6. Metadata Group Comparison Table
7. Existing Frontmatter and Body-Preservation Findings
8. Security and Privacy Findings
9. Uncertainty and Human Review Findings
10. Risks and Gaps
11. Allzy Schema Assessment
12. Practical Recommendations
13. Missing or Unverified Information

Comparison table requirements:
For each major metadata group, include:

* group name
* purpose
* public-practice support
* retrieval value
* risk if guessed incorrectly
* recommendation
* classification as required, optional, empty-if-unknown, retrieval-specific, or Allzy-specific

Major metadata groups:

* Core identity
* Dates and review metadata
* Language metadata
* Tags, aliases, and keywords
* Summary and retrieval intent
* Source and provenance
* Classification
* Scope
* Structure and relationships
* Yin/Yang conversion metadata
* Retrieval readiness
* Validation and uncertainty
* Output filename/folder suggestions

Missing-information behavior:
If reliable public information is not available for a claim or metadata category, say that it is not available or mark it as uncertain.

Final grounding rule:
Base the answer on publicly available search results. Do not fill gaps with unsupported assumptions. Do not generate source URLs in the answer. Do not directly enrich documents, convert documents into Yin/Yang, or generate implementation artifacts.
