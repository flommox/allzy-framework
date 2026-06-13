---
id: "examples.user-login.user-login-implementation-preview"
title: "User Login & Auth — Implementation Preview"
artifact_type: "Sandbox Example Artifact"
document_role: "Implementation Preview"
status: "Demo Preview"
version: "0.1.0"
framework_version: "5.0.2"
language: "English"
technical_identifiers_language: "English"
source:
  type: "sandbox-demo-output"
  generated_from:
    - "examples/user-login/user_login_full.md"
    - "examples/user-login/user_login_core_contract.md"
    - "08c Agent Context Package preview"
related:
  sandbox: "08d — Implementation Agent"
  previous_sandbox: "08c — Metadata Retrieval / Context Package"
  next_sandbox: "08e — Triage Fix"
tags:
  - allzy-framework
  - sandbox
  - implementation-preview
  - user-login
  - functional-core
  - imperative-shell
  - agent-2-handoff
---

# User Login & Auth — Implementation Preview

## 1. Status and Safety Notice

This document is a deterministic sandbox implementation preview for the Allzy Framework website.

It is **not production-ready code**.

It demonstrates how an implementation agent could apply a selected Yin/Yang contract and a scoped context package when implementing the `User Login / Auth` segment.

The code snippets are intentionally incomplete and illustrative. They are meant to show boundaries, file organization, and implementation discipline, not to provide a drop-in authentication system.

This preview must not be presented as:

```text
production code
live AI-generated code
verified repository output
complete authentication implementation
security-audited software
```

Use this artifact only as a visible example output for:

```text
08d — Implementation Agent Sandbox
```

---

## 2. Source Inputs Used

This preview is based on the following source-backed artifacts:

```text
examples/user-login/user_login_full.md
examples/user-login/user_login_core_contract.md
08c Agent Context Package preview
```

The important source-backed constraints are:

```text
UserLoginCore is a Functional Core.
The core uses the signature: LoginResult = f(LoginConfig, LoginStateSnapshot, LoginAttemptEvent).
The Functional Core must not perform I/O.
The Functional Core must not compare password hashes.
The Functional Core must not create sessions directly.
The Functional Core must return Action objects for the Imperative Shell.
The Imperative Shell loads configuration, state, and input, then executes returned actions.
```

Important source-backed action concepts include:

```text
CREATE_SESSION
REJECT_LOGIN
RECORD_FAILED_LOGIN_ATTEMPT
LOCK_ACCOUNT
RESET_FAILED_LOGIN_COUNTER
SEND_SECURITY_NOTIFICATION
EMIT_AUDIT_EVENT
EMIT_METRIC
```

This preview does not introduce new Login/Auth rules. If a detail is missing from the source contract, it is not implemented here.

---

## 3. Implementation Goal

Implement a small illustrative skeleton for the `UserLoginCore` boundary.

The goal is to demonstrate the implementation pattern:

```text
Config + StateSnapshot + InputEvent
→ Functional Core decision
→ Functional Result with Action objects
→ Imperative Shell executes side effects outside the core
```

The preview focuses on structure:

```text
pure decision function
explicit input types
explicit result type
action object output
shell boundary
small test examples
state update notes
```

It does not implement:

```text
real password hashing
real database access
real session persistence
real email sending
real metrics backend
real audit persistence
real HTTP API routes
real UI
real deployment configuration
```

---

## 4. Simulated File Tree

The implementation agent would not modify the whole repository. It would work inside a narrow target area.

Illustrative file tree:

```text
src/
└── auth/
    └── user-login/
        ├── core/
        │   ├── login-core.ts
        │   ├── login-types.ts
        │   └── login-actions.ts
        ├── shell/
        │   └── login-shell.example.ts
        └── tests/
            └── login-core.preview.test.ts
```

These paths are demo paths. They do not claim that a real repository already contains this structure.

---

## 5. Functional Core Types Preview

File:

```text
src/auth/user-login/core/login-types.ts
```

Illustrative TypeScript preview:

