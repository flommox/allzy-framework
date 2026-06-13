# Yin/Yang Prompt Generator

This folder contains the prompt type that generates a task-specific Agent-2 prompt for one Allzy specification artifact.

## Use This Folder First

Start with [`000_universal.md`](./000_universal.md). It is the canonical/default prompt in this folder.

## Files

- [`000_universal.md`](./000_universal.md): canonical/default provider-neutral prompt
- [`101_chatgpt_gpt-5-5.md`](./101_chatgpt_gpt-5-5.md): ChatGPT GPT-5.5 variant
- [`102_chatgpt_gpt-5-4.md`](./102_chatgpt_gpt-5-4.md): ChatGPT GPT-5.4 variant
- [`103_chatgpt_gpt-5-3-codex.md`](./103_chatgpt_gpt-5-3-codex.md): ChatGPT GPT-5.3 Codex variant
- [`201_claude.xml`](./201_claude.xml): Claude XML variant
- [`301_gemini.md`](./301_gemini.md): Gemini variant
- [`401_perplexity.md`](./401_perplexity.md): Perplexity variant

## Nearby Differences

- This prompt generates the next prompt. It does not directly produce the final Yin, Yang, or Yin/Yang artifact.
- Use [`../../Retrieval/metadata-index-generation/000_universal.md`](../../Retrieval/metadata-index-generation/000_universal.md) when the job is metadata indexing rather than specification-prompt generation.
