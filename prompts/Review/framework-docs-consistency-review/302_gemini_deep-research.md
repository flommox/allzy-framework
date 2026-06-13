---
id: "allzy.framework.prompts.review.framework-docs-consistency-review.gemini-deep-research"
title: "Framework Docs Consistency Review Prompt — Gemini Deep Research"
artifact_type: "Prompt"
prompt_family: "Review"
prompt_variant: "Framework Docs Consistency Review"
adaptation_target: "Gemini Deep Research"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - review
  - framework-docs-consistency-review
  - gemini
  - deep-research
---

# Framework Docs Consistency Review Prompt — Gemini Deep Research
Use Gemini Deep Research.
Act as a senior framework documentation consistency analyst.
Research objective:
Conduct a source-based consistency review of the provided Allzy Framework documentation set. Identify drift, contradictions, incorrect numbering, missing cross-references, mismatched terminology, source-of-truth confusion, and V5 summary alignment issues.
Decision context:
This report will support maintenance and correction of the Allzy Framework documentation. The goal is to identify what needs to be patched, what should remain unchanged, and whether the V5 master specification accurately summarizes docs 01–09.
Scope:
- Source boundary: only the provided Allzy Framework documentation files.
- Geography: not applicable.
- Timeframe: not applicable except where the provided docs themselves define versioning or V5 alignment.
- Domain: Allzy Framework documentation consistency.
- Include: document numbering, file names, framework phases, layer model, Full / Compact / Direct terminology, Yin/Yang artifact types, no standalone Yang Compact, Triage Fast / Standard / Deep, Workspace Context Initialization, Workspace State Maintenance, Context Retrieval Builder, Document Metadata Enrichment, Metadata/frontmatter rules, Prompt Config Block rules, Search Log / Context Package / Metadata Index distinctions, Skills vs. Memory distinction, Model vs. Platform distinction, Template availability rules, and V5 summary alignment.
- Exclude: external web research, unrelated framework concepts, implementation planning, code generation, new framework rules, and rewriting documentation text.
Expected documentation set:
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

Source expectations:
Use the provided documents as the only sources. Compare claims across the provided files where possible. Do not use external websites, repository links, general knowledge, or unstated framework assumptions as evidence.

Avoid:

* unsupported claims
* invented source truth
* inferred agreement from missing docs
* treating repository links as attached template content
* treating skills/ or skills_bundle.md as source truth
* treating a Metadata Index as source truth
* creating new framework rules

Research tasks:

1. Determine whether all expected files are present and accessible.
2. Check whether document numbering and file names are consistent, especially:
    * 07_Metadata_Config_and_Retrieval_Conventions.md
    * 08_Glossary_and_Terminology.md
    * 09_Origin_and_Principles.md
3. Check whether the docs consistently use the current scope terms:
    * Full
    * Compact
    * Direct
4. Check whether the docs consistently use the valid Yin/Yang artifact types:
    * Yin Page
    * Compact Yin Page
    * Yang Core Module
    * Yin/Yang Document
    * Yin/Yang Compact
5. Check that the docs do not introduce or legitimize the invalid concept:
    * standalone Yang Compact
6. Check whether the framework phases are consistent:
    * Genesis
    * Segmentation
    * Modularization
    * Specification
    * Execution
7. Verify that Genesis is not described as creating final Yin/Yang documents or implementation code.
8. Check workspace and state distinctions:
    * Workspace Context Initialization ≠ Workspace State Maintenance
    * Workspace State Maintenance ≠ Triage
    * plan.md ≠ memory.md
    * Search Log ≠ memory.md
    * Context Package ≠ memory.md
    * context_retrieval.md ≠ Context Package
    * skills/ ≠ Memory 2.0
    * skills_bundle.md ≠ source of truth
9. Check metadata and retrieval distinctions:
    * Document Frontmatter ≠ Prompt Config Block
    * Document Metadata Enrichment ≠ Yin/Yang Conversion
    * Context Retrieval Builder ≠ only Agent-2 package
    * Metadata Index ≠ source of truth
10. Check prompt/template boundaries:

* Prompt = instruction for AI
* Template = reusable structure
* Example = filled reference
* Reference = supporting material

11. Check that repository links are not treated as attached template content.
12. Compare the V5 master specification against docs 01–09 and explain whether V5 accurately summarizes them.
13. Categorize all findings by severity:

* Critical Inconsistencies: contradictions that could cause wrong framework behavior, wrong phase execution, invalid artifact generation, or source-of-truth confusion.
* Major Inconsistencies: meaningful drift that would confuse users or implementation agents but does not immediately invalidate the whole framework.
* Minor Inconsistencies: naming, wording, cross-reference, or local alignment issues that are easy to patch and do not change core behavior.

14. Identify a recommended patch order.
15. Identify sections or files that should remain untouched.

Verification rules:

* Compare findings across provided docs where possible.
* Mark unverifiable or ambiguous findings as uncertain.
* Separate directly supported findings from interpretation.
* Identify contradictions between files explicitly.
* Do not fill missing information with unsupported assumptions.
* If a requested data point is not available in the provided docs, state that it is unavailable.
* If no issues are found in a severity table, keep the table and write None found.

Required output structure:
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
* Do not use external search.
* Do not use outside knowledge for factual claims.
* Do not treat missing docs as agreeing with present docs.
* Do not treat repository links as attached template content.
* Do not treat skills/ or skills_bundle.md as source truth.
* Do not treat a Metadata Index as source truth.
* Do not use unsupported guarantees such as “eliminate hallucinations,” “always find the truth,” or “use hundreds of sources.”
* Do not rely on broad instructions such as “never reason.” Logical synthesis is allowed only when clearly grounded in the provided docs.
* If a finding is uncertain, mark it as uncertain.
* If a claim is an inference rather than directly stated in the docs, label it as an inference.
* Prefer German explanations for the user-facing review.
* Keep file names, artifact names, identifiers, and technical terms in English.
* If the environment supports citations, cite the relevant file or section for each material finding. If citations are unavailable, name the affected files precisely.
* Do not fabricate citations, URLs, file names, line numbers, quote spans, or IDs.

Final instruction:
Base the report only on the provided documentation context. Do not fill gaps with unsupported assumptions. If information cannot be verified from the provided docs, mark it as unavailable or uncertain. Separate factual findings from interpretation. Return only the required Markdown report structure and no extra commentary.
