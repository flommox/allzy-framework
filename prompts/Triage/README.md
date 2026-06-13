# Triage Prompts

## Purpose

`prompts/Triage/` contains prompts that convert messy bug reports, screenshots, rough notes, or visual context into scoped Agent-2 handoffs.

Agent 1 diagnoses, gathers context, and prepares the handoff. Agent 1 does not patch code. Agent 2 executes from the scoped handoff.

## Contents

| Folder | Canonical prompt | Use for |
|---|---|---|
| [`fast/`](fast/) | [`000_universal.md`](fast/000_universal.md) | One clear low-risk issue |
| [`standard/`](standard/) | [`000_universal.md`](standard/000_universal.md) | Default maintenance intake and handoff |
| [`deep/`](deep/) | [`000_universal.md`](deep/000_universal.md) | High-risk, unclear, multi-scope, or research-heavy maintenance |

## How to Use

Use [`standard/000_universal.md`](standard/000_universal.md) first unless the situation is clearly smaller or riskier. Use universal prompts as the safe baseline. Treat provider/model variants as usable only when the specific file or folder explicitly marks readiness.

## Canonical vs Supporting

The triage output is a scoped handoff for an implementation agent, not the fix itself. Screenshots, logs, rough notes, and demo artifacts are supporting evidence.

## Not Included / Do Not Confuse

Do not use Triage prompts for greenfield ideation, direct implementation, or final code patching. Use [`../Genesis/`](../Genesis/) for new ideas and an Agent-2 implementation prompt or handoff for execution.

## Related Resources

Looking for current platform profiles, model-specific prompt references, or additional prompt resources?  
See: https://github.com/flommox/allzy-prism-library

Note: The Prism Library is still in progress. It currently focuses on major US model/provider ecosystems and will be expanded over time with additional models, platforms, and prompt profiles.
