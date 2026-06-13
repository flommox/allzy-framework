# Retrieval Prompts

## Purpose

`prompts/Retrieval/` contains prompts that prepare context packages, search logs, metadata indexes, metadata frontmatter, and context selection artifacts.

## Contents

| Folder | Canonical prompt | Use for |
|---|---|---|
| [`context-retrieval-builder/`](context-retrieval-builder/) | [`000_universal.md`](context-retrieval-builder/000_universal.md) | Task-specific retrieval and context packaging |
| [`document-metadata-enrichment/`](document-metadata-enrichment/) | [`000_universal.md`](document-metadata-enrichment/000_universal.md) | Adding or repairing metadata frontmatter |
| [`metadata-index-generation/`](metadata-index-generation/) | [`000_universal.md`](metadata-index-generation/000_universal.md) | Generating metadata index artifacts |

## How to Use

Use [`context-retrieval-builder/000_universal.md`](context-retrieval-builder/000_universal.md) when a task needs selected context. Use [`document-metadata-enrichment/000_universal.md`](document-metadata-enrichment/000_universal.md) before indexing if documents lack metadata. Use [`metadata-index-generation/000_universal.md`](metadata-index-generation/000_universal.md) when metadata exists and a lookup index is needed.

Universal prompts are the safe baseline. Retrieval prompts may be adapted to specific platforms/models only when the active prompt references or a companion profile supports that choice.

## Canonical vs Supporting

Retrieval artifacts are support structures. They help select context; they do not override canonical docs, prompt instructions, or template definitions.

## Not Included / Do Not Confuse

Metadata enrichment proposes or repairs frontmatter. Metadata index generation creates derived lookup artifacts. Context retrieval builder selects and packages context for a specific task.

## Related Resources

Looking for current platform profiles, model-specific prompt references, or additional prompt resources?  
See: https://github.com/flommox/allzy-prism-library

Note: The Prism Library is still in progress. It currently focuses on major US model/provider ecosystems and will be expanded over time with additional models, platforms, and prompt profiles.
