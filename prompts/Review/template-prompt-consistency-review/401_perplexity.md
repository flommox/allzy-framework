---
id: "allzy.framework.prompts.review.template-prompt-consistency-review.perplexity"
title: "Template Prompt Consistency Review Prompt — Perplexity"
artifact_type: "Prompt"
prompt_family: "Review"
prompt_variant: "Template Prompt Consistency Review"
adaptation_target: "Perplexity"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - review
  - template-prompt-consistency-review
  - perplexity
---

# Template / Prompt Consistency Review Prompt — Perplexity
## instructions
Provide a concise, strict, evidence-oriented review report.
Use German for user-facing explanations. Keep file names, paths, artifact names, prompt IDs, metadata keys, and technical identifiers in English.
Base findings only on the provided or publicly indexed source material available to the Perplexity workflow. Do not invent missing files, undocumented framework rules, citations, URLs, IDs, line numbers, or repository paths.
Do not ask the model to generate source URLs. If the host application needs links, use the `search_results` returned by the Perplexity API, not generated answer text.
If reliable information is missing, unavailable, inaccessible, private, not indexed, or not supported by search results, state that clearly. Do not provide speculative information.
Return exactly the required Markdown report structure. Do not add extra sections or commentary after the report.
## input
Review the Allzy Framework Prompt Library templates, prompts, README files, and folder structure for consistency with the final Allzy Framework docs.
Search and analyze publicly available or provided source material relevant to these exact Allzy Framework files and concepts:
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
- Allzy Framework templates
- Allzy Framework prompts
- Allzy Framework README files
- Allzy Framework Prompt Library folder structure
- Full / Compact / Direct terminology
- Yin/Yang artifact types
- `Yin Page`
- `Compact Yin Page`
- `Yang Core Module`
- `Yin/Yang Document`
- `Yin/Yang Compact`
- invalid standalone `Yang Compact`
- invalid `yang_compact` template or prompt
- document frontmatter
- prompt config block
- source traceability
- retrieval metadata
- model/platform handling
- `Triage Fast`
- `Triage Standard`
- `Triage Deep`
- Workspace boundaries
- Retrieval boundaries
- Specification boundaries
- `metadata_frontmatter_template.md`
- `prompt_config_block_template.md`
- `context_package_template.md`
- `search_log_template.md`
- `metadata_index_template.md`
- `Document Frontmatter ≠ Prompt Config Block`
- `Search Log ≠ memory.md`
- `Context Package ≠ memory.md`
- `context_retrieval.md ≠ Context Package`
- `skills/ ≠ Memory 2.0`
- `skills_bundle.md ≠ source of truth`
- `Document Metadata Enrichment ≠ Yin/Yang Conversion`
- `Context Retrieval Builder ≠ only Agent-2 Package`
The review task is to check whether the provided or discoverable target materials match the final Allzy Framework docs, terminology, metadata conventions, folder structure, and workflow boundaries.
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
Check templates for:
- correct artifact name
- correct frontmatter
- correct metadata shape
- correct source traceability
- correct retrieval fields
- correct scope fields
- correct Yin/Yang fields
- correct Open Questions / Contract Gaps handling
- no prompt execution config stored as document metadata
Check prompts for:
- correct role
- correct task boundary
- config-first behavior where needed
- Assistant Mode behavior where needed
- fallback labeling
- model/platform separation
- no false optimization claims
- correct output format
- no implementation when prompt is diagnostic, generator, or retrieval-only
Check folder and README consistency:
- files are located in the correct folder
- README files describe the actual folder contents
- README references point to existing files
- planned or future files are clearly marked if they do not exist
Use these valid Yin/Yang artifact types:
- `Yin Page`
- `Compact Yin Page`
- `Yang Core Module`
- `Yin/Yang Document`
- `Yin/Yang Compact`
Treat standalone `Yang Compact` as invalid. There must be no `yang_compact` template or prompt.
Expected context templates:
- `metadata_frontmatter_template.md`
- `prompt_config_block_template.md`
- `context_package_template.md`
- `search_log_template.md`
- `metadata_index_template.md`
Required context and metadata distinctions:
- `Document Frontmatter ≠ Prompt Config Block`
- `Search Log ≠ memory.md`
- `Context Package ≠ memory.md`
- `context_retrieval.md ≠ Context Package`
- `skills/ ≠ Memory 2.0`
- `skills_bundle.md ≠ source of truth`
- `Document Metadata Enrichment ≠ Yin/Yang Conversion`
- `Context Retrieval Builder ≠ only Agent-2 Package`
Do not perform any of these actions:
- rewrite templates or prompts
- move files
- reorganize folders
- create missing files
- delete files
- generate architecture
- generate modules or submodules
- generate Yin/Yang documents
- generate API contracts
- generate database schemas
- generate implementation plans
- generate execution prompts
- generate code
- treat future or planned files as errors when clearly marked as planned/future
- invent expected file contents
- infer undocumented framework rules
- claim consistency when evidence is missing
Use severity consistently:
- `BLOCKING`: breaks framework boundaries, creates invalid artifacts, enables wrong phase execution, or makes output unsafe to use.
- `MAJOR`: causes incorrect prompt/template behavior, wrong terminology, wrong artifact structure, wrong folder semantics, or misleading README guidance.
- `MINOR`: small inconsistency, incomplete metadata, unclear wording, or non-breaking mismatch.
- `INFO`: observation or planned/future note that does not require immediate correction.
Use exactly one verdict:
- `CONSISTENT`
- `MOSTLY_CONSISTENT`
- `NEEDS_MINOR_FIXES`
- `NEEDS_MAJOR_FIXES`
Use `CONSISTENT` only when no required fixes are found. Use `MOSTLY_CONSISTENT` when only informational or very small non-blocking issues exist. Use `NEEDS_MINOR_FIXES` when issues exist but do not break framework boundaries or artifact validity. Use `NEEDS_MAJOR_FIXES` when issues break framework boundaries, artifact validity, metadata conventions, folder logic, README trust, or prompt/task safety. The verdict must match the highest confirmed issue severity.
If final Allzy Framework docs, target templates, prompts, README files, folder structure, or referenced files are not publicly indexed, not provided, inaccessible, or unavailable in search results, state that limitation clearly. Do not fill gaps with unsupported assumptions.
Return exactly this Markdown report structure:
```markdown
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

If a table has no findings, include exactly one empty-state row.

For Template Issues, Prompt Issues, and Folder / README Issues, use:

| None | — | — | — |

For Missing Files Referenced by README, use:

| None | — | — | — |

For Invalid / Forbidden Artifacts, use:

| None | — | — |

Final instruction: Based on publicly available or provided source material, return only the required Markdown consistency review report. Do not include source URLs in the generated answer. If reliable information is unavailable, inaccessible, private, not indexed, or unsupported by search results, state that clearly instead of speculating.
