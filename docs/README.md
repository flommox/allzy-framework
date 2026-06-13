# Documentation

## Purpose

`docs/` contains the canonical Allzy Framework concept documentation. These files explain the framework model, operating rules, terminology, and the concepts behind the prompts, templates, and examples.

The central docs map to visual website pages. They are not intended to be rendered as one raw public docs page.

## Contents

Start with [`01_Philosophy.md`](./01_Philosophy.md), then read the numbered files in order. Use [`allzy-framework-master-specification-v5.md`](./allzy-framework-master-specification-v5.md) as the consolidated V5 reference.

| File | Website route |
|---|---|
| [`01_Philosophy.md`](./01_Philosophy.md) | `/framework/philosophy` |
| [`02_Architecture.md`](./02_Architecture.md) | `/framework/architecture` |
| [`03_Yin_Yang_Contracts.md`](./03_Yin_Yang_Contracts.md) | `/framework/yin-yang` |
| [`04_Deterministic_Metadata_Graph.md`](./04_Deterministic_Metadata_Graph.md) | `/framework/metadata-graph` |
| [`05_Triage_and_Maintenance.md`](./05_Triage_and_Maintenance.md) | `/framework/triage-maintenance` |
| [`06_State_Management.md`](./06_State_Management.md) | `/framework/state-management` |
| [`07_Metadata_Config_and_Retrieval_Conventions.md`](./07_Metadata_Config_and_Retrieval_Conventions.md) | `/framework/metadata-config-retrieval` |
| [`08_Glossary_and_Terminology.md`](./08_Glossary_and_Terminology.md) | `/framework/glossary` |
| [`09_Origin_and_Principles.md`](./09_Origin_and_Principles.md) | `/origin` |

## How to Use

Humans and agents should use `docs/` as the source for framework claims, definitions, page concepts, and terminology. Website agents should translate these docs into designed pages rather than dumping the raw Markdown into a single docs page.

## Canonical vs Supporting

The numbered docs and the V5 master specification are canonical framework references. README files support navigation only. `website-context/` supports presentation and build planning, not framework doctrine.

## Not Included / Do Not Confuse

This folder does not contain prompts, templates, examples, website implementation code, or active public material from local/internal folders.
