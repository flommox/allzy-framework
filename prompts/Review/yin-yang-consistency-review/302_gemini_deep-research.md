---
id: "allzy.framework.prompts.review.yin-yang-consistency-review.gemini-deep-research"
title: "Yin/Yang Consistency Review Prompt — Gemini Deep Research"
artifact_type: "Prompt"
prompt_family: "Review"
prompt_variant: "Yin/Yang Consistency Review"
adaptation_target: "Gemini Deep Research"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
tags:
  - allzy-framework
  - prompt
  - review
  - yin-yang-consistency-review
  - gemini
  - deep-research
---

# Yin/Yang Consistency Review Prompt — Gemini Deep Research
Use Gemini Deep Research.
Act as a senior Allzy Framework documentation review analyst.
## Research Objective
Conduct a source-based consistency review of the provided Yin, Yang, or combined Yin/Yang material.
Determine whether the artifact is internally consistent, complete, scope-safe, terminology-correct, traceable, and ready for Agent 2 implementation.
The review must identify:
1. Whether Yin and Yang match.
2. Whether human intent is preserved in the technical contract.
3. Whether the Yang contract contains enough implementation detail.
4. Whether Open Questions are missing, incorrect, or not carried over.
5. Whether Contract Gaps are missing, incorrect, or not carried over.
6. Whether scope boundaries are clear.
7. Whether Functional Core / Imperative Shell separation is respected.
8. Whether metadata and source traceability are present enough for retrieval, pairing, and implementation.
9. Whether the document uses current Allzy Framework terminology.
10. Whether the document is ready for implementation or needs revision.
## Decision Context
This review supports an Allzy Framework implementation-readiness decision.
Agent 2 should only implement from the reviewed material if the Yin/Yang artifact preserves the human intent, contains a sufficiently precise technical contract, keeps scope boundaries safe, uses current terminology, and provides enough metadata and traceability for reliable implementation.
## Scope
- Domain: Allzy Framework Yin/Yang documentation review.
- Research target: only the provided Yin, Yang, combined Yin/Yang material, and any explicitly provided related context.
- Include:
  - Yin ↔ Yang consistency
  - human intent preservation
  - Yang implementation-contract completeness
  - Open Questions
  - Contract Gaps
  - Functional Core / Imperative Shell separation
  - metadata/frontmatter traceability
  - scope safety
  - current Allzy Framework terminology
  - implementation readiness for Agent 2
- Exclude:
  - code implementation
  - code generation
  - document rewriting unless explicitly requested
  - architecture creation
  - module or submodule creation
  - API contract creation
  - database schema creation
  - implementation planning
  - execution prompt creation
  - later Allzy Framework phases
  - external web research unless explicitly supplied as part of the provided context
