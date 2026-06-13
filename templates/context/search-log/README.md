# Search Log Template

This folder contains the reusable Search Log structure for retrieval audit trails.

## Use This Folder First

Start with [`search_log_template.md`](./search_log_template.md). It is the canonical/default template in this folder.

## What This Folder Contains

- [`search_log_template.md`](./search_log_template.md): Search Log structure for deterministic retrieval records.

## Nearby Differences

- A Search Log records what was searched, selected, excluded, and left uncertain.
- [`../context-package/context_package_template.md`](../context-package/context_package_template.md) carries the selected context itself.
- [`../metadata-index/metadata_index_template.md`](../metadata-index/metadata_index_template.md) is the generated lookup file, not the retrieval audit trail.

The related retrieval prompt is [`../../../prompts/Retrieval/context-retrieval-builder/000_universal.md`](../../../prompts/Retrieval/context-retrieval-builder/000_universal.md).
