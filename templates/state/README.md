# State Templates

This folder contains the workspace state structure used for project continuity across sessions and agents.

## Use This Folder First

Start with [`state-management/state_management_template.md`](state-management/state_management_template.md). It is the canonical/default state template in this repository.

## What This Folder Contains

| Folder | Canonical template | Use for |
|---|---|---|
| [`state-management/`](state-management/) | [`state_management_template.md`](state-management/state_management_template.md) | `plan.md`, `memory.md`, retrieval context, and handoff state conventions |

## Nearby Differences

- State templates are for workspace continuity, not application runtime state.
- Context support templates live in [`../context/`](../context/).
- Yin, Yang, and Yin/Yang templates define specification artifacts, not state artifacts.

Related operational prompts live in [`../../prompts/Workspace/full/000_universal.md`](../../prompts/Workspace/full/000_universal.md), [`../../prompts/Workspace/maintenance/000_universal.md`](../../prompts/Workspace/maintenance/000_universal.md), and [`../../prompts/Retrieval/context-retrieval-builder/000_universal.md`](../../prompts/Retrieval/context-retrieval-builder/000_universal.md).
