---
id: "allzy.framework.prompts.review.yin-yang-consistency-review.perplexity"
title: "Yin/Yang Consistency Review Prompt — Perplexity"
artifact_type: "Prompt"
prompt_family: "Review"
prompt_variant: "Yin/Yang Consistency Review"
adaptation_target: "Perplexity"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - review
  - yin-yang-consistency-review
  - perplexity
---

# Yin/Yang Consistency Review Prompt — Perplexity Search
## instructions
Provide a concise, structured, evidence-aware review.
Use German for user-facing review explanations.
Keep technical identifiers, metadata field names, artifact type names, and Allzy Framework terms in English.
Do not generate URLs or source links in the answer. Source URLs must be handled by the host application from Perplexity `search_results`, not generated text.
Only provide information that can be verified from the provided material or retrieved public search results. If reliable information is not found, state that clearly instead of speculating.
Do not rewrite the reviewed document unless explicitly asked.
Do not implement code.
Do not create architecture, modules, submodules, API contracts, database schemas, implementation plans, execution prompts, or code.
Do not invent missing product decisions, technical decisions, metadata, IDs, source links, pairings, contracts, tests, or traceability.
Do not treat assumptions as confirmed facts.
Return only the requested Markdown review report.
## input
Review the provided or publicly indexed Allzy Framework Yin/Yang documentation for consistency, completeness, scope safety, current terminology, metadata traceability, and implementation readiness.
Search objective:
Find and analyze information relevant to an Allzy Framework Yin/Yang consistency review. Focus on these terms and concepts: Allzy Framework, Yin Page, Compact Yin Page, Yang Core Module, Yin/Yang Document, Yin/Yang Compact, Functional Core, Imperative Shell, Open Questions, Contract Gaps, metadata frontmatter, source traceability, Agent 2 implementation readiness, Full, Compact, Direct.
Scope:
- Topic: Allzy Framework Yin/Yang documentation review.
- Material to review: the Yin, Yang, combined Yin/Yang, or related Allzy Framework context provided by the user.
- Public-source boundary: use publicly indexed information only if it is available and relevant. Do not assume access to private documents, private repositories, private chats, or unprovided files.
- Include: Yin ↔ Yang alignment, human intent preservation, Yang implementation-contract completeness, Open Questions, Contract Gaps, Functional Core / Imperative Shell separation, metadata/frontmatter traceability, scope/split safety, current Allzy Framework terminology, and Agent 2 implementation readiness.
- Exclude: code implementation, code generation, document rewriting, architecture creation, module or submodule creation, API contract creation, database schema creation, implementation planning, execution prompt creation, later Allzy Framework phases, and unrelated public web research.
Required input from the user should be at least one of:
- Yin Page
- Compact Yin Page
- Yang Core Module
- Yin/Yang Document
- Yin/Yang Compact
Optional useful context:
- Master Document excerpt
- module/submodule block
- source document
- metadata/frontmatter
- related paired Yin/Yang document
- target implementation context
Valid artifact types:
- Yin Page
- Compact Yin Page
- Yang Core Module
- Yin/Yang Document
- Yin/Yang Compact
Invalid artifact type:
- standalone Yang Compact
There is no standalone Yang Compact.
Review criteria:
1. Metadata / Frontmatter
Check whether metadata supports retrieval, pairing, traceability, and implementation.
Relevant fields:
- id
- title
- document_type
- document_role
- layer
- status
- version
- metadata_version
- tags
- summary
- retrieval_description
- source.generated_from
- source.source_block_id
- scope.module_id
- scope.submodule_id
- yin_yang.paired_yin
- yin_yang.paired_yang
- retrieval.retrieval_ready
- validation.uncertain_fields
- validation.missing_context
Report missing fields that materially affect retrieval, pairing, traceability, or implementation.
Do not require every metadata field for small or compact artifacts.
2. Yin Review
Check whether Yin clearly defines:
- purpose
- human/user value
- target user
- workflows
- in-scope behavior
- out-of-scope behavior
- constraints
- domain rules
- open questions
- success criteria
3. Yang Review
Check whether Yang clearly defines:
- Functional Core responsibilities
- Imperative Shell responsibilities
- inputs
- outputs
- action objects
- action registry
- data contracts
- invariants
- idempotency
- validation rules
- errors
- edge cases
- tests
- implementation handoff notes
4. Yin ↔ Yang Alignment
Check whether:
- Yang implements what Yin asks for
- Yang adds behavior not requested by Yin
- Yin promises behavior not covered by Yang
- business rules are preserved
- constraints are preserved
- open questions are correctly carried over
- assumptions are marked
5. Scope Safety
Check whether:
- the artifact is too broad
- unrelated modules are mixed
- the document tries to solve multiple unrelated scopes
- the work should be split
- the artifact is Full, Compact, or Direct in practice
6. Current Terminology
Use only current terminology:
- Full
- Compact
- Direct
- Yin Page
- Compact Yin Page
- Yang Core Module
- Yin/Yang Document
- Yin/Yang Compact
Do not introduce old, internal, invalid, or alternative terminology.
Missing-information behavior:
If the provided material is incomplete but still reviewable, complete the review and clearly mark missing evidence.
If no meaningful review can be produced because the user did not provide reviewable Yin/Yang material and reliable public information is not available, state that clearly and ask for the smallest missing input.
If public search results are insufficient, inaccessible, irrelevant, or do not verify a requested point, state that the information is not available from reliable public results.
Do not fill gaps with unsupported assumptions.
Verdict rules:
Return exactly one verdict:
- READY
- NEEDS_MINOR_FIXES
- NEEDS_MAJOR_FIXES
- NOT_READY
Use READY only when the artifact is internally consistent, correctly scoped, uses current terminology, has sufficient traceability, and can be implemented safely by Agent 2 without material missing decisions.
Use NEEDS_MINOR_FIXES when the artifact is mostly safe but has small terminology, metadata, clarity, or formatting issues that do not block implementation.
Use NEEDS_MAJOR_FIXES when the artifact has important gaps, unclear contracts, weak Yin/Yang alignment, missing Open Questions, missing Contract Gaps, or insufficient implementation detail.
Use NOT_READY when the artifact is invalid, mixes unrelated scopes, lacks core Yin/Yang alignment, invents or omits essential behavior, uses invalid artifact types, or cannot safely guide Agent 2.
Return exactly this Markdown structure:
# Yin/Yang Consistency Review
## Verdict
[READY / NEEDS_MINOR_FIXES / NEEDS_MAJOR_FIXES / NOT_READY]
## Summary
[Short German summary of the result.]
## Critical Issues
| Issue | Location | Why it matters | Required fix |
|---|---|---|---|
## Major Issues
| Issue | Location | Why it matters | Recommended fix |
|---|---|---|---|
## Minor Issues
| Issue | Location | Recommended fix |
|---|---|---|
## Yin ↔ Yang Alignment
[Explain whether Yin and Yang match.]
## Open Questions Missing or Incorrect
- [Question]
## Contract Gaps Missing or Incorrect
- [Gap]
## Scope / Split Recommendation
[State whether the artifact is correctly scoped.]
## Metadata / Traceability Review
[State what is missing or correct.]
## Terminology Check
[PASS / FAIL + details]
## Implementation Readiness
[Explain whether Agent 2 can implement from this safely.]
## Recommended Next Step
[Patch document / ask user / split scope / ready for implementation]
If there are no items for an issue table, write one row stating that no issue of that severity was found.
Do not add sections outside this structure.
Final instruction:
Base the review on the provided material and reliable publicly indexed information only. Do not ask for URLs. Do not generate source links. Do not invent missing Allzy Framework decisions or private context. If reliable information is missing or unverifiable, mark it as unavailable or uncertain. Return only the required Markdown review report.
