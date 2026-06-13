# Context Retrieval Prompt

This folder contains the prompt type for creating, inspecting, or repairing the reusable `context_retrieval.md` method file.

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

- Use [`../context-package-generation/000_universal.md`](../context-package-generation/000_universal.md) when you need selected context output for one task.
- Use [`../../../Retrieval/context-retrieval-builder/000_universal.md`](../../../Retrieval/context-retrieval-builder/000_universal.md) when the job is task-specific retrieval rather than maintaining the reusable method file.
