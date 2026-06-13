# Context Templates

## Purpose

This folder contains support structures for metadata, retrieval, prompt configuration, Search Logs, context packages, and metadata indexes.

`templates/context/` is the context template root. There is no top-level `context/` root for these templates.

## Contents

| Folder | Canonical template | Use for |
|---|---|---|
| [`metadata-frontmatter/`](metadata-frontmatter/) | [`metadata_frontmatter_template.md`](metadata-frontmatter/metadata_frontmatter_template.md) | Describing an artifact for retrieval and classification |
| [`prompt-config-block/`](prompt-config-block/) | [`prompt_config_block_template.md`](prompt-config-block/prompt_config_block_template.md) | Execution settings inside an operational prompt |
| [`context-package/`](context-package/) | [`context_package_template.md`](context-package/context_package_template.md) | One task-specific context bundle |
| [`search-log/`](search-log/) | [`search_log_template.md`](search-log/search_log_template.md) | Retrieval audit trail |
| [`metadata-index/`](metadata-index/) | [`metadata_index_template.md`](metadata-index/metadata_index_template.md) | Generated lookup structure derived from metadata |

## How to Use

Start with the leaf folder that matches the artifact you need. The `.md` file inside that leaf folder is the canonical structure for that support artifact.

## Canonical vs Supporting

Context templates define support artifact shape. Retrieval and workspace prompts may generate or repair artifacts based on these templates.

## Not Included / Do Not Confuse

- Frontmatter describes an artifact.
- A Prompt Config Block controls how a prompt run behaves.
- A Context Package carries selected task context.
- A Search Log records how retrieval happened.
- A Metadata Index is a generated lookup artifact, not the manual source of truth.

Related prompt families live in [`../../prompts/Retrieval/`](../../prompts/Retrieval/) and [`../../prompts/Workspace/artifact-prompts/`](../../prompts/Workspace/artifact-prompts/).
