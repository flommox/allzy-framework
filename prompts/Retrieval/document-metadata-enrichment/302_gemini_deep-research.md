---
id: "allzy.framework.prompts.retrieval.document-metadata-enrichment.gemini-deep-research"
title: "Document Metadata Enrichment Prompt — Gemini Deep Research"
artifact_type: "Prompt"
prompt_family: "Retrieval"
prompt_variant: "Document Metadata Enrichment"
adaptation_target: "Gemini Deep Research"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - retrieval
  - document-metadata-enrichment
  - gemini
  - deep-research
---

# Document Metadata Enrichment Research Brief — Gemini Deep Research
Use Gemini Deep Research.
Act as a senior technical documentation and retrieval systems research analyst.
## Research Objective
Conduct a source-based research report that evaluates best practices for enriching existing documents with YAML frontmatter metadata for deterministic retrieval, indexing, linking, filtering, review, context packaging, and later AI-assisted workflows.
The research must support the Allzy Framework’s **Document Metadata Enrichment** workflow.
This is a research-and-synthesis task.
Do not directly enrich a user document.
Do not convert documents into Yin/Yang.
Do not generate Yang contracts, Master Documents, Genesis outputs, Triage outputs, implementation plans, application code, API schemas, or database schemas.
## Decision Context
This report will be used to validate and improve the Allzy Framework Prompt Library’s Document Metadata Enrichment prompt and metadata schema.
The target workflow is:
```text
existing document
→ analyze content
→ add or update metadata/frontmatter
→ preserve document body
→ make the document easier to find, link, classify, and reuse

The report should help decide whether the prompt’s metadata fields, frontmatter conventions, uncertainty handling, retrieval fields, document classification logic, and preservation rules are aligned with current documentation, static-site, knowledge-base, retrieval, and AI-context-management practices.

Scope

* Geography: Global / English-language technical documentation ecosystem
* Timeframe: latest available information, prioritizing current documentation and recent sources where relevant
* Domain: technical documentation, Markdown metadata, YAML frontmatter, knowledge-base organization, retrieval/indexing, AI-assisted document workflows, context packaging
* Target audience: Allzy Framework maintainers and prompt-library designers
* Company/project context: local-first / deterministic documentation workflows with optional later AI assistance
* Include:
    * YAML frontmatter conventions
    * metadata fields for retrieval and document discovery
    * document IDs, titles, aliases, tags, keywords, summaries, and descriptions
    * source, path, filename, origin, and provenance fields
    * classification fields such as confidentiality, sensitivity, audience, lifecycle, priority, stability
    * scope fields such as project, product, system, domain, module, component, feature, topic
    * relationship fields such as parent, children, related, references, dependencies, supersession, conflicts
    * retrieval readiness, indexing, chunking, preferred retrieval keys, and exclusion logic
    * uncertainty and human-review metadata
    * preservation of document bodies during metadata enrichment
    * handling existing frontmatter and unknown custom fields
    * secret/privacy handling in metadata workflows
    * risks of over-tagging, vague tags, invented links, invented dates, and unsupported classification
* Exclude:
    * direct rewriting of the Allzy prompt
    * direct enrichment of a specific user document
    * Yin/Yang conversion design
    * code implementation
    * database schema implementation
    * API contract generation
    * product architecture expansion beyond metadata-enrichment relevance
    * unsupported SEO listicles
    * claims that are not relevant to document metadata, retrieval, or knowledge organization

Source Expectations

Prioritize:

* official documentation for Markdown/YAML frontmatter systems
* static-site generator documentation where frontmatter conventions are specified
* documentation tooling references
* knowledge-base and information architecture guidance
* search/indexing and retrieval documentation
* AI/RAG/context-management documentation where relevant
* security/privacy guidance for secrets and sensitive data in documentation
* reputable technical articles or engineering blogs when official documentation is unavailable
* standards or de facto conventions for structured metadata where relevant

Avoid:

* unsupported claims
* anonymous forum posts as primary evidence
* outdated documentation when current documentation exists
* low-quality SEO listicles
* sources that do not provide evidence for their claims
* marketing claims that do not explain practical metadata behavior

Research Tasks

1. Identify current best practices for YAML frontmatter metadata in Markdown and documentation workflows.
2. Evaluate which metadata categories are useful for deterministic retrieval, indexing, linking, filtering, review, and context packaging.
3. Compare how documentation systems and knowledge tools commonly use:
    * id
    * title
    * description
    * tags
    * aliases
    * keywords
    * summary
    * source/provenance fields
    * relationship fields
    * status/lifecycle fields
4. Research how retrieval-oriented metadata should handle:
    * stable identifiers
    * tag quality
    * aliases and search intent
    * chunking hints
    * preferred retrieval keys
    * exclusion from indexing
    * review and confidence indicators
5. Research best practices for preserving original document content when adding or updating metadata.
6. Research how existing frontmatter should be updated safely:
    * preserve valid fields
    * normalize only where justified
    * keep unknown custom fields
    * avoid deleting user-specific metadata without reason
7. Research how metadata workflows should handle uncertainty:
    * missing context
    * inferred fields
    * uncertain document type
    * uncertain status
    * guessed module or topic relationships
    * human review flags
8. Research security and privacy risks in document metadata workflows:
    * secrets in source documents
    * accidental indexing of sensitive data
    * confidential source paths
    * private customer/user data
    * metadata summaries that leak sensitive content
9. Compare the researched best practices against the Allzy Document Metadata Enrichment metadata shape below.
10. Identify:

* fields that are strongly supported by current practice
* fields that are useful but Allzy-specific
* fields that may be too broad, redundant, or risky
* fields that require strict uncertainty handling
* fields that should remain empty rather than guessed
* any missing metadata category that would materially improve deterministic retrieval

11. Produce recommendations only when supported by the research.

Allzy Metadata Shape Under Review

Use this schema as the object being evaluated.

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

Required Comparison Dimensions

Include a comparison table that evaluates each major metadata group:

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

For each group, compare:

* purpose
* support from researched sources or practices
* retrieval value
* risk if guessed incorrectly
* recommendation
* whether it should be required, optional, empty-if-unknown, or Allzy-specific

Required Output Structure

Return a structured research report with these sections:

1. Executive Summary
2. Research Scope
3. Source Approach / Methodology
4. Key Findings
5. YAML Frontmatter and Metadata Practice Overview
6. Retrieval-Oriented Metadata Findings
7. Metadata Group Comparison Table
8. Preservation, Existing Frontmatter, and Body-Safety Findings
9. Security, Privacy, and Secret-Handling Findings
10. Uncertainty and Human Review Findings
11. Risks, Gaps, and Contradictions
12. Allzy Schema Assessment
13. Recommendations
14. Source Notes and Citations

Verification and Grounding Rules

* Base factual claims on researched and source-supported information.
* Compare findings across sources where possible.
* Separate sourced facts from interpretation.
* Mark unverifiable claims as uncertain.
* Identify contradictions between sources.
* Do not fill information gaps with unsupported assumptions.
* If a requested data point is not available, state that it is unavailable.
* Logical synthesis is allowed only when clearly grounded in researched sources.
* Recommendations must be tied to researched evidence or clearly marked as Allzy-specific design judgment.
* Do not invent URLs, standards, tool behaviors, or documentation rules.
* Do not claim that a field is industry-standard unless the research supports that claim.
* Do not treat Allzy-specific concepts such as Yin/Yang, layer, module_id, submodule_id, or deterministic context retrieval as external standards.

Final Instruction

Base the report on researched and source-supported information. Do not fill gaps with unsupported assumptions. If information cannot be verified, mark it as unavailable or uncertain. Separate factual findings from interpretation and recommendations. Do not directly enrich documents, do not convert documents into Yin/Yang, and do not generate implementation artifacts.
