# Review Prompts

This folder contains review-only prompts for consistency checks and audit-style findings.

## Use This Folder First

Choose the exact review scope first:

- [`framework-docs-consistency-review/000_universal.md`](framework-docs-consistency-review/000_universal.md) for framework documentation.
- [`template-prompt-consistency-review/000_universal.md`](template-prompt-consistency-review/000_universal.md) for prompt, template, and README consistency.
- [`yin-yang-consistency-review/000_universal.md`](yin-yang-consistency-review/000_universal.md) for Yin/Yang artifact alignment.

`000_universal.md` is the canonical/default prompt inside each concrete prompt-type folder.

## Prompt Types

| Folder | Canonical prompt | Use for |
|---|---|---|
| [`framework-docs-consistency-review/`](framework-docs-consistency-review/) | [`000_universal.md`](framework-docs-consistency-review/000_universal.md) | Docs consistency review |
| [`template-prompt-consistency-review/`](template-prompt-consistency-review/) | [`000_universal.md`](template-prompt-consistency-review/000_universal.md) | Prompt/template/README consistency review |
| [`yin-yang-consistency-review/`](yin-yang-consistency-review/) | [`000_universal.md`](yin-yang-consistency-review/000_universal.md) | Yin/Yang artifact review |

## Nearby Differences

- These prompts review and report.
- They do not directly rewrite files or implement code.
- Use the exact review type that matches the material under review.

Universal prompts are the safe baseline. Provider/model variants may exist in this family, but treat them as ready only when the specific file or folder explicitly marks readiness.

## Related Resources

Looking for current platform profiles, model-specific prompt references, or additional prompt resources?  
See: https://github.com/flommox/allzy-prism-library

Note: The Prism Library is still in progress. It currently focuses on major US model/provider ecosystems and will be expanded over time with additional models, platforms, and prompt profiles.
