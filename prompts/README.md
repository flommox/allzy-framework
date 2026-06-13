# Prompts

## Purpose

`prompts/` contains the operational prompt families used by the Allzy Framework. These prompts drive framework workflows; they are not templates or examples.

## Contents

| Folder | What it contains | Use first |
|---|---|---|
| [`Genesis/`](Genesis/) | Phase 1 ideation and requirements-interview prompts | [`Genesis/README.md`](Genesis/README.md) |
| [`Triage/`](Triage/) | Maintenance intake and scoped Agent-2 handoff prompts | [`Triage/README.md`](Triage/README.md) |
| [`Workspace/`](Workspace/) | Workspace initialization, maintenance, state, retrieval, and support-artifact prompts | [`Workspace/README.md`](Workspace/README.md) |
| [`Retrieval/`](Retrieval/) | Metadata enrichment, metadata indexes, search logs, and context selection prompts | [`Retrieval/README.md`](Retrieval/README.md) |
| [`Specification/`](Specification/) | Specification-prompt generation prompts | [`Specification/README.md`](Specification/README.md) |
| [`Review/`](Review/) | Review-only consistency and audit prompts | [`Review/README.md`](Review/README.md) |

## How to Use

Start with the family that matches the job, then open the matching prompt-type folder and use `000_universal.md` first. Universal prompts are the safe baseline.

Provider/model variants may exist beside a universal prompt, but they must not be treated as ready unless the specific file or folder explicitly marks them ready. `201_claude.xml` is a Claude XML variant where present. `302_gemini_deep-research.md` appears only where Deep Research support is intentional. There is no `adapted/` folder.

Some workflows use Agent 1 / Agent 2 handoff patterns. When a workflow requires model/provider/platform-specific profiles, use the active prompt references or the companion Prism Library.

## Canonical vs Supporting

The canonical operational default inside each concrete prompt-type folder is `000_universal.md`. Family READMEs explain selection and boundaries. Templates define output shape in [`../templates/`](../templates/); examples show filled outputs in [`../examples/`](../examples/).

## Not Included / Do Not Confuse

`Specification/` is active, but it currently has one active prompt type: [`Specification/yin-yang-prompt-generator/`](Specification/yin-yang-prompt-generator/). Metadata index generation belongs in [`Retrieval/metadata-index-generation/`](Retrieval/metadata-index-generation/).

## Related Resources

Looking for current platform profiles, model-specific prompt references, or additional prompt resources?  
See: https://github.com/flommox/allzy-prism-library

Note: The Prism Library is still in progress. It currently focuses on major US model/provider ecosystems and will be expanded over time with additional models, platforms, and prompt profiles.
