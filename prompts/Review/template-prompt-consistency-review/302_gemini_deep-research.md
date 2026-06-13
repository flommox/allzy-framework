---
id: "allzy.framework.prompts.review.template-prompt-consistency-review.gemini-deep-research"
title: "Template Prompt Consistency Review Prompt — Gemini Deep Research"
artifact_type: "Prompt"
prompt_family: "Review"
prompt_variant: "Template Prompt Consistency Review"
adaptation_target: "Gemini Deep Research"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - review
  - template-prompt-consistency-review
  - gemini
  - deep-research
---

# Template / Prompt Consistency Review Prompt — Gemini Deep Research
Use Gemini Deep Research.
Act as a senior framework documentation and prompt-library consistency analyst.
## Research Objective
Conduct a source-based consistency review of the provided Allzy Framework templates, prompts, README files, and folder structure against the final Allzy Framework docs.
The goal is to determine whether the reviewed files match the final framework terminology, metadata conventions, folder structure, workflow boundaries, artifact rules, and prompt behavior.
## Decision Context
This report will support a safe maintenance or patching decision for the Allzy Framework Prompt Library.
The report must identify exactly where the library is consistent, where it drifts from the final framework docs, which issues require fixes, and whether it is safe to proceed.
This is a review task only. Do not rewrite, move, create, delete, or implement anything.
## Scope
- Domain: Allzy Framework Prompt Library consistency review
- Target materials: provided templates, prompts, README files, folder structure, and related prompt-library files
- Reference baseline: provided final Allzy Framework docs
- Geography: not applicable
- Timeframe: use only the provided materials and the current review context
- Include:
  - file names
  - folder placement
  - Full / Compact / Direct terminology
  - Yin/Yang artifact types
  - metadata/frontmatter presence
  - prompt config block conventions
  - source traceability
  - retrieval metadata
  - model/platform handling
  - Triage Fast / Standard / Deep
  - Workspace / Retrieval / Specification boundaries
  - no invalid standalone Yang Compact
  - README accuracy
- Exclude:
  - rewriting templates or prompts
  - reorganizing folders
  - creating missing files
  - deleting files
  - generating architecture
  - generating modules or submodules
  - generating Yin/Yang documents
  - generating API contracts
  - generating database schemas
  - generating implementation plans
  - generating execution prompts
  - generating code
  - performing later Allzy Framework phases
## Source Expectations
Use these final Allzy Framework docs as source of truth when provided:
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

Use the provided templates, prompts, README files, and folder structure as the target materials being checked.

Do not use outside knowledge for factual claims about the framework or reviewed files.

If one or more expected reference docs are missing, continue with the available evidence and clearly state the limitation in the report.

Research Tasks

1. Identify which final Allzy Framework docs are available and which are missing.
2. Identify which templates, prompts, README files, and folder structures are available for review.
3. Compare templates against the final framework docs for:
    * correct artifact name
    * correct frontmatter
    * correct metadata shape
    * correct source traceability
    * correct retrieval fields
    * correct scope fields
    * correct Yin/Yang fields
    * correct Open Questions / Contract Gaps handling
    * no prompt execution config stored as document metadata
4. Compare prompts against the final framework docs for:
    * correct role
    * correct task boundary
    * config-first behavior where needed
    * Assistant Mode behavior where needed
    * fallback labeling
    * model/platform separation
    * no false optimization claims
    * correct output format
    * no implementation when prompt is diagnostic, generator, or retrieval-only
5. Check folder and README consistency:
    * files are located in the correct folder
    * README files describe the actual folder contents
    * README references point to existing files
    * planned or future files are clearly marked if they do not exist
6. Check Yin/Yang artifact validity.
7. Check context and metadata distinctions.
8. Identify missing files referenced by README files.
9. Identify invalid or forbidden artifacts.
10. Compare findings across provided sources where possible.
11. Mark contradictions, missing evidence, uncertainty, and unverifiable claims clearly.
12. Produce a final structured review report with concrete required fixes.

Required Framework Rules to Check

Valid Yin/Yang Artifact Types

Yin Page
Compact Yin Page
Yang Core Module
Yin/Yang Document
Yin/Yang Compact

Invalid Yin/Yang Artifact Type

