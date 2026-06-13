# Examples

## Purpose

`examples/` contains illustrative, source-backed Allzy Framework examples and demo payloads. Examples show completed output shape and sandbox-facing payloads.

Examples are not production apps, not templates, and not prompts. HTML demos are local browser demo artifacts, not production app code.

## Contents

| Path | What it contains | Why it is here |
|---|---|---|
| [`master-document/`](master-document/) | Master Document preview payload | Used by the Idea -> Master Document sandbox |
| [`user-login/`](user-login/) | Completed example set for one authentication module | Shows how the same module can be expressed in different artifact shapes |
| [`implementation-preview/`](implementation-preview/) | Illustrative implementation preview output | Used by the Implementation Agent sandbox |
| [`triage-fix/`](triage-fix/) | Bug intake, handoff, fix preview, and minimal HTML demo artifacts | Used by the Triage Fix sandbox |
| [`user-login/user_login_intent.md`](user-login/user_login_intent.md) | Filled Yin Page example | Human intent and domain meaning |
| [`user-login/user_login_core_contract.md`](user-login/user_login_core_contract.md) | Filled Yang Core Module example | Deterministic technical contract |
| [`user-login/user_login_full.md`](user-login/user_login_full.md) | Filled combined Yin/Yang Document example | Single-file combined specification |

## How to Use

Start with [`user-login/README.md`](user-login/README.md). If you want the fastest single-file entry point, read [`user-login/user_login_full.md`](user-login/user_login_full.md) first and then compare it with the paired Yin and Yang examples.

Use examples to understand completed artifact shape, traceability, sandbox payloads, and boundaries. Use [`../templates/`](../templates/) when creating new artifacts.

## Canonical vs Supporting

The examples are illustrative and source-backed. They are not canonical framework doctrine and do not override [`../docs/`](../docs/). Demo payloads support website and sandbox explanations.

## Optional Future Payloads

- `metadata-context-explorer/`: the website route `/examples/metadata-context-explorer` is specified, but no dedicated payload folder is required yet.

## Not Included / Do Not Confuse

- Examples are completed reference artifacts.
- Templates in [`../templates/`](../templates/) are blank reusable structures.
- Docs in [`../docs/`](../docs/) explain the rules behind the artifacts.
- HTML demos are minimal standalone demos, not production frontend code.
- `metadata-context-explorer/` is optional and should not be treated as an active example folder unless that payload folder exists.

## Related Resources

Some examples demonstrate model/platform-dependent Agent 1 / Agent 2 workflows. Looking for current platform profiles, model-specific prompt references, or additional prompt resources?  
See: https://github.com/flommox/allzy-prism-library

Note: The Prism Library is still in progress. It currently focuses on major US model/provider ecosystems and will be expanded over time with additional models, platforms, and prompt profiles.
