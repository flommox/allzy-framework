---
id: "allzy.examples.triage-fix.login-password-visibility.bug-intake"
title: "Login Password Visibility Bug Intake"
artifact_type: "Example"
example_family: "Triage Fix"
sandbox_step: "08e"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
source_demo:
  broken_html: "examples/triage-fix/login_password_visibility_broken_demo.html"
related_examples:
  fixed_html: "examples/triage-fix/login_password_visibility_fixed_demo.html"
  handoff: "examples/triage-fix/login_password_visibility_handoff.md"
  fix_preview: "examples/triage-fix/login_password_visibility_fix_preview.md"
tags:
  - allzy-framework
  - example
  - triage
  - bug-intake
  - login
  - password-visibility
  - ui-bug
  - agent-1
---

# Login Password Visibility Bug Intake

## Purpose

This file is the source-backed Bug Intake artifact for the `08e — Triage Fix` sandbox.

It demonstrates how a rough, user-level bug report and a simple visual demo state can be captured before any implementation work starts.

This artifact is not a patch, not production code, and not a source modification. It preserves the observed problem, relevant UI context, messy user input, extracted triage signals, and uncertainty before Agent 1 creates a scoped handoff for Agent 2.

## Sandbox Context

```text
Sandbox: 08e — Triage Fix
Route: /sandbox/triage-fix
Visual layer: Agent Workspace Layer
Broken demo: examples/triage-fix/login_password_visibility_broken_demo.html
```

The broken demo shows a simple Login page for the Private Local Cloud / Secure Drive example.

The demo is intentionally minimal. It should look like a standalone login screen, not a triage interface. The Sandbox application may observe local demo state and create a separate Triage action outside the HTML demo.

## Related Flow

```text
08a — Idea → Master Document
08b — Master Document → Yin/Yang Artifact
08c — Metadata Retrieval / Context Package
08d — Implementation Agent
08e — Triage Fix
```

The relevant implemented area is still the User Login/Auth example. This intake focuses only on visual password visibility behavior in the Login UI.

It must not expand into authentication contract changes.

## Broken Demo State

The broken HTML demo renders:

```text
Page: Login
Product context: Private Local Cloud / Secure Drive
Email: allzy@example.de
Password field: visible input
Eye button: visible but ineffective
Sign-in: disabled in sandbox
```

Observed interaction:

```text
1. User enters a demo password.
2. The password remains visible in plain text.
3. User clicks the eye / visibility button.
4. The field does not switch to hidden mode.
5. The user can infer that the visibility toggle has no effect.
```

Important demo boundary:

```text
Do not enter a real password.
The demo input is local-only.
No data is submitted, stored, logged, or transmitted.
```

## Messy User Report

The user report intentionally sounds like a rough voice-note-style bug description:

```text
On the Login Page, the password field is broken. I can see the password in plain text, and the eye button does not change anything. It looks like the visibility toggle is not connected or the input state is wrong.
```

This is not yet a fix instruction. It is an intake signal that must be converted into a scoped triage handoff.

## Visual Evidence Summary

```yaml
visualEvidence:
  location: "Login Page"
  affected_component: "Password Field"
  affected_interaction: "Eye / visibility toggle"
  observed_problem: "Typed password remains visible in plain text."
  failed_action: "Clicking the eye button does not hide the password."
  expected_behavior: "Password should be hidden by default and toggle visible/hidden when the eye button is clicked."
  demo_email: "allzy@example.de"
  demo_password_value_policy: "Do not persist or transmit entered demo values."
```

## Extracted Triage Signals

Agent 1 should extract these signals from the messy input and visual evidence:

```yaml
triageSignals:
  location:
    value: "Login Page"
    why_it_matters: "Limits the bug to the login UI rather than the entire authentication system."

  component:
    value: "Password Field"
    why_it_matters: "Identifies the UI element where the broken behavior is observed."

  interaction:
    value: "Eye / visibility toggle"
    why_it_matters: "Identifies the user action that fails."

  observed_behavior:
    value: "Password remains visible in plain text."
    why_it_matters: "Defines the actual broken behavior."

  expected_behavior:
    value: "Password hidden by default; toggle changes hidden/visible state."
    why_it_matters: "Defines the desired result without changing authentication rules."

  likely_affected_area:
    value: "Local UI state for password input visibility."
    why_it_matters: "Suggests the probable implementation area while remaining non-final until source inspection."

  evidence_type:
    value: "Interactive HTML demo state."
    why_it_matters: "The bug is visually reproducible in the sandbox demo."
```

## Confirmed Scope

The bug appears limited to:

```text
Login Page password visibility UI behavior.
```

Confirmed scope includes:

```text
Password field visibility state.
Eye button click behavior.
Accessible label for the visibility toggle.
Visual feedback after the toggle works or fails.
```

## Out of Scope

Do not expand this bug into:

```text
Authentication rules
Password validation
Password hashing
Session handling
Rate limits
Account lockout behavior
Credential verification
Backend logic
Storage logic
Database schemas
OAuth / SSO / MFA
NAS / SMB / Samba behavior
Remote access behavior
```

If any of those areas appear relevant during implementation, Agent 2 must stop and report an open question instead of silently expanding scope.

## Unknowns / Open Questions

```yaml
openQuestions:
  - question: "Where is the real Login Page component located?"
    status: "unknown"
    owner: "Agent 2 / implementation environment"

  - question: "Is the password field controlled through local component state, form state, or a UI library component?"
    status: "unknown"
    owner: "Agent 2 / implementation environment"

  - question: "Which icon system or button component is used in the actual app?"
    status: "unknown"
    owner: "Agent 2 / implementation environment"

  - question: "Are accessibility labels already defined elsewhere?"
    status: "unknown"
    owner: "Agent 2 / implementation environment"
```

## Intake Quality Gate

This intake is usable only if it preserves:

```text
Observed problem
Location
Component
Interaction
Expected behavior
Scope boundary
Out-of-scope boundaries
Open uncertainty
```

This intake fails if it:

```text
directly patches code
changes authentication rules
claims a verified implementation
stores or repeats real passwords
turns visual evidence into unconfirmed architecture facts
```

## Next Artifact

```text
examples/triage-fix/login_password_visibility_handoff.md
```