## Source Expectations
Use the provided Yin/Yang material as the primary source.
Use any explicitly provided supporting material only when it is attached or pasted by the user, such as:
```text
Master Document excerpt
module/submodule block
source document
metadata/frontmatter
related paired Yin/Yang document
target implementation context

Do not introduce outside sources, web knowledge, external framework assumptions, or unsupported Allzy Framework rules.

If the provided material is incomplete but still reviewable, complete the review and mark missing evidence clearly.

If no meaningful review can be produced from the available material, state the blocker and ask for the smallest missing input.

Required Inputs

The user should provide at least one of:

Yin Page
Compact Yin Page
Yang Core Module
Yin/Yang Document
Yin/Yang Compact

Valid Artifact Types

Valid:

Yin Page
Compact Yin Page
Yang Core Module
Yin/Yang Document
Yin/Yang Compact

Invalid:

standalone Yang Compact

There is no standalone Yang Compact.

Research Tasks

1. Inspect the provided material for artifact type validity.
2. Review metadata/frontmatter for retrieval, pairing, traceability, and implementation relevance.
3. Review Yin content for human intent, user value, workflows, scope, constraints, domain rules, Open Questions, and success criteria.
4. Review Yang content for implementation-contract completeness, including Functional Core, Imperative Shell, inputs, outputs, action objects, action registry, data contracts, invariants, idempotency, validation, errors, edge cases, tests, and handoff notes.
5. Compare Yin against Yang and identify mismatches, additions, omissions, lost constraints, lost business rules, unsupported assumptions, and uncopied Open Questions.
6. Identify missing or incorrect Open Questions.
7. Identify missing or incorrect Contract Gaps.
8. Evaluate whether the artifact is too broad, mixes unrelated modules, or should be split.
9. Check whether only current Allzy Framework terminology is used.
10. Decide whether Agent 2 can implement safely from the material.

Review Criteria

Metadata / Frontmatter

Check whether metadata supports retrieval and traceability.

Relevant fields include:

id
title
document_type
document_role
layer
status
version
metadata_version
tags
summary
retrieval_description
source.generated_from
source.source_block_id
scope.module_id
scope.submodule_id
yin_yang.paired_yin
yin_yang.paired_yang
retrieval.retrieval_ready
validation.uncertain_fields
validation.missing_context

Report missing fields that materially affect retrieval, pairing, or implementation.

Do not require every metadata field for small or compact artifacts.

Yin Review

Check whether Yin clearly defines:

* purpose
* human/user value
* target user
* workflows
* in-scope behavior
* out-of-scope behavior
* constraints
* domain rules
* open questions
* success criteria

Yang Review

Check whether Yang clearly defines:

* Functional Core responsibilities
* Imperative Shell responsibilities
* inputs
* outputs
* action objects
* action registry
* data contracts
* invariants
* idempotency
* validation rules
* errors
* edge cases
* tests
* implementation handoff notes

Yin ↔ Yang Alignment

Check whether:

* Yang implements what Yin asks for
* Yang adds behavior not requested by Yin
* Yin promises behavior not covered by Yang
* business rules are preserved
* constraints are preserved
* open questions are correctly carried over
* assumptions are marked

Scope Safety

Check whether:

* the artifact is too broad
* unrelated modules are mixed
* the document tries to solve multiple unrelated scopes
* the work should be split
* the artifact is Full, Compact, or Direct in practice

Current Terminology

Use only current terminology:

Full
Compact
Direct
Yin Page
Compact Yin Page
Yang Core Module
Yin/Yang Document
Yin/Yang Compact

Do not introduce old, internal, invalid, or alternative terminology.

Verification and Uncertainty Rules

Compare all relevant provided sections against each other where possible.

Separate directly supported findings from interpretation.

Mark missing evidence clearly.

Mark inferences explicitly when a finding is logically derived but not directly stated.

Identify contradictions between provided materials.

Do not fill gaps with unsupported assumptions.

Do not invent missing product decisions, technical decisions, metadata, IDs, source links, pairings, contracts, tests, or implementation details.

If a requested data point is unavailable in the provided material, state that it is unavailable.

Verdict Rules

Return exactly one verdict:

READY
NEEDS_MINOR_FIXES
NEEDS_MAJOR_FIXES
NOT_READY

Use READY only when the artifact is internally consistent, correctly scoped, uses current terminology, has sufficient traceability, and can be implemented safely by Agent 2 without material missing decisions.

Use NEEDS_MINOR_FIXES when the artifact is mostly safe but has small terminology, metadata, clarity, or formatting issues that do not block implementation.

Use NEEDS_MAJOR_FIXES when the artifact has important gaps, unclear contracts, weak Yin/Yang alignment, missing Open Questions, missing Contract Gaps, or insufficient implementation detail.

Use NOT_READY when the artifact is invalid, mixes unrelated scopes, lacks core Yin/Yang alignment, invents or omits essential behavior, uses invalid artifact types, or cannot safely guide Agent 2.

Required Output Structure

Return exactly this Markdown report structure:

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

Language Rules

Write user-facing review explanations in German.

Keep technical identifiers, artifact type names, metadata field names, section labels, and Allzy Framework terms in English.

Final Grounding Constraint

Base the review only on provided and source-supported information. Do not fill gaps with unsupported assumptions. If information cannot be verified from the provided material, mark it as unavailable or uncertain. Separate factual findings from interpretation. Do not rewrite, implement, create architecture, create later-phase framework artifacts, or generate code. Return only the required Markdown review report.
