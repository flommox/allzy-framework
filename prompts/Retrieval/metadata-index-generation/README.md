# Metadata Index Generation Prompt

This folder contains the prompt type for generating metadata index artifacts from existing document metadata.

## Use This Folder First

Start with [`000_universal.md`](./000_universal.md). It is the canonical/default prompt in this folder.

## Files

- [`000_universal.md`](./000_universal.md): canonical/default provider-neutral prompt
- [`101_chatgpt_gpt-5-5.md`](./101_chatgpt_gpt-5-5.md): ChatGPT GPT-5.5 variant
- [`102_chatgpt_gpt-5-4.md`](./102_chatgpt_gpt-5-4.md): ChatGPT GPT-5.4 variant
- [`103_chatgpt_gpt-5-3-codex.md`](./103_chatgpt_gpt-5-3-codex.md): ChatGPT GPT-5.3 Codex variant
- [`201_claude.xml`](./201_claude.xml): Claude XML variant
- [`301_gemini.md`](./301_gemini.md): Gemini variant
- [`302_gemini_deep-research.md`](./302_gemini_deep-research.md): Gemini Deep Research variant
- [`401_perplexity.md`](./401_perplexity.md): Perplexity variant

## Nearby Differences

- Use [`../document-metadata-enrichment/000_universal.md`](../document-metadata-enrichment/000_universal.md) when the source documents still need frontmatter.
- Use this folder rather than any old Specification metadata-index location. The active prompt type is here in `prompts/Retrieval/metadata-index-generation/`.