```ts
export type AccountStatus = "ACTIVE" | "LOCKED" | "DISABLED";

export type LoginDecision = "APPROVED" | "REJECTED";

export type LoginReason =
  | "INVALID_CREDENTIALS"
  | "ACCOUNT_LOCKED"
  | "ACCOUNT_DISABLED"
  | "RATE_LIMITED"
  | "INVALID_EVENT"
  | null;

export interface LoginConfig {
  configVersion: 1;
  maxFailedAttempts: number;
  lockoutDurationMinutes: number;
  rateLimitWindowSeconds: number;
  rateLimitMaxAttempts: number;
  maxEventAgeSeconds: number;
  notifyOnSuspiciousLogin: boolean;
}

export interface LoginStateSnapshot {
  account: {
    accountId: string;
    identifier: string;
    status: AccountStatus;
    failedLoginAttempts: number;
    lockedAt?: string | null;
    lastLoginAt?: string | null;
  };
  rateLimitState: {
    attemptsInWindow: number;
    windowStartedAt: string;
  };
  processedEventIds: string[];
  currentTime: string;
}

export interface LoginAttemptEvent {
  schemaVersion: 1;
  eventId: string;
  eventType: "LOGIN_ATTEMPT";
  occurredAt: string;
  actor: {
    actorType: "ANONYMOUS" | "SERVICE";
  };
  payload: {
    identifier: string;
    passwordVerificationResult: boolean;
    clientMeta?: Record<string, unknown>;
  };
}

export interface LoginAction {
  type:
    | "CREATE_SESSION"
    | "REJECT_LOGIN"
    | "RECORD_FAILED_LOGIN_ATTEMPT"
    | "LOCK_ACCOUNT"
    | "RESET_FAILED_LOGIN_COUNTER"
    | "SEND_SECURITY_NOTIFICATION"
    | "EMIT_AUDIT_EVENT"
    | "EMIT_METRIC";
  priority: "HIGH" | "NORMAL" | "LOW";
  idempotencyKey: string;
  parameters: Record<string, unknown>;
}

export interface LoginResult {
  schemaVersion: 1;
  decision: LoginDecision;
  reason: LoginReason;
  outcome: "SUCCESS" | "FAILURE";
  actions: LoginAction[];
  audit: {
    eventId: string;
    accountId?: string;
    decision: LoginDecision;
    reason: LoginReason;
  };
}
```

Preview notes:

```text
The exact schema must follow the real Yang Core Module.
This file is a visible preview of the boundary, not the final source of truth.
```

---

## 6. Action Helpers Preview

File:

```text
src/auth/user-login/core/login-actions.ts
```

Illustrative TypeScript preview:

```ts
import type { LoginAction, LoginAttemptEvent, LoginStateSnapshot } from "./login-types";

export function createSessionAction(
  event: LoginAttemptEvent,
  state: LoginStateSnapshot,
): LoginAction {
  return {
    type: "CREATE_SESSION",
    priority: "HIGH",
    idempotencyKey: `${event.eventId}-CREATE_SESSION`,
    parameters: {
      accountId: state.account.accountId,
      identifier: state.account.identifier,
      clientMeta: event.payload.clientMeta ?? {},
    },
  };
}

export function resetFailedCounterAction(event: LoginAttemptEvent, accountId: string): LoginAction {
  return {
    type: "RESET_FAILED_LOGIN_COUNTER",
    priority: "HIGH",
    idempotencyKey: `${event.eventId}-RESET`,
    parameters: { accountId },
  };
}

export function recordFailedAttemptAction(event: LoginAttemptEvent, accountId: string): LoginAction {
  return {
    type: "RECORD_FAILED_LOGIN_ATTEMPT",
    priority: "HIGH",
    idempotencyKey: `${event.eventId}-FAILED_ATTEMPT`,
    parameters: { accountId },
  };
}

export function lockAccountAction(event: LoginAttemptEvent, accountId: string, lockedAt: string): LoginAction {
  return {
    type: "LOCK_ACCOUNT",
    priority: "HIGH",
    idempotencyKey: `${event.eventId}-LOCK_ACCOUNT`,
    parameters: { accountId, lockedAt },
  };
}

export function rejectLoginAction(event: LoginAttemptEvent, reason: string): LoginAction {
  return {
    type: "REJECT_LOGIN",
    priority: "HIGH",
    idempotencyKey: `${event.eventId}-REJECT_LOGIN`,
    parameters: { reason },
  };
}

export function auditAction(event: LoginAttemptEvent, decision: string, reason: string | null): LoginAction {
  return {
    type: "EMIT_AUDIT_EVENT",
    priority: "NORMAL",
    idempotencyKey: `${event.eventId}-AUDIT`,
    parameters: { decision, reason },
  };
}

export function metricAction(event: LoginAttemptEvent, outcome: string): LoginAction {
  return {
    type: "EMIT_METRIC",
    priority: "LOW",
    idempotencyKey: `${event.eventId}-METRIC`,
    parameters: { outcome },
  };
}
```

Preview notes:

```text
Actions are returned by the core.
The core does not execute these actions.
The Imperative Shell executes them after receiving LoginResult.
```

---

## 7. Functional Core Preview

File:

```text
src/auth/user-login/core/login-core.ts
```

Illustrative TypeScript preview:

