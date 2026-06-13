---
id: "allzy.framework.prompts.review.framework-docs-consistency-review.gemini"
title: "Framework Docs Consistency Review Prompt — Gemini"
artifact_type: "Prompt"
prompt_family: "Review"
prompt_variant: "Framework Docs Consistency Review"
adaptation_target: "Gemini"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - review
  - framework-docs-consistency-review
  - gemini
---

# Framework Docs Consistency Review Prompt — Gemini Standard
Act as a neutral framework documentation consistency reviewer for the Allzy Framework.
Task:
Analyze the provided Allzy Framework documentation set for internal consistency. Identify drift, contradictions, incorrect numbering, missing cross-references, mismatched terminology, and V5 summary alignment issues.
Use only the provided documentation files as context. You may perform logical deductions based strictly on the provided docs, but do not introduce external information or invent missing framework rules.
Context:
The expected documentation set is:
```text
01_Philosophy.md
02_Architecture.md
03_Yin_Yang_Contracts.md
04_Deterministic_Metadata_Graph.md
05_Triage_and_Maintenance.md
06_State_Management.md
07_Metadata_Config_and_Retrieval_Conventions.md
08_Glossary_and_Terminology.md
09_Origin_and_Principles.md
allzy-framework-master-specification-v5.md

If one or more expected docs are missing, report them as missing. Do not infer their content.

Check whether the docs agree on:

* document numbering
* file names
* framework phases
* layer model
* Full / Compact / Direct terminology
* Yin/Yang artifact types
* no standalone Yang Compact
* Triage Fast / Standard / Deep
* Workspace Context Initialization
* Workspace State Maintenance
* Context Retrieval Builder
* Document Metadata Enrichment
* Metadata/frontmatter rules
* Prompt Config Block rules
* Search Log / Context Package / Metadata Index distinctions
* Skills vs. Memory distinction
* Model vs. Platform distinction
* Template availability rules
* V5 summary alignment

Review areas:

1. File Numbering and Naming

Check that these are consistent everywhere:

07_Metadata_Config_and_Retrieval_Conventions.md
08_Glossary_and_Terminology.md
09_Origin_and_Principles.md

2. Terminology

Current scope terms:

Full
Compact
Direct

Valid Yin/Yang artifacts:

Yin Page
Compact Yin Page
Yang Core Module
Yin/Yang Document
Yin/Yang Compact

Invalid:

standalone Yang Compact

3. Framework Phases

Expected framework phases:

Genesis
Segmentation
Modularization
Specification
Execution

Genesis must not be described as creating final Yin/Yang documents or implementation code.

4. Workspace / State

Check these distinctions:

Workspace Context Initialization ≠ Workspace State Maintenance
Workspace State Maintenance ≠ Triage
plan.md ≠ memory.md
Search Log ≠ memory.md
Context Package ≠ memory.md
context_retrieval.md ≠ Context Package
skills/ ≠ Memory 2.0
skills_bundle.md ≠ source of truth

5. Metadata / Retrieval

Check these distinctions:

Document Frontmatter ≠ Prompt Config Block
Document Metadata Enrichment ≠ Yin/Yang Conversion
Context Retrieval Builder ≠ only Agent-2 package
Metadata Index ≠ source of truth

6. Prompt / Template Boundaries

Check these distinctions:

Prompt = instruction for AI
Template = reusable structure
Example = filled reference
Reference = supporting material

Also check that repository links are not treated as attached template content.

Output format:
Return exactly this Markdown report structure:

# Framework Docs Consistency Review
## Verdict
[CONSISTENT / MOSTLY_CONSISTENT / NEEDS_MINOR_FIXES / NEEDS_MAJOR_FIXES]
## Summary
[German summary.]
## Critical Inconsistencies
| Issue | Files affected | Why it matters | Required fix |
|---|---|---|---|
## Major Inconsistencies
| Issue | Files affected | Why it matters | Recommended fix |
|---|---|---|---|
## Minor Inconsistencies
| Issue | Files affected | Recommended fix |
|---|---|---|
## Numbering / File Name Check
[PASS / FAIL + details]
## Terminology Check
[PASS / FAIL + details]
## Yin/Yang Rule Check
[PASS / FAIL + details]
## Workspace / State Check
[PASS / FAIL + details]
## Metadata / Retrieval Check
[PASS / FAIL + details]
## V5 Alignment
[Explain whether V5 accurately summarizes 01–09.]
## Recommended Patch Order
1. [File]
2. [File]
## Do Not Change
[List sections/files that should remain untouched.]

Constraints:

* Do not rewrite docs unless explicitly asked.
* Do not create new framework rules.
* Do not invent source truth.
* Do not generate architecture, modules, submodules, Yin/Yang documents, API contracts, database schemas, implementation plans, execution prompts, or code.
* Do not use outside knowledge for factual claims.
* Do not treat missing docs as agreeing with present docs.
* Do not treat repository links as attached template content.
* Do not treat skills/ or skills_bundle.md as source truth.
* Do not treat a Metadata Index as source truth.
* If a finding is uncertain, mark it as uncertain.
* If a claim is an inference rather than directly stated in the docs, label it as an inference.
* If no issues are found in a severity table, keep the table and write None found.
* Prefer German explanations for the user-facing review.
* Keep file names, artifact names, identifiers, and technical terms in English.
* If the environment supports citations, cite the relevant file or section for each material finding. If citations are unavailable, name the affected files precisely.
* Do not fabricate citations, URLs, file names, line numbers, quote spans, or IDs.

Final instruction:
Base the review only on the provided documentation context. Do not stop at the first relevant match; synthesize across the entire provided documentation set before returning the report. Return only the required Markdown report structure and no extra commentary.
