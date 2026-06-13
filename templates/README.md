# Templates

## Purpose

`templates/` contains reusable Allzy Framework artifact structures. Templates define output shape, required sections, metadata expectations, and boundaries.

Templates are not filled examples and they are not operational prompts.

## Contents

| Folder | What it contains | Use first |
|---|---|---|
| [`yin/`](yin/) | Full and compact human-intent artifacts | [`yin/README.md`](yin/README.md) |
| [`yang/`](yang/) | Full Yang technical contract artifacts | [`yang/README.md`](yang/README.md) |
| [`yin-yang/`](yin-yang/) | Combined intent-plus-contract artifacts | [`yin-yang/README.md`](yin-yang/README.md) |
| [`context/`](context/) | Metadata, retrieval, and handoff support structures | [`context/README.md`](context/README.md) |
| [`state/`](state/) | Workspace state structures | [`state/README.md`](state/README.md) |

## How to Use

Start with the family that matches the artifact you need, then open the numbered template file inside the leaf folder. The numbered template file is the canonical structure for that artifact.

## Canonical vs Supporting

The template files define reusable structure. READMEs explain selection and boundaries. Filled artifacts belong in [`../examples/`](../examples/).

## Not Included / Do Not Confuse

- `yin/` is intent only.
- `yang/` is deterministic execution contract only.
- `yin-yang/` combines both layers in one artifact.
- `context/` supports metadata, retrieval, and task packaging.
- `state/` supports `plan.md`, `memory.md`, and workspace continuity.

There is no standalone Yang Compact template.
