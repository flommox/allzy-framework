---
id: "allzy.framework.prompts.review.template-prompt-consistency-review.gemini"
title: "Template Prompt Consistency Review Prompt — Gemini"
artifact_type: "Prompt"
prompt_family: "Review"
prompt_variant: "Template Prompt Consistency Review"
adaptation_target: "Gemini"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - review
  - template-prompt-consistency-review
  - gemini
---

# Template / Prompt Consistency Review Prompt — Gemini Standard
Act as a template and prompt consistency reviewer for the Allzy Framework.
## Task
Review the provided templates, prompts, README files, and folder structure for consistency with the final Allzy Framework docs.
Check whether the reviewed files match the final framework docs, terminology, metadata conventions, folder structure, and workflow boundaries.
Focus on:
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
## Context
Use the following final Allzy Framework docs as source of truth when provided:
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

Treat the reviewed templates, prompts, README files, and folder structure as the target being checked.

If one or more expected reference docs are missing, continue with the available evidence and clearly state the limitation in the report.

Use only the provided context for factual claims. You may perform logical deductions based strictly on the provided context. Do not introduce external information. If the exact answer is not supported by the provided files, state that it is not available in the provided context.

Review Areas

1. Template Checks

Check templates for:

* correct artifact name
* correct frontmatter
* correct metadata shape
* correct source traceability
* correct retrieval fields
* correct scope fields
* correct Yin/Yang fields
* correct Open Questions / Contract Gaps handling
* no prompt execution config stored as document metadata

2. Prompt Checks

Check prompts for:

* correct role
* correct task boundary
* config-first behavior where needed
* Assistant Mode behavior where needed
* fallback labeling
* model/platform separation
* no false optimization claims
* correct output format
* no implementation when prompt is diagnostic, generator, or retrieval-only

3. Folder / README Checks

Check whether:

* files are located in the correct folder
* README files describe the actual folder contents
* README references point to existing files
* planned or future files are clearly marked if they do not exist

4. Yin/Yang Checks

The following artifact types are valid:

Yin Page
Compact Yin Page
Yang Core Module
Yin/Yang Document
Yin/Yang Compact

The following artifact type is invalid:

standalone Yang Compact

There must be no yang_compact template or prompt.

5. Context / Metadata Checks

Expected context templates:

metadata_frontmatter_template.md
prompt_config_block_template.md
context_package_template.md
search_log_template.md
metadata_index_template.md

Check that templates and prompts do not confuse:

Document Frontmatter ≠ Prompt Config Block
Search Log ≠ memory.md
Context Package ≠ memory.md
context_retrieval.md ≠ Context Package
skills/ ≠ Memory 2.0
skills_bundle.md ≠ source of truth
Document Metadata Enrichment ≠ Yin/Yang Conversion
Context Retrieval Builder ≠ only Agent-2 Package

Output format

Return exactly this Markdown structure:

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

Verdict rules

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

Severity rules

Use severity consistently:

* BLOCKING: breaks framework boundaries, creates invalid artifacts, enables wrong phase execution, or makes output unsafe to use.
* MAJOR: causes incorrect prompt/template behavior, wrong terminology, wrong artifact structure, wrong folder semantics, or misleading README guidance.
* MINOR: small inconsistency, incomplete metadata, unclear wording, or non-breaking mismatch.
* INFO: observation or planned/future note that does not require immediate correction.

Constraints

* Do not rewrite files unless explicitly asked.
* Do not move files unless explicitly asked.
* Do not invent missing files.
* If a README references a future file, mark it as planned/future, not deleted.
* If a referenced file should exist but is missing, report it clearly.
* Do not treat future or planned files as errors when they are clearly marked as planned/future.
* Do not generate architecture.
* Do not generate modules or submodules.
* Do not generate Yin/Yang documents.
* Do not generate API contracts.
* Do not generate database schemas.
* Do not generate implementation plans.
* Do not generate execution prompts.
* Do not generate code.
* Do not claim consistency when evidence is missing.
* Do not report assumptions as confirmed findings.
* Do not use undocumented framework rules as findings.
* Do not treat skills_bundle.md as the source of truth.
* Do not confuse document metadata with prompt execution config.
* Do not validate any standalone Yang Compact artifact.

Final checks

Before finalizing, verify:

* Every requested review area is covered or explicitly marked as blocked by missing evidence.
* The verdict matches the highest confirmed issue severity.
* Every issue has a concrete required fix.
* Missing files referenced by README are listed separately.
* Invalid or forbidden artifacts are listed separately.
* No file rewrite, move, creation, deletion, implementation, or later framework phase was performed.
* No missing file, path, URL, source, or line number was invented.
* German explanations are used where user-facing prose is required.
* Technical identifiers remain unchanged.
* The output exactly follows the required Markdown structure.

Final instruction:
Return only the required Markdown review report. Do not include extra sections, commentary, TODOs, or explanations after the report.
