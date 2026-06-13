# Triage Fix Example

## Purpose

This folder contains Triage Fix sandbox artifacts for the Login password visibility bug example.

It demonstrates an Agent 1 / Agent 2 handoff pattern: Agent 1 diagnoses the bug evidence and prepares a scoped handoff; Agent 2 executes from that handoff.

## Contents

Expected files:

- [`login_password_visibility_broken_demo.html`](./login_password_visibility_broken_demo.html)
- [`login_password_visibility_fixed_demo.html`](./login_password_visibility_fixed_demo.html)
- [`login_password_visibility_bug_intake.md`](./login_password_visibility_bug_intake.md)
- [`login_password_visibility_handoff.md`](./login_password_visibility_handoff.md)
- [`login_password_visibility_fix_preview.md`](./login_password_visibility_fix_preview.md)

A screenshot may be kept as visual reference for design/build agents. It is not required runtime behavior.

## How to Use

Use the broken demo, intake, handoff, and fix preview to understand how messy bug evidence becomes a scoped implementation handoff. Use the fixed demo only as a local browser confirmation of the intended behavior.

## Canonical vs Supporting

The Markdown artifacts are example payloads for the Triage Fix sandbox. The HTML demos are minimal standalone demo artifacts, not production app code.

## Not Included / Do Not Confuse

The broken HTML demo must not contain Sandbox/Triage UI. The Sandbox app listens externally and renders the "Send bug evidence to Triage" pop-in. The fixed HTML demo may show local success feedback.

## Related Resources

Looking for current platform profiles, model-specific prompt references, or additional prompt resources?  
See: https://github.com/flommox/allzy-prism-library

Note: The Prism Library is still in progress. It currently focuses on major US model/provider ecosystems and will be expanded over time with additional models, platforms, and prompt profiles.
