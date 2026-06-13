# Workspace Artifact Prompts

This folder contains targeted prompts for individual workspace support artifacts.

## Use This Folder First

Choose the artifact you need, then start with that folder's `000_universal.md`.

## Prompt Types

| Folder | Canonical prompt | Use for |
|---|---|---|
| [`plan-md/`](plan-md/) | [`000_universal.md`](plan-md/000_universal.md) | Current task plan |
| [`memory-md/`](memory-md/) | [`000_universal.md`](memory-md/000_universal.md) | Confirmed project memory |
| [`context-retrieval/`](context-retrieval/) | [`000_universal.md`](context-retrieval/000_universal.md) | Reusable retrieval method file |
| [`context-package-generation/`](context-package-generation/) | [`000_universal.md`](context-package-generation/000_universal.md) | Task-specific context package |
| [`skills-maintenance/`](skills-maintenance/) | [`000_universal.md`](skills-maintenance/000_universal.md) | Workspace skills support |

## Nearby Differences

- `plan-md/` is for current work focus.
- `memory-md/` is for lasting confirmed project truth.
- `context-retrieval/` is for the reusable retrieval method file, not one-off selected context.
- `context-package-generation/` is for one task-specific selected context package.
- `skills-maintenance/` is for workspace skills support.

Claude variants use `201_claude.xml`. Deep Research is present only in [`context-package-generation/`](context-package-generation/) within this subfamily.
