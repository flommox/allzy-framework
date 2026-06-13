# Workspace Prompts

## Purpose

`prompts/Workspace/` contains prompts that initialize or maintain task context, state, retrieval, memory, plans, and workspace helper artifacts.

## Contents

| Folder | Canonical prompt | Use for |
|---|---|---|
| [`full/`](full/) | [`000_universal.md`](full/000_universal.md) | Full workspace context initialization |
| [`maintenance/`](maintenance/) | [`000_universal.md`](maintenance/000_universal.md) | Workspace state maintenance and cleanup |
| [`artifact-prompts/`](artifact-prompts/) | Varies by leaf folder | Targeted support artifacts such as `plan.md`, `memory.md`, and context packages |

## How to Use

Use [`full/000_universal.md`](full/000_universal.md) when a workspace needs initial setup or a full rebuild. Use [`maintenance/000_universal.md`](maintenance/000_universal.md) when the workspace already exists and needs cleanup or repair. Use [`artifact-prompts/README.md`](artifact-prompts/README.md) for one specific helper artifact.

Universal prompts are the safe baseline. If workspace setup depends on model, provider, platform, or agent-profile selection, use current prompt references or the companion Prism Library.

## Canonical vs Supporting

Workspace prompts maintain execution context. They do not replace framework docs, templates, or examples. Generated state files are working artifacts, not canonical framework doctrine.

## Not Included / Do Not Confuse

Do not use Workspace prompts as product specifications or implementation instructions. They prepare and maintain the workspace around the task.

## Related Resources

Looking for current platform profiles, model-specific prompt references, or additional prompt resources?  
See: https://github.com/flommox/allzy-prism-library

Note: The Prism Library is still in progress. It currently focuses on major US model/provider ecosystems and will be expanded over time with additional models, platforms, and prompt profiles.
