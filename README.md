# Allzy Framework

This repository contains the public Allzy Framework documentation, prompts, templates, examples, and website build context.

## Start Here

1. Read [`docs/README.md`](docs/README.md) for the framework concept docs and website page mapping.
2. Read [`prompts/README.md`](prompts/README.md) to choose the right operational prompt family.
3. Read [`templates/README.md`](templates/README.md) to choose the right reusable artifact structure.
4. Read [`examples/README.md`](examples/README.md) to inspect source-backed examples and demo payloads.
5. Read [`website-context/README.md`](website-context/README.md) only when building or reviewing the public website.

## Public Structure

| Path | What it contains | Use first |
|---|---|---|
| [`docs/`](docs/) | Canonical framework concept documentation and the consolidated V5 specification | [`docs/README.md`](docs/README.md) |
| [`prompts/`](prompts/) | Operational prompts for Genesis, Triage, Workspace, Retrieval, Specification, and Review workflows | [`prompts/README.md`](prompts/README.md) |
| [`templates/`](templates/) | Reusable artifact templates that define output shape | [`templates/README.md`](templates/README.md) |
| [`examples/`](examples/) | Source-backed examples, sandbox payloads, and local demo artifacts | [`examples/README.md`](examples/README.md) |
| [`website-context/`](website-context/) | Build-supporting context for the public website | [`website-context/README.md`](website-context/README.md) |

`LICENSE.md` and `ai.txt` belong to the public root.

## Canonical vs Supporting

`docs/` is the canonical concept layer. `prompts/` contains operational prompt instructions. `templates/` contains reusable structures, not filled examples. `examples/` shows completed or preview payloads, not production products. `website-context/` explains how the public website should present the material; it is not framework doctrine.

Universal prompts remain the safe default. Provider or model variants must not be treated as ready unless the specific file or folder explicitly marks them ready.

## Not Included / Do Not Confuse

The following local/internal/supporting folders are not active public source areas and should not be described as required public repository folders:

- `Referenzen/`
- `Audits/`
- `Input/`
- `Samples/`
- `Codecs/`
- `ClaudeReview/`

Build outputs and dependency folders such as `node_modules/`, `dist/`, `build/`, `.next/`, and `.git/` are also outside the public source set.

## Related Resources

Looking for current platform profiles, model-specific prompt references, or additional prompt resources?  
See: https://github.com/flommox/allzy-prism-library

Note: The Prism Library is still in progress. It currently focuses on major US model/provider ecosystems and will be expanded over time with additional models, platforms, and prompt profiles.
