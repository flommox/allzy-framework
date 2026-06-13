# Specification Prompts

This folder contains prompts for specification-prompt generation.

## Use This Folder First

Start with [`yin-yang-prompt-generator/000_universal.md`](yin-yang-prompt-generator/000_universal.md). It is the active canonical/default prompt in this family.

## Active Prompt Type

| Folder | Canonical prompt | Use for |
|---|---|---|
| [`yin-yang-prompt-generator/`](yin-yang-prompt-generator/) | [`000_universal.md`](yin-yang-prompt-generator/000_universal.md) | Generating a task-specific Agent-2 prompt for Yin, Yang, or combined specification artifacts |

## Nearby Differences

- This family is active even though it currently has one prompt type.
- The generator creates a prompt for the next agent. It does not directly write the final specification artifact.
- If you are looking for metadata index generation, use [`../Retrieval/metadata-index-generation/`](../Retrieval/metadata-index-generation/) instead. Do not treat `Specification/metadata-index-generation/` as an active prompt type.

Universal prompts are the safe baseline. Provider/model variants may exist directly in [`yin-yang-prompt-generator/`](yin-yang-prompt-generator/), but treat them as ready only when the specific file or folder explicitly marks readiness.

## Related Resources

Looking for current platform profiles, model-specific prompt references, or additional prompt resources?  
See: https://github.com/flommox/allzy-prism-library

Note: The Prism Library is still in progress. It currently focuses on major US model/provider ecosystems and will be expanded over time with additional models, platforms, and prompt profiles.
