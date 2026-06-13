---
id: "allzy.framework.prompts.review.framework-docs-consistency-review.perplexity"
title: "Framework Docs Consistency Review Prompt — Perplexity"
artifact_type: "Prompt"
prompt_family: "Review"
prompt_variant: "Framework Docs Consistency Review"
adaptation_target: "Perplexity"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - review
  - framework-docs-consistency-review
  - perplexity
---

# Framework Docs Consistency Review Prompt — Perplexity
## instructions
Provide a concise, evidence-grounded framework documentation consistency review.
Use German for user-facing explanations. Keep file names, artifact names, identifiers, and technical terms in English.
Only provide findings that can be verified from the provided or publicly accessible source material available to the search/retrieval system.
If reliable source material is missing or inaccessible, state that clearly instead of speculating.
Do not generate URLs in the answer. If the host application needs links, it must use the `search_results` metadata returned by Perplexity, not generated text.
Do not rewrite the documentation unless explicitly asked.
Do not invent missing framework rules.
Do not create architecture, modules, submodules, Yin/Yang documents, API contracts, database schemas, implementation plans, execution prompts, code, patches, or diffs.
If no issue is found in a severity table, keep the table and write `None found`.
Return only the required Markdown report structure.
## input
Review the Allzy Framework documentation set for internal consistency using the provided documentation files or publicly accessible indexed material for these exact files:
- `01_Philosophy.md`
- `02_Architecture.md`
- `03_Yin_Yang_Contracts.md`
- `04_Deterministic_Metadata_Graph.md`
- `05_Triage_and_Maintenance.md`
- `06_State_Management.md`
- `07_Metadata_Config_and_Retrieval_Conventions.md`
- `08_Glossary_and_Terminology.md`
- `09_Origin_and_Principles.md`
- `allzy-framework-master-specification-v5.md`
Search/retrieval objective:
Find whether the Allzy Framework docs contain drift, contradictions, incorrect numbering, missing cross-references, mismatched terminology, source-of-truth confusion, or V5 summary alignment issues.
Source boundary:
Use only the provided Allzy Framework documentation files or publicly indexed versions of those exact documentation files if the host workflow provides them. Do not use general Allzy assumptions, unrelated repositories, external framework concepts, or non-document sources as evidence.
Missing-information behavior:
If one or more expected files are missing, inaccessible, or not available in search/retrieval results, report them as missing or inaccessible. Do not infer their content. If a claim cannot be verified from available source material, mark it as unavailable or uncertain.
Check whether the docs agree on:
- document numbering
- file names
- framework phases
- layer model
- Full / Compact / Direct terminology
- Yin/Yang artifact types
- no standalone Yang Compact
- Triage Fast / Standard / Deep
- Workspace Context Initialization
- Workspace State Maintenance
- Context Retrieval Builder
- Document Metadata Enrichment
- Metadata/frontmatter rules
- Prompt Config Block rules
- Search Log / Context Package / Metadata Index distinctions
- Skills vs. Memory distinction
- Model vs. Platform distinction
- Template availability rules
- V5 summary alignment
Specific consistency checks:
1. File numbering and naming:
Check whether these file names are consistent everywhere:
- `07_Metadata_Config_and_Retrieval_Conventions.md`
- `08_Glossary_and_Terminology.md`
- `09_Origin_and_Principles.md`
2. Terminology:
Check whether the current scope terms are used consistently:
- `Full`
- `Compact`
- `Direct`
Check whether valid Yin/Yang artifact types are used consistently:
- `Yin Page`
- `Compact Yin Page`
- `Yang Core Module`
- `Yin/Yang Document`
- `Yin/Yang Compact`
Check whether the invalid concept `standalone Yang Compact` appears or is legitimized.
3. Framework phases:
Check whether the expected phases are consistent:
- `Genesis`
- `Segmentation`
- `Modularization`
- `Specification`
- `Execution`
Verify that `Genesis` is not described as creating final Yin/Yang documents or implementation code.
4. Workspace and state distinctions:
Check these distinctions:
- `Workspace Context Initialization ≠ Workspace State Maintenance`
- `Workspace State Maintenance ≠ Triage`
- `plan.md ≠ memory.md`
- `Search Log ≠ memory.md`
- `Context Package ≠ memory.md`
- `context_retrieval.md ≠ Context Package`
- `skills/ ≠ Memory 2.0`
- `skills_bundle.md ≠ source of truth`
5. Metadata and retrieval distinctions:
Check these distinctions:
- `Document Frontmatter ≠ Prompt Config Block`
- `Document Metadata Enrichment ≠ Yin/Yang Conversion`
- `Context Retrieval Builder ≠ only Agent-2 package`
- `Metadata Index ≠ source of truth`
6. Prompt, template, example, and reference boundaries:
Check these distinctions:
- `Prompt = instruction for AI`
- `Template = reusable structure`
- `Example = filled reference`
- `Reference = supporting material`
Also check that repository links are not treated as attached template content.
Severity rules:
- Critical Inconsistencies: contradictions that could cause wrong framework behavior, wrong phase execution, invalid artifact generation, or source-of-truth confusion.
- Major Inconsistencies: meaningful drift that would confuse users or implementation agents but does not immediately invalidate the whole framework.
- Minor Inconsistencies: naming, wording, cross-reference, or local alignment issues that are easy to patch and do not change core behavior.
Evidence rules:
Only provide information that can be verified from the available source material. Clearly state if details are unavailable, inaccessible, uncertain, or unsupported. Do not fabricate citations, URLs, file names, line numbers, quote spans, IDs, or source claims. Do not ask the model to generate source links.
Output shape:
Return exactly this Markdown report structure:
```markdown
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

Final constraint:
Base the report only on verified available source material for the exact Allzy Framework documentation set above. If reliable information is not available for a required check, state that clearly and mark the affected check as uncertain or unavailable. Do not include generated URLs or extra commentary outside the required report.
