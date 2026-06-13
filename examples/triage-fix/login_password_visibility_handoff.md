---
id: "allzy.examples.triage-fix.login-password-visibility.handoff"
title: "Login Password Visibility Agent-2 Handoff"
artifact_type: "Example"
example_family: "Triage Fix"
sandbox_step: "08e"
status: "Stable"
version: "1.0.0"
framework_version: "5.0.2"
generated_from:
  - "examples/triage-fix/login_password_visibility_bug_intake.md"
source_demo:
  broken_html: "examples/triage-fix/login_password_visibility_broken_demo.html"
related_examples:
  fixed_html: "examples/triage-fix/login_password_visibility_fixed_demo.html"
  fix_preview: "examples/triage-fix/login_password_visibility_fix_preview.md"
tags:
  - allzy-framework
  - example
  - triage
  - handoff
  - agent-2
  - login
  - password-visibility
  - scoped-fix
---

# Login Password Visibility Agent-2 Handoff

## Purpose

This file is the Agent-2 handoff artifact for the `08e — Triage Fix` sandbox.

It demonstrates how Agent 1 turns messy bug context into a scoped implementation request.

This handoff is intentionally narrow. It does not ask Agent 2 to redesign authentication, inspect the entire repository, or change backend behavior. It gives Agent 2 enough context to fix one UI behavior while preserving scope boundaries.

## Handoff Summary

```yaml
handoff:
  task: "Fix the Login Page password visibility toggle."
  target_area: "Login Page UI"
  affected_component: "Password field and eye / visibility toggle"
  expected_result: "Password is hidden by default and can be toggled visible/hidden."
  implementation_mode: "scoped UI fix"
  source_intake: "examples/triage-fix/login_password_visibility_bug_intake.md"
  verification_required: true
```

## Observed Problem

The password field on the Login Page exposes the typed password in plain text.

Clicking the eye / visibility button does not hide the value.

Observed behavior:

```text
Password remains visible after typing.
Eye button appears interactive.
Clicking the eye button has no useful effect.
```

Expected behavior:

```text
Password is hidden by default.
Clicking the eye button reveals the password.
Clicking it again hides the password.
The button label describes the next action.
```

## Likely Affected Area

Likely affected area:

```text
Login Page password input visibility state.
```

Possible implementation causes:

```text
Password input type is hardcoded as "text".
Visibility state is missing.
Eye button does not update input type.
Eye button click handler is missing or disconnected.
Accessible label does not update with visibility state.
```

These causes are hypotheses. Agent 2 must inspect the actual source files before applying changes.

## Scope

Agent 2 may change only what is necessary to fix:

```text
Password input hidden-by-default state.
Eye button visibility toggle behavior.
Accessible label for the toggle.
Local UI feedback if already present in the component pattern.
Associated component-level tests if the project has tests.
```

## Out of Scope

Agent 2 must not change:

```text
Authentication rules
Credential validation
Password hashing
Session creation
Session storage
Rate limits
Account status decisions
Backend APIs
Database schemas
OAuth / SSO / MFA
Password reset behavior
NAS / SMB / Samba behavior
Routing outside the Login Page
Global design system tokens unless required by an existing component API
```

Do not rename unrelated files, refactor unrelated auth logic, replace the login flow, or introduce a new authentication library.

## Sources to Inspect

Agent 2 should inspect only relevant implementation files.

Likely search targets:

```yaml
sourceDiscovery:
  likely_terms:
    - "Login"
    - "Password"
    - "password"
    - "visibility"
    - "show password"
    - "hide password"
    - "Eye"
    - "EyeIcon"
    - "PasswordInput"
    - "LoginForm"

  likely_file_patterns:
    - "**/Login*.tsx"
    - "**/Login*.jsx"
    - "**/login*.tsx"
    - "**/login*.jsx"
    - "**/Password*.tsx"
    - "**/Password*.jsx"
    - "**/auth/**"
    - "**/components/**"
```

If the actual repository is unavailable, Agent 2 should produce an implementation plan or illustrative patch preview only.

## Context Sources

Agent 2 may use these context sources if available:

```yaml
contextSources:
  - path: "examples/user-login/user_login_full.md"
    reason: "Provides the full User Login/Auth specification context."

  - path: "examples/user-login/user_login_core_contract.md"
    reason: "Provides technical execution boundaries and confirms this bug must not alter auth decisions."

  - path: "examples/implementation-preview/user_login_implementation_preview.md"
    reason: "Shows the prior implementation preview that this triage bug follows."

  - path: "examples/triage-fix/login_password_visibility_bug_intake.md"
    reason: "Provides the observed bug and extracted triage signals."
```

## Implementation Constraints

Agent 2 must preserve these constraints:

```text
Password must be hidden by default.
The toggle must change only local visibility state.
The toggle must not submit the form.
The toggle must not store or transmit the password.
The toggle must not change auth/business logic.
The accessible label must describe the next action.
Keyboard focus behavior must remain usable.
```

Recommended behavior:

```yaml
recommendedBehavior:
  initial_input_type: "password"
  visible_state_false_label: "Show password"
  visible_state_true_label: "Hide password"
  state_scope: "local component state"
```

## Verification Steps

Agent 2 must verify:

```text
1. Password field renders hidden by default.
2. Typing a password does not expose the value by default.
3. Clicking the eye button reveals the value.
4. Clicking the eye button again hides the value.
5. The accessible label updates between “Show password” and “Hide password”.
6. The toggle does not submit the form.
7. No authentication rules are changed.
8. No backend files are touched unless the inspected code proves a direct dependency.
9. No unrelated UI is changed.
```

If visual verification is available:

```text
Capture or inspect a fixed Login Page state.
Confirm hidden and visible states.
```

If automated tests exist:

```text
Add or update the smallest relevant component test.
```

If tests do not exist:

```text
Report manual verification steps instead of inventing test infrastructure.
```

## Expected Output From Agent 2

Agent 2 should return:

```text
Files inspected
Files changed
Implementation summary
Verification summary
Out-of-scope confirmation
Remaining open questions
```

If no real source repository is available, Agent 2 should return:

```text
Illustrative fix preview only
No production code claim
No file-change claim
```

## Stop Conditions

Agent 2 must stop and ask or report uncertainty if:

```text
The Login Page source cannot be found.
The password field is controlled by an unknown external system.
The fix requires changing authentication contract behavior.
The fix requires global design system changes.
The bug cannot be reproduced in available sources.
The requested change conflicts with the User Login/Auth contract.
```

## Agent-2 Prompt Preview

```markdown
You are Agent 2, a scoped implementation agent.

Task:
Fix the Login Page password visibility toggle.

Observed problem:
The password remains visible in plain text, and the eye button does not hide it.

Expected behavior:
The password field is hidden by default.
The eye button toggles between visible and hidden states.
The accessible label updates between “Show password” and “Hide password”.

Scope:
Only update the Login Page password visibility UI behavior.

Out of scope:
Authentication rules, backend logic, session behavior, password validation, rate limits, account state, database schemas, OAuth/SSO/MFA, NAS/SMB behavior, and unrelated UI.

Required verification:
Confirm hidden-by-default, visible/hidden toggle, accessible label update, no form submission from the toggle, and no unrelated auth behavior changes.

Use the provided context sources and inspect only relevant implementation files.
If source files are unavailable, return an illustrative implementation preview and clearly label it as non-production.
```

## Next Artifact

```text
examples/triage-fix/login_password_visibility_fix_preview.md
```