```ts
import type {
  LoginAction,
  LoginAttemptEvent,
  LoginConfig,
  LoginReason,
  LoginResult,
  LoginStateSnapshot,
} from "./login-types";
import {
  auditAction,
  createSessionAction,
  lockAccountAction,
  metricAction,
  recordFailedAttemptAction,
  rejectLoginAction,
  resetFailedCounterAction,
} from "./login-actions";

export function evaluateLogin(
  config: LoginConfig,
  state: LoginStateSnapshot,
  event: LoginAttemptEvent,
): LoginResult {
  if (state.processedEventIds.includes(event.eventId)) {
    return rejected(event, state, "INVALID_EVENT", []);
  }

  if (event.eventType !== "LOGIN_ATTEMPT") {
    return rejected(event, state, "INVALID_EVENT", []);
  }

  if (state.account.status === "LOCKED") {
    return rejected(event, state, "ACCOUNT_LOCKED", [
      rejectLoginAction(event, "ACCOUNT_LOCKED"),
    ]);
  }

  if (state.account.status === "DISABLED") {
    return rejected(event, state, "ACCOUNT_DISABLED", [
      rejectLoginAction(event, "ACCOUNT_DISABLED"),
    ]);
  }

  if (state.rateLimitState.attemptsInWindow >= config.rateLimitMaxAttempts) {
    return rejected(event, state, "RATE_LIMITED", [
      rejectLoginAction(event, "RATE_LIMITED"),
    ]);
  }

  if (!event.payload.passwordVerificationResult) {
    const nextFailedAttemptCount = state.account.failedLoginAttempts + 1;
    const actions: LoginAction[] = [
      rejectLoginAction(event, "INVALID_CREDENTIALS"),
      recordFailedAttemptAction(event, state.account.accountId),
    ];

    if (nextFailedAttemptCount >= config.maxFailedAttempts) {
      actions.push(lockAccountAction(event, state.account.accountId, state.currentTime));
    }

    return rejected(event, state, "INVALID_CREDENTIALS", actions);
  }

  const actions: LoginAction[] = [
    createSessionAction(event, state),
    resetFailedCounterAction(event, state.account.accountId),
  ];

  if (config.notifyOnSuspiciousLogin && state.account.failedLoginAttempts >= 1) {
    actions.push({
      type: "SEND_SECURITY_NOTIFICATION",
      priority: "NORMAL",
      idempotencyKey: `${event.eventId}-NOTIFY`,
      parameters: {
        accountId: state.account.accountId,
        loginTimestamp: state.currentTime,
        clientMeta: event.payload.clientMeta ?? {},
      },
    });
  }

  actions.push(auditAction(event, "APPROVED", null));
  actions.push(metricAction(event, "SUCCESS"));

  return {
    schemaVersion: 1,
    decision: "APPROVED",
    reason: null,
    outcome: "SUCCESS",
    actions,
    audit: {
      eventId: event.eventId,
      accountId: state.account.accountId,
      decision: "APPROVED",
      reason: null,
    },
  };
}

function rejected(
  event: LoginAttemptEvent,
  state: LoginStateSnapshot,
  reason: Exclude<LoginReason, null>,
  domainActions: LoginAction[],
): LoginResult {
  const actions: LoginAction[] = [
    ...domainActions,
    auditAction(event, "REJECTED", reason),
    metricAction(event, "FAILURE"),
  ];

  return {
    schemaVersion: 1,
    decision: "REJECTED",
    reason,
    outcome: "FAILURE",
    actions,
    audit: {
      eventId: event.eventId,
      accountId: state.account.accountId,
      decision: "REJECTED",
      reason,
    },
  };
}
```

Preview notes:

```text
The core decides.
The core returns actions.
The core does not read/write databases.
The core does not compare password hashes.
The core does not create sessions.
The core does not emit logs directly.
```

---

## 8. Imperative Shell Boundary Preview

File:

```text
src/auth/user-login/shell/login-shell.example.ts
```

Illustrative TypeScript preview:

```ts
import { evaluateLogin } from "../core/login-core";
import type { LoginAttemptEvent, LoginConfig, LoginStateSnapshot } from "../core/login-types";

export async function handleLoginAttempt(request: unknown): Promise<unknown> {
  // Shell responsibility: validate request shape and extract credentials.
  const identifier = "user@example.com";
  const password = "redacted";

  // Shell responsibility: load config from trusted source.
  const config: LoginConfig = await loadLoginConfig();

  // Shell responsibility: find account, rate limit, dedup state, and current time.
  const state: LoginStateSnapshot = await loadLoginStateSnapshot(identifier);

  // Shell responsibility: perform credential verification outside the Functional Core.
  const passwordVerificationResult = await verifyPasswordOutsideCore(identifier, password);

  const event: LoginAttemptEvent = {
    schemaVersion: 1,
    eventId: createEventId(),
    eventType: "LOGIN_ATTEMPT",
    occurredAt: new Date().toISOString(),
    actor: { actorType: "ANONYMOUS" },
    payload: {
      identifier,
      passwordVerificationResult,
      clientMeta: {},
    },
  };

  const result = evaluateLogin(config, state, event);

  // Shell responsibility: execute only returned Action objects.
  await executeLoginActions(result.actions);

  // Shell responsibility: translate internal result into safe user-facing response.
  return toPublicLoginResponse(result);
}

async function loadLoginConfig(): Promise<LoginConfig> {
  throw new Error("Preview only: load config in real shell implementation.");
}

async function loadLoginStateSnapshot(_identifier: string): Promise<LoginStateSnapshot> {
  throw new Error("Preview only: load account/rate-limit state in real shell implementation.");
}

async function verifyPasswordOutsideCore(_identifier: string, _password: string): Promise<boolean> {
  throw new Error("Preview only: perform hash comparison outside the core.");
}

async function executeLoginActions(_actions: unknown[]): Promise<void> {
  throw new Error("Preview only: execute returned Action objects in the shell.");
}

function createEventId(): string {
  return "preview-event-id";
}

function toPublicLoginResponse(result: { decision: string }): { ok: boolean } {
  return { ok: result.decision === "APPROVED" };
}
```

Preview notes:

```text
This file intentionally contains placeholder shell functions.
The shell is where I/O belongs.
The core remains pure and deterministic.
```

---

## 9. Test Preview

File:

```text
src/auth/user-login/tests/login-core.preview.test.ts
```

Illustrative test preview:

```ts
import { evaluateLogin } from "../core/login-core";
import type { LoginConfig, LoginAttemptEvent, LoginStateSnapshot } from "../core/login-types";

const config: LoginConfig = {
  configVersion: 1,
  maxFailedAttempts: 5,
  lockoutDurationMinutes: 15,
  rateLimitWindowSeconds: 300,
  rateLimitMaxAttempts: 10,
  maxEventAgeSeconds: 60,
  notifyOnSuspiciousLogin: true,
};

const baseState: LoginStateSnapshot = {
  account: {
    accountId: "acct_123",
    identifier: "user@example.com",
    status: "ACTIVE",
    failedLoginAttempts: 0,
    lockedAt: null,
    lastLoginAt: null,
  },
  rateLimitState: {
    attemptsInWindow: 0,
    windowStartedAt: "2026-06-11T10:00:00Z",
  },
  processedEventIds: [],
  currentTime: "2026-06-11T10:01:00Z",
};

const baseEvent: LoginAttemptEvent = {
  schemaVersion: 1,
  eventId: "evt_123",
  eventType: "LOGIN_ATTEMPT",
  occurredAt: "2026-06-11T10:01:00Z",
  actor: { actorType: "ANONYMOUS" },
  payload: {
    identifier: "user@example.com",
    passwordVerificationResult: true,
  },
};

it("approves a valid login and returns session-related actions", () => {
  const result = evaluateLogin(config, baseState, baseEvent);

  expect(result.decision).toBe("APPROVED");
  expect(result.actions.map((action) => action.type)).toContain("CREATE_SESSION");
  expect(result.actions.map((action) => action.type)).toContain("RESET_FAILED_LOGIN_COUNTER");
});

it("rejects an invalid password and records failed attempt", () => {
  const result = evaluateLogin(config, baseState, {
    ...baseEvent,
    eventId: "evt_wrong_password",
    payload: {
      ...baseEvent.payload,
      passwordVerificationResult: false,
    },
  });

  expect(result.decision).toBe("REJECTED");
  expect(result.reason).toBe("INVALID_CREDENTIALS");
  expect(result.actions.map((action) => action.type)).toContain("RECORD_FAILED_LOGIN_ATTEMPT");
});

it("returns LOCK_ACCOUNT when failed attempt reaches threshold", () => {
  const result = evaluateLogin(config, {
    ...baseState,
    account: {
      ...baseState.account,
      failedLoginAttempts: 4,
    },
  }, {
    ...baseEvent,
    eventId: "evt_lockout_threshold",
    payload: {
      ...baseEvent.payload,
      passwordVerificationResult: false,
    },
  });

  expect(result.decision).toBe("REJECTED");
  expect(result.actions.map((action) => action.type)).toContain("LOCK_ACCOUNT");
});
```

Preview notes:

```text
These tests are illustrative only.
The real test suite must follow the complete test matrix from the Yang Core Module.
```

---

## 10. Verification Checklist Preview

The Implementation Agent should verify:

```text
The Functional Core is pure.
No database reads or writes occur inside the core.
No password hash comparison occurs inside the core.
No sessions are created inside the core.
No audit logs or metrics are emitted directly by the core.
All side effects are represented as Action objects.
Rejected login paths return safe, structured results.
Successful login paths return CREATE_SESSION and RESET_FAILED_LOGIN_COUNTER actions.
Failed login paths can return RECORD_FAILED_LOGIN_ATTEMPT and LOCK_ACCOUNT actions when contract conditions require them.
The shell executes actions, but does not invent business decisions.
Tests cover approved, rejected, lockout, rate-limit, disabled-account, and idempotency cases according to the real Yang contract.
```

This preview does not claim that these checks were actually executed.

---

## 11. Agent Output Summary Preview

Example implementation summary:

```markdown
## Agent Output Summary

Implemented a preview skeleton for `UserLoginCore` using the Functional Core / Imperative Shell boundary.

### Changed Preview Files

- `src/auth/user-login/core/login-types.ts`
- `src/auth/user-login/core/login-actions.ts`
- `src/auth/user-login/core/login-core.ts`
- `src/auth/user-login/shell/login-shell.example.ts`
- `src/auth/user-login/tests/login-core.preview.test.ts`

### Contract Boundaries Respected

- Functional Core performs no I/O.
- Password verification is injected as a boolean.
- Session creation is returned as an Action object.
- Account lockout is returned as an Action object.
- Audit and metrics are returned as Action objects.
- Shell owns external reads, writes, credential verification, and action execution.

### Not Implemented

- Real account store.
- Real rate-limit store.
- Real session persistence.
- Real password hashing.
- Real audit or metrics backend.
- Real HTTP route.
- Real UI.

### Verification Status

Preview only. No real tests were executed.
```

---

## 12. State Update Preview

The Implementation Agent may suggest state updates after a real implementation. In this sandbox, only a preview is shown.

### `plan.md` Preview

```markdown
- [x] User Login/Auth implementation preview reviewed
- [ ] Replace preview paths with real repository paths when implementation begins
- [ ] Run full Yang contract test matrix during real implementation
```

### `memory.md` Preview

```markdown
## Auth / User Login

Confirmed current direction:
- UserLoginCore follows Functional Core / Imperative Shell.
- Core receives LoginConfig, LoginStateSnapshot, and LoginAttemptEvent.
- Core returns LoginResult with Action objects.
- Shell performs password verification, state loading, persistence, session creation, audit, and metrics execution.

Preview caveat:
- The current implementation artifact is a sandbox preview, not production-ready code.
```

### Handoff Preview for Follow-Up

```markdown
## Follow-Up Handoff

Use the real `examples/user-login/user_login_core_contract.md` as the source of truth.
Replace illustrative paths with real repository paths.
Implement only the scoped User Login/Auth core.
Do not add OAuth, SSO, MFA, password reset, UI, NAS, SMB/Samba, or unrelated document workflows unless a later contract explicitly requires them.
```

---

## 13. Open Questions / Not Implemented

This preview intentionally leaves the following unresolved:

```text
Real repository path mapping
Actual framework/runtime setup
Actual test runner
Actual state store
Actual rate-limit store
Actual account store
Actual action execution infrastructure
Actual session persistence
Actual API route
Actual UI integration
Actual deployment/security review
```

These are implementation-workspace concerns and must be resolved when a real implementation task exists.

---

## 14. Sandbox Usage Notes

`08d` may render this artifact as:

```text
Implementation Preview Artifact
```

Desktop behavior:

```text
Open in right-side document panel.
Keep Agent Run visible in the center.
Allow collapse back to artifact stack.
```

Mobile behavior:

```text
Show inline artifact card.
Open fullscreen in SandboxMobileDocumentViewer.
Return to same agent-run position after close.
```

Completion condition for `08d`:

```text
Agent run preview completed.
Implementation preview artifact opened or acknowledged.
Verification preview shown.
State update preview shown.
```

Next sandbox:

```text
08e — Triage Fix
```

---

## 15. Quality Gate

This artifact is acceptable only if it remains clear that:

```text
It is a sandbox preview.
It is not production-ready code.
It does not claim live AI generation.
It does not claim real tests were executed.
It does not invent new Login/Auth product behavior.
It preserves Functional Core / Imperative Shell separation.
It shows how an Implementation Agent should work from scoped context.
It prepares the viewer to understand why Triage is needed later.
```