standalone Yang Compact

There must be no yang_compact template or prompt.

Expected Context Templates

metadata_frontmatter_template.md
prompt_config_block_template.md
context_package_template.md
search_log_template.md
metadata_index_template.md

Required Context / Metadata Distinctions

Document Frontmatter ≠ Prompt Config Block
Search Log ≠ memory.md
Context Package ≠ memory.md
context_retrieval.md ≠ Context Package
skills/ ≠ Memory 2.0
skills_bundle.md ≠ source of truth
Document Metadata Enrichment ≠ Yin/Yang Conversion
Context Retrieval Builder ≠ only Agent-2 Package

Verification and Uncertainty Rules

* Base the report only on provided framework docs, reviewed files, README files, folder structure, and explicit user instructions.
* Compare findings across provided sources where possible.
* Mark missing reference docs or unavailable files as missing evidence.
* Separate sourced facts from interpretation.
* If a finding is an inference rather than directly visible in the provided files, label it as an inference.
* If sources conflict, state the conflict clearly.
* Do not fill gaps with unsupported assumptions.
* Do not invent missing files, undocumented framework rules, paths, URLs, citations, IDs, or line numbers.
* If a README references a future file, mark it as planned/future, not deleted.
* If a referenced file should exist but is missing, report it clearly.
* Do not treat future or planned files as errors when they are clearly marked as planned/future.

Severity Rules

Use severity consistently:

* BLOCKING: breaks framework boundaries, creates invalid artifacts, enables wrong phase execution, or makes output unsafe to use.
* MAJOR: causes incorrect prompt/template behavior, wrong terminology, wrong artifact structure, wrong folder semantics, or misleading README guidance.
* MINOR: small inconsistency, incomplete metadata, unclear wording, or non-breaking mismatch.
* INFO: observation or planned/future note that does not require immediate correction.

Verdict Rules

Use exactly one verdict:

CONSISTENT
MOSTLY_CONSISTENT
NEEDS_MINOR_FIXES
NEEDS_MAJOR_FIXES

Use:

* CONSISTENT only when no required fixes are found.
* MOSTLY_CONSISTENT when only informational or very small non-blocking issues exist.
* NEEDS_MINOR_FIXES when issues exist but do not break framework boundaries or artifact validity.
* NEEDS_MAJOR_FIXES when issues break framework boundaries, artifact validity, metadata conventions, folder logic, README trust, or prompt/task safety.

The verdict must match the highest confirmed issue severity.

Required Output Structure

Return exactly this Markdown report structure:

# Template / Prompt Consistency Review
## Verdict
[CONSISTENT / MOSTLY_CONSISTENT / NEEDS_MINOR_FIXES / NEEDS_MAJOR_FIXES]
## Summary
[German summary.]
## Template Issues
| Issue | File | Severity | Required fix |
|---|---|---|---|
## Prompt Issues
| Issue | File | Severity | Required fix |
|---|---|---|---|
## Folder / README Issues
| Issue | Path | Severity | Required fix |
|---|---|---|---|
## Missing Files Referenced by README
| Referenced file | Referenced in | Required? | Action |
|---|---|---|---|
## Invalid / Forbidden Artifacts
| Artifact | Location | Required fix |
|---|---|---|
## Terminology Check
[PASS / FAIL + details]
## Metadata / Frontmatter Check
[PASS / FAIL + details]
## Prompt Config Check
[PASS / FAIL + details]
## Recommended Patch Plan
1. [Patch]
2. [Patch]
## Safe to Proceed?
[YES / NO + explanation]

Use German for user-facing explanations. Keep file names, paths, artifact names, prompt IDs, metadata keys, and technical identifiers in English.

If a table has no findings, include exactly one empty-state row.

For Template Issues, Prompt Issues, and Folder / README Issues, use:

| None | — | — | — |

For Missing Files Referenced by README, use:

| None | — | — | — |

For Invalid / Forbidden Artifacts, use:

| None | — | — |

Final Grounding Constraint

Base the report on provided and source-supported information. Do not fill gaps with unsupported assumptions. If information cannot be verified from the provided materials, mark it as unavailable or uncertain. Separate factual findings from interpretation and recommendations. Return only the required Markdown review report and no extra commentary after it.
