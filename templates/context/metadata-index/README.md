# Metadata Index Template

This folder contains the reusable shape for generated metadata index artifacts.

## Use This Folder First

Start with [`metadata_index_template.md`](./metadata_index_template.md). It is the canonical/default template in this folder.

## What This Folder Contains

- [`metadata_index_template.md`](./metadata_index_template.md): generated metadata index structure.

## Nearby Differences

- A metadata index is a generated lookup artifact.
- [`../metadata-frontmatter/metadata_frontmatter_template.md`](../metadata-frontmatter/metadata_frontmatter_template.md) lives on the source documents that the index summarizes.
- [`../search-log/search_log_template.md`](../search-log/search_log_template.md) records retrieval activity, not the index itself.

The active generation prompt is [`../../../prompts/Retrieval/metadata-index-generation/000_universal.md`](../../../prompts/Retrieval/metadata-index-generation/000_universal.md).
