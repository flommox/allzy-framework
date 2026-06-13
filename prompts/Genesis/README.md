# Genesis Prompts

This folder contains the Phase 1 Genesis prompt family for turning raw product or system ideas into structured framework input.

## Use This Folder First

- Use [`full/000_universal.md`](full/000_universal.md) for broad, long-lived, or architecture-relevant ideas.
- Use [`compact/000_universal.md`](compact/000_universal.md) for smaller bounded ideas that still need structured clarification.

`000_universal.md` is the canonical/default prompt inside each concrete prompt-type folder.

## Prompt Types

| Folder | Canonical prompt | Use for |
|---|---|---|
| [`full/`](full/) | [`000_universal.md`](full/000_universal.md) | Full Genesis interview and Master Document output |
| [`compact/`](compact/) | [`000_universal.md`](compact/000_universal.md) | Compact Genesis interview and compact output |

## Nearby Differences

- `full/` is the default when the idea is broad, multi-user, stateful, or likely to expand.
- `compact/` is for smaller, lower-risk, utility-like ideas.

Universal prompts are the safe baseline. Provider/model variants may exist directly in each prompt-type folder, but treat them as ready only when the specific file or folder explicitly marks readiness. Deep Research is present only in [`full/`](full/) because that is the only Genesis prompt type in this family that currently includes [`302_gemini_deep-research.md`](full/302_gemini_deep-research.md).

## Related Resources

Looking for current platform profiles, model-specific prompt references, or additional prompt resources?  
See: https://github.com/flommox/allzy-prism-library

Note: The Prism Library is still in progress. It currently focuses on major US model/provider ecosystems and will be expanded over time with additional models, platforms, and prompt profiles.
