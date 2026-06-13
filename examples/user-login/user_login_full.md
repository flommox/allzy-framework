---
id: "allzy.examples.auth.user-login.yin-yang-document"
title: "User Login & Auth — Yin/Yang Document"
artifact_type: "Example"
document_type: "Yin/Yang Document"
document_role: "Filled Example"
layer: "System"
status: "Draft"
version: "0.1.0"
framework_version: "5.0.2"
metadata_version: "1.0.0"
created: "2026-06-06"
updated: "2026-06-07"
language: "English"
technical_identifiers_language: "English"
tags:
  - example
  - yin-yang
  - yin-yang-document
  - user-login
  - authentication
  - allzy-framework
aliases: []
summary: "Example Yin/Yang Document for the User Login & Auth module. Contains both the complete Yin Page (human intent, domain rules, workflows, data concepts) and the complete Yang Core Module (API schemas, decision logic, action registry, test cases, trace map) in a single file."
retrieval_description: "Retrieve this example when learning how to write a combined Yin/Yang Document, or when looking for a complete, filled example of both the Yin Page and Yang Core Module for an authentication or login module."
source:
  generated_from_template: "Templates/yin-yang/yin-yang-document/04_yin_yang_template.md"
  framework_references:
    - "Docs/07_Metadata_Config_and_Retrieval_Conventions.md"
    - "Docs/08_Glossary_and_Terminology.md"
scope:
  domain: "authentication"
  module_id: "auth.user-login"
yin_yang:
  is_yin_yang_document: true
  yin_document: "allzy.examples.auth.user-login.yin-page"
  yang_document: "allzy.examples.auth.user-login.yang-core-module"
  paired_yin: "allzy.examples.auth.user-login.yin-page"
  paired_yang: "allzy.examples.auth.user-login.yang-core-module"
  paired_yin_file: "Examples/user-login/user_login_intent.md"
  paired_yang_file: "Examples/user-login/user_login_core_contract.md"
retrieval:
  retrieval_ready: true
  retrieval_confidence: "high"
  retrieval_priority: "supporting"
  preferred_retrieval_keys:
    - "auth.user-login"
    - "user-login-full-example"
    - "yin-yang-document-example"
  excluded_from_retrieval: false
  exclusion_reason: ""
contract:
  schema_version: "1.0.0"
  config_version: "1"
  core_signature: "LoginResult = f(LoginConfig, LoginStateSnapshot, LoginAttemptEvent)"
  idempotency_anchor: "InputEvent.eventId"
  action_registry_defined: true
  decision_matrix_defined: true
  preflight_gap_check_passed: true
validation:
  metadata_inferred: false
  uncertain_fields: []
  missing_context: []
  needs_human_review: false
  validation_notes: []
---

# User Login & Auth — Yin Page

**Yin output language:** `English`  
**Module ID:** `auth.user-login`  
**Submodule ID:** Not applicable  
**Layer:** `System`  
**Version:** `0.1.0`  
**Status:** `Draft`  
**Owner:** Platform / Auth Team  
**Last updated:** 2026-06-07  
**Paired Yang document:** `allzy.examples.auth.user-login.yang-core-module`

---

## 1. Short Description

This module handles the core email-and-password login flow: it validates credentials, checks account
status, enforces rate limits, creates a session on success, and records every attempt for audit and
security purposes. It is the entry point for all human users authenticating to the platform.

---

## 2. Purpose and Product Meaning

### 2.1 Concept and Objective

User Login & Auth is the gatekeeper between an anonymous visitor and an authenticated session. Its
job is to answer one question reliably: *is this person who they claim to be, and are they allowed
to proceed right now?*

The module receives an identifier (email address) and the result of a password verification check.
It evaluates the request against the current state of the account — including whether the account
is active, whether it is temporarily locked due to repeated failures, and whether the request
exceeds the allowed rate limit for the requesting client. If every check passes, it signals the
system to create a session. If any check fails, it rejects the attempt with a clear, specific
reason, records the failure for audit, and — where warranted — triggers a security notification.

The module does not store passwords, does not perform the cryptographic password hash comparison
itself (that result is injected as an already-evaluated fact), and does not manage sessions
directly. It is a pure decision engine: it receives facts and produces decisions.

### 2.2 Problem and Motivation

Before this module existed, login logic was scattered across multiple layers of the application:
rate-limit checks happened in the API gateway, account status checks happened in a service function,
and audit events were emitted inconsistently — or not at all. The result was a system that was hard
to reason about, hard to test, and difficult to audit after security incidents.

This module centralises all login-decision logic into a single, deterministic, testable unit. Any
change to login policy — a new lockout threshold, a new account status type, a different rate-limit
window — is made in one place and is immediately reflected everywhere the module is used.

---

## 3. Target Audience

| Audience / Actor | Need or expectation | Context |
|---|---|---|
| `ANONYMOUS` end user | Needs a safe, clear, and reliable login flow using email and password | Before authentication, the user has no session and cannot access protected resources |
| Account holder | Needs protection against brute-force attempts, account enumeration, and suspicious login patterns | Security behavior must be strong without exposing internal account state |
| Platform operator | Needs auditable login decisions and predictable handling of failed attempts, lockouts, and rate limits | Used for security review, debugging, incident analysis, and compliance support |
| Imperative Shell | Needs deterministic Action objects that can be executed without duplicating login decision logic | Executes session creation, failed-attempt recording, lockout, audit, metrics, and notifications |

---

## 4. Core Value

This module centralizes login decision logic into one deterministic, auditable contract. It reduces scattered authentication behavior, prevents account-state leakage, and gives implementation agents a clear boundary between pure decision logic and side-effect execution.

The main value is not only successful authentication. The module also ensures that failed authentication is handled consistently, securely, and without exposing sensitive account information to the client.

---

## 5. Main Capabilities

| Capability | Description | Practical example | Status |
|---|---|---|---|
| Credential validation | Evaluates the password verification result provided by the shell and produces an approved or rejected decision | A user submits their password; the shell performs the hash comparison and passes `passwordVerificationResult: true` to the core, which returns `APPROVED` | `Active` |
| Account status enforcement | Checks whether the account is `ACTIVE`, `LOCKED`, or `DISABLED` before allowing login | If a user's account was locked after repeated failures, the core receives `status: LOCKED` and rejects the attempt with `ACCOUNT_LOCKED`, without evaluating the password | `Active` |
| Rate limiting | Prevents brute-force attacks by counting failed attempts within a configurable time window per identifier | If the configured `rateLimitMaxAttempts` is 10 and the identifier has 10 attempts in the current window, the core returns `RATE_LIMIT_EXCEEDED` | `Active` |
| Session creation signal | Returns an action for the shell to create an authenticated session on successful login | On `APPROVED`, the core returns a `CREATE_SESSION` action with the account ID and client metadata; the shell then issues the session token | `Active` |
| Failed-attempt recording | Returns an action to increment the failed-attempt counter stored in the data layer | On `REJECTED` with `INVALID_CREDENTIALS`, the core returns `RECORD_FAILED_LOGIN_ATTEMPT` so the shell can increment the counter in the account store | `Active` |
| Counter reset on success | Returns an action to reset the failed-attempt counter when a login succeeds | After a successful login following two prior failures, the core returns `RESET_FAILED_LOGIN_COUNTER` to clear the counter | `Active` |
| Security notification | Returns an action to send a notification to the account holder after a suspicious login pattern is detected | When `notifyOnSuspiciousLogin: true` and the account had prior failed attempts, the core returns `SEND_SECURITY_NOTIFICATION` | `Active` |
| Full audit trail | Records every decision step in a structured audit log attached to the result | Every login attempt — successful or failed — produces a structured `auditLog` array with one entry per pipeline step, attached to `FunctionalResult` | `Active` |
| Idempotent processing | Re-submitting the same login event produces no duplicate side effects | If the same `eventId` is submitted twice, the second call returns `REJECT_DUPLICATE` with no actions emitted | `Active` |

---

## 6. Domain Logic / Business Rules

| Rule | Meaning | Example | Priority |
|---|---|---|---|
| Generic client-facing failure | The user must not receive different error messages for wrong password, unknown account, locked account, or disabled account | The UI may show "email or password is incorrect" while internal logs record `ACCOUNT_LOCKED` | `Required` |
| Core does not verify passwords | The password hash comparison is performed before the core is called; the core receives only `passwordVerificationResult` | The core evaluates `true` or `false`, never a raw password or password hash | `Required` |
| Core does not create sessions directly | Session creation is a side effect owned by the Imperative Shell | The core returns `CREATE_SESSION`; the shell creates the actual session | `Required` |
| Core decides lockout need | When a failed login reaches the lockout threshold, the core must return a `LOCK_ACCOUNT` action; the shell only executes it | If `failedLoginAttempts + 1 >= maxFailedAttempts`, the result includes `LOCK_ACCOUNT` | `Required` |
| Time is injected | Time-dependent checks use `StateSnapshot.currentTime`, never direct system time access | Lockout expiry and event age are calculated from injected time | `Required` |
| Duplicate submissions are safe | Reprocessing the same `eventId` must not create duplicate sessions, counters, audit entries, or notifications | A duplicate login event returns `REJECT_DUPLICATE` and no side-effect actions | `Required` |
| Client metadata is not decision logic | Client metadata may be passed to session/audit actions, but the core does not evaluate IP or user-agent for this module | Risk scoring belongs to a separate security module | `Required` |

---

## 7. Workflows

### 7.1 Workflow Overview

| Workflow | Trigger | Actor | Outcome |
|---|---|---|---|
| Successful login | User submits correct credentials, account active, rate limit not exceeded | End user | Session created, failed-attempt counter reset, audit event emitted |
| Failed login — wrong credentials | User submits incorrect password | End user | Attempt recorded, audit event emitted, no session |
| Failed login — account locked | User attempts login while account is temporarily locked | End user | Request rejected with `ACCOUNT_LOCKED` reason, audit event emitted |
| Failed login — account disabled | User attempts login while account is permanently disabled | End user | Request rejected with `ACCOUNT_DISABLED` reason, audit event emitted |
| Rate limit exceeded | Too many attempts from the same identifier in the configured window | End user or automated script | Request rejected with `RATE_LIMIT_EXCEEDED`, audit event emitted |

### 7.2 Successful Login Workflow

1. The user submits their email address and password through the login form.
2. The API layer performs the password hash comparison and passes the binary result (`true` / `false`) to the Login Core along with the account's current state snapshot.
3. The Login Core validates the request, confirms the account is active, confirms the rate limit has not been exceeded, and confirms the password verification result is `true`.
4. The core returns a `SUCCESS` result with an `APPROVED` decision and an ordered list of actions.
5. The Imperative Shell executes the actions: it creates a session, resets the failed-attempt counter, emits an audit event, and emits a metric.
6. The API layer receives the session token and returns it to the user's browser.

> **Edge case:** If the account's failed-attempt counter is at the threshold and the password is
> correct, the counter is still reset and a session is created. A correct password clears the
> failed-attempt history.

### 7.3 Failed Login — Credential Error Workflow

1. The user submits their email address and an incorrect password.
2. The API layer performs the hash comparison, which returns `false`, and passes this to the Login Core.
3. The Login Core registers the failed verification and increments the conceptual failure count.
4. If the new failure count reaches the lockout threshold defined in configuration, the core returns a `LOCK_ACCOUNT` action for the shell to execute.
5. The core returns a `FAILURE` result with a `REJECTED` decision and reason `INVALID_CREDENTIALS`.
6. The Imperative Shell records the failed attempt, optionally locks the account, and emits an audit event.
7. The API layer returns a generic "invalid email or password" error to the user (the specific reason must not be disclosed to the client).

> **Edge case:** The reason returned to the client must always be a generic credential error message,
> regardless of whether the specific failure reason is a wrong password, an unknown email address,
> or a locked account. Revealing the specific reason leaks account existence and lock state.

### 7.4 Account Locked Workflow

1. The user attempts to log in to an account that has reached the maximum failed-attempt threshold.
2. The Login Core reads the account status from the state snapshot and finds `LOCKED`.
3. If the lockout duration has not yet elapsed (comparing the lock timestamp against the injected current time), the core rejects the attempt immediately without evaluating the password.
4. The core returns a `FAILURE` result with a `REJECTED` decision and reason `ACCOUNT_LOCKED`.
5. No session is created. No password check is performed. One audit event is emitted.

> **Edge case:** If the lockout duration has elapsed (the lock has expired), the shell is
> responsible for resetting the account status to `ACTIVE` before the next login attempt is
> processed by the core. This reset is triggered by a separate housekeeping workflow, not by the
> login module itself.

---

## 8. UI / Interaction Meaning

### 8.1 Screens / Views

| View name | Purpose | Primary actor | Notes |
|---|---|---|---|
| Login page | User enters email and password | End user | Generic error message only — never disclose specific failure reason |
| Session expired screen | Informs the user their session has ended | End user | Includes a link back to the login page |
| Account locked notice | Informs the user their account is temporarily locked | End user | Should display the approximate unlock time without exposing internal lock state |

### 8.2 Key UI Concepts

- **Generic error message:** The login form must always show the same error message regardless of the specific failure reason (wrong password, unknown account, locked account). This prevents account enumeration attacks.
- **Rate-limit feedback:** When a rate limit is exceeded, the UI may show a "too many attempts, please wait" message without specifying the exact cooldown period.
- **Lockout notice:** If the account is locked, the UI shows a friendly notice with an approximate wait time. It must not reveal the exact lockout mechanism or threshold values.
- **Loading state:** The submit button is disabled during processing to prevent duplicate submissions. The idempotency mechanism in the core handles the rare case where a duplicate does reach the server.

### 8.3 States and Feedback

| State | What the user sees |
|---|---|
| Login in progress | Submit button disabled, spinner visible |
| Login success | Redirect to post-login destination |
| Invalid credentials | Generic "email or password is incorrect" message |
| Account locked | "Your account is temporarily locked. Please try again later." |
| Account disabled | "Your account has been disabled. Please contact support." |
| Rate limit exceeded | "Too many login attempts. Please wait before trying again." |
| Service unavailable | Generic error with retry prompt (shell-level fallback, not core) |

---

## 9. Data Concepts and Field Definitions

### 9.1 Account

The Login Core receives a snapshot of the relevant account fields. It does not write to the account record directly; it returns actions for the shell to execute.

| Field | Type | Required | Meaning | Validation / constraint | Example |
|---|---|---:|---|---|---|
| `accountId` | string (uuid) | Yes | Unique identifier for the account | Must be a valid UUID v4; immutable after creation | `"550e8400-e29b-41d4-a716-446655440000"` |
| `identifier` | string | Yes | The email address used as the login identifier | Non-empty string; used for consistency check against input payload | `"alex.chen@example.com"` |
| `status` | enum | Yes | Current account status | Must be one of: `ACTIVE`, `LOCKED`, `DISABLED` | `"ACTIVE"` |
| `failedLoginAttempts` | integer | Yes | Number of consecutive failed login attempts since last successful login | Must be ≥ 0; reset to 0 on successful login | `2` |
| `lockedAt` | string (date-time) | No | UTC timestamp when the account was locked. Null if not locked. | Required when `status == LOCKED`; null when `status == ACTIVE` or `DISABLED` | `"2026-06-06T14:32:00Z"` |
| `lastLoginAt` | string (date-time) | No | UTC timestamp of the last successful login. Null if never logged in. | Null for accounts that have never logged in successfully | `"2026-06-05T09:11:00Z"` |

**Enum values for `status`:**

| Value | Meaning |
|---|---|
| `ACTIVE` | Account is in good standing and eligible for login |
| `LOCKED` | Account has been temporarily locked due to repeated failed attempts. Eligible for unlock after the configured lockout duration. |
| `DISABLED` | Account has been permanently disabled by an administrator. Cannot log in until re-enabled by an admin action. |

### 9.2 RateLimitState

The Login Core receives a pre-loaded rate-limit state for the requesting identifier. It does not query the rate-limit store directly.

| Field | Type | Required | Meaning | Validation / constraint | Example |
|---|---|---:|---|---|---|
| `identifier` | string | Yes | The email or client key for which this rate-limit state applies | Must match `payload.identifier` from the login event | `"alex.chen@example.com"` |
| `attemptsInWindow` | integer | Yes | Number of login attempts recorded in the current rate-limit window | Must be ≥ 0; compared against `Config.rateLimitMaxAttempts` | `3` |
| `windowStartedAt` | string (date-time) | Yes | UTC timestamp when the current rate-limit window began | Used to determine if the rate-limit window has expired | `"2026-06-06T14:00:00Z"` |

### 9.3 Session

The core signals the shell to create a session by returning a `CREATE_SESSION` action. The shell owns session creation and token generation.

| Field | Type | Required | Meaning | Validation / constraint | Example |
|---|---|---:|---|---|---|
| `sessionId` | string (uuid) | Yes | Unique identifier for the session | Must be a valid UUID v4; generated by the shell | `"7f4e9b2c-1a3d-4f6e-8b9c-0d2e4f6a8b0c"` |
| `accountId` | string (uuid) | Yes | The account this session belongs to | Must match the `accountId` from the login attempt | `"550e8400-e29b-41d4-a716-446655440000"` |
| `createdAt` | string (date-time) | Yes | UTC timestamp of session creation | Set by the shell at the moment of `CREATE_SESSION` execution | `"2026-06-06T14:32:05Z"` |
| `expiresAt` | string (date-time) | Yes | UTC timestamp when the session expires | Computed as `createdAt + $ENV_SESSION_EXPIRY_SECONDS` | `"2026-06-07T14:32:05Z"` |
| `clientMeta` | object | No | Optional metadata about the requesting client: `userAgent`, `ipAddress` | Privacy-sensitive; handling must comply with applicable privacy regulations | `{"userAgent": "Mozilla/5.0", "ipAddress": "203.0.113.1"}` |

---

## 10. Roles, Permissions, Privacy, and Safety

| Role | Expected access / capability | Restriction | Notes |
|---|---|---|---|
| `ANONYMOUS` | May submit a login attempt | Cannot access any authenticated resource; cannot read account state | The core treats all login attempts as anonymous until a session is created |
| `USER` | Has an active session; may use authenticated features | Cannot access other users' accounts or admin functions | Post-login role |
| `ADMIN` | May disable or re-enable accounts; may view audit logs | Cannot bypass the login flow to create sessions directly | Admin actions use separate module contracts |

### 10.1 Security Considerations

- **Password hash comparison is never performed inside the Login Core.** The API layer or a dedicated credential-verification service performs the comparison and injects the boolean result. This keeps the core free of cryptographic dependencies and ensures the password hash is never passed through the core's input pipeline.
- **Failure reasons must not be disclosed to the client.** The specific reason for rejection (`INVALID_CREDENTIALS`, `ACCOUNT_LOCKED`, `ACCOUNT_DISABLED`) is available in the structured result for internal use, audit, and logging. The API response to the client must always be a generic message.
- **All login decisions are audited.** Every decision step — including successful logins, rejections, and duplicate detections — is recorded in the structured audit log attached to the result.
- **The core never reads system time directly.** Current time is injected via the state snapshot, making time-dependent decisions fully deterministic and testable.
- **No credentials, tokens, or secrets pass through any Yin/Yang document.** All sensitive values are referenced by environment variable names only.
- Environment variables required by this module (names only, no values):
  - `$ENV_SESSION_SECRET` — Used by the Imperative Shell to sign session tokens
  - `$ENV_SESSION_EXPIRY_SECONDS` — Used by the shell to calculate session expiry

### 10.2 Compliance Notes

- Failed login attempts and their outcomes must be retained in the audit log for a minimum period defined by applicable data-retention policy (configured at the infrastructure level, not in this module).
- The `clientMeta` field may contain IP address data. Handling of this data must comply with applicable privacy regulations. The Login Core does not process `clientMeta` beyond passing it through to the `CREATE_SESSION` action — it does not evaluate or log IP addresses directly.

---

## 11. Integrations and Dependencies

| Dependency | Type | Purpose | Required |
|---|---|---|---|
| `auth.credential-verifier` | Internal module | Performs the password hash comparison and injects the boolean result | Yes |
| `auth.session-manager` | Internal module | Executes the `CREATE_SESSION` action and generates session tokens | Yes |
| `auth.account-store` | Internal module / data layer | Source of the account state snapshot injected into the core | Yes |
| `auth.rate-limit-store` | Internal module / data layer | Source of the rate-limit state snapshot injected into the core | Yes |
| `platform.audit-log` | Internal service | Receives `EMIT_AUDIT_EVENT` actions from the Imperative Shell | Yes |
| `platform.metrics` | Internal service | Receives `EMIT_METRIC` actions from the Imperative Shell | Recommended |
| `platform.notification-service` | Internal service | Executes `SEND_SECURITY_NOTIFICATION` actions | Recommended |

### 11.1 Upstream Dependencies

- `auth.credential-verifier` — provides the `passwordVerificationResult` boolean injected into the input event payload
- `auth.account-store` — provides the `account` object in the state snapshot
- `auth.rate-limit-store` — provides the `rateLimitState` object in the state snapshot

### 11.2 Downstream Dependents

- `auth.session-manager` — depends on the `CREATE_SESSION` action to issue a valid session token
- All authenticated modules — depend on a valid session created by this module's success path
- `platform.audit-log` — depends on `EMIT_AUDIT_EVENT` actions to maintain the security audit trail

---

## 12. Out of Scope

This module does not handle:

- OAuth login
- SSO login
- multi-factor authentication
- password reset
- account registration
- billing checks
- tenant-level authorization
- session refresh
- password hashing or cryptographic verification
- risk scoring based on IP address, device reputation, or geolocation
- admin account enable/disable workflows

These concerns belong to separate modules or shell-level integrations.

---

## 13. Example Application

**Scenario:** A returning user, Alex Chen, logs in to the platform after two previous failed attempts earlier in the day.

1. Alex navigates to the login page and enters their email (`alex.chen@example.com`) and password.
2. The frontend sends the credentials to the API layer. The credential verifier performs the hash comparison and returns `true`.
3. The API layer assembles a state snapshot: Alex's account is `ACTIVE`, has 2 failed attempts recorded, and the rate limit shows 3 total attempts in the current window (2 failures + 1 current). The max failed attempts threshold in config is `5`, so no lockout applies.
4. The API layer constructs a `LOGIN_ATTEMPT` input event with a new `eventId`, injects the snapshot, and calls the Login Core.
5. The Login Core validates the input, confirms the account is `ACTIVE`, confirms the rate limit (3 of a max of 10 attempts) has not been exceeded, and confirms `passwordVerificationResult: true`.
6. The core produces an `APPROVED` result with actions: `RESET_FAILED_LOGIN_COUNTER`, `CREATE_SESSION`, `EMIT_AUDIT_EVENT`, and `EMIT_METRIC`.
7. The Imperative Shell executes the actions in order: resets Alex's failed-attempt counter to 0, creates a new session with a 24-hour expiry, emits the audit event, and increments the login-success metric.
8. The API layer returns the session token to Alex's browser.

> **Result:** Alex is authenticated and redirected to their dashboard. The failed-attempt history is
> cleared. A clean audit entry records the successful login with the snapshot ID, the event ID, and
> the UTC timestamp.

---

## 14. Connection to the Yang Core Module

The following concepts described in this Yin Page require a corresponding formal specification
in the paired Yang Core Module (`auth.user-login` Yang):

- [x] Configuration schema — `maxFailedAttempts`, `lockoutDurationMinutes`, `rateLimitWindowSeconds`, `rateLimitMaxAttempts`, `maxEventAgeSeconds`, `notifyOnSuspiciousLogin`
- [x] State Snapshot schema — `account` (with `status`, `failedLoginAttempts`, `lockedAt`), `rateLimitState`, `processedEventIds` dedup cache, `currentTime`
- [x] Input Event schema — `LOGIN_ATTEMPT` event with `identifier`, `passwordVerificationResult`, `clientMeta`
- [x] Functional Result schema — `verdict`, `decision`, `reason`, `actions`, `telemetry`, `auditLog`
- [x] Decision logic for all five login outcomes: approved, invalid credentials, locked account, disabled account, rate limit exceeded
- [x] Actions: `CREATE_SESSION`, `RECORD_FAILED_LOGIN_ATTEMPT`, `RESET_FAILED_LOGIN_COUNTER`, `EMIT_AUDIT_EVENT`, `EMIT_METRIC`, `SEND_SECURITY_NOTIFICATION`, `REJECT_LOGIN`
- [x] Idempotency — duplicate `eventId` detection and behavior
- [x] Invariants — account status validity, timestamp freshness, config version guard
- [x] Error taxonomy — all edge cases from schema failure through unknown event type
- [x] Test cases — one per decision path
- [x] Yin/Yang Trace Map

---

## 15. Source Traceability

This Yin Page is a framework example document. It was not generated from a specific master document or external source block. In production use, this section records where each Yin requirement, domain rule, workflow, or constraint originated.

| Source | Type | Relevant sections / blocks | Used for |
|---|---|---|---|
| Framework example: user-login domain | Example / Framework artifact | All sections | All Yin intent and domain rules |
| `docs/03_Yin_Yang_Contracts.md` | Framework documentation | §"What the Imperative Shell May Do / Must Not Do", §"Trace Map" | Domain boundary definitions, security constraints, Shell/Core separation |
| `templates/yin/yin-page/02_yin_template.md` | Template | §1–§17 structure | Yin Page structure, section definitions, table formats |

> **Note for production use:** In a real project, this section would reference specific Master Documents, Source Block IDs (`source_block_id`), meeting transcripts, design files, or issue tickets from which the Yin requirements were derived. The `source.source_blocks` and `source.generated_from_template` frontmatter fields would also be fully populated.

---

## 16. Open Questions

None for this example. All relevant login-decision behavior is specified in the paired Yang section.

---

## 17. Quality Checklist

Before using this Yin Page as AI context or handing it to a Yang author, verify:

- [x] The configured Yin output language was followed.
- [x] Technical identifiers remained in English.
- [x] Document frontmatter is complete enough for retrieval.
- [x] The module is understandable from a human/product/domain perspective.
- [x] Target audience and actor expectations are clear.
- [x] Core value is clear.
- [x] User, admin, or system workflows are concrete.
- [x] Domain logic and business rules are explicit.
- [x] UI or interaction meaning is understandable without reading code.
- [x] Relevant data concepts and fields are listed in human terms.
- [x] Roles, permissions, privacy, and safety expectations are visible.
- [x] Integrations and dependencies are listed.
- [x] Out-of-scope boundaries are explicit.
- [x] Source traceability is recorded where known.
- [x] Open questions are marked instead of invented.
- [x] The matching Yang Core Module can be logically derived from this Yin Page if needed.
- [x] No secrets, tokens, passwords, or private credentials appear anywhere in the document.

---

# UserLoginCore — Core Module

**Document type:** `Yang Core Module`
**Module ID:** `auth.user-login`
**Schema version:** `1.0.0`
**Config version:** `1`
**Paired Yin document:** User Login & Auth — Yin Page (`auth.user-login` Yin)
**Status:** `APPROVED`
**Last updated:** 2026-06-07
**Owner:** Platform / Auth Team


---

## 1. Domain Context

`UserLoginCore` is the Functional Core for the email-and-password login decision in the Auth
domain. It receives a login attempt event, evaluates the attempt against injected account state
and rate-limit state, and produces a deterministic result containing either an approved session-
creation signal or a structured rejection. The core belongs to the `auth` bounded context and sits
at the boundary between the unauthenticated API surface and the authenticated session layer. It is
triggered by every login form submission that reaches the server. It depends on pre-loaded account
and rate-limit state provided by the Imperative Shell before each call. It does not perform the
password hash comparison; the result of that comparison is injected as a fact in the input payload.

**Bounded context:** `auth`
**Upstream dependencies:** `auth.credential-verifier`, `auth.account-store`, `auth.rate-limit-store`
**Downstream dependents:** `auth.session-manager`, `platform.audit-log`, `platform.metrics`, `platform.notification-service`
**Triggering event:** `LOGIN_ATTEMPT` — emitted by the API layer when a user submits the login form

**Out of scope for this module:** OAuth flows, SSO, MFA, password reset, account registration,
billing checks, tenant-level access control, and session refresh. These are separate modules.

---

## 2. Architecture Overview

| Property | Value |
|---|---|
| Module name | `UserLoginCore` |
| Paradigm | Functional Core / Imperative Shell |
| Core signature | `Result = f(Config, StateSnapshot, InputEvent)` |
| Side-effect strategy | Action objects returned to Imperative Shell; core performs zero I/O |
| Idempotency key field | `InputEvent.eventId` |
| Schema version | `1.0.0` |
| Config version | `1` |

**Core guarantees:**

| Guarantee | Status | Notes |
|---|---|---|
| Deterministic | ✅ | Same Config + StateSnapshot + InputEvent always produces the same Result |
| Idempotent | ✅ | Duplicate `eventId` returns `REJECT_DUPLICATE` with no new side effects |
| Side-effect-free | ✅ | No database writes, no HTTP calls, no file I/O, no queue operations inside the core |
| Testable | ✅ | All inputs and outputs are schema-validatable; no hidden state |
| Auditable | ✅ | Every pipeline step is recorded in `FunctionalResult.auditLog` |
| Versionable | ✅ | `configVersion` and `schemaVersion` are explicit; mismatches cause `ABANDON` |

---

## 3. API Contract

### 3.1 Configuration Schema

Static configuration loaded at system initialisation. Defines thresholds, durations, and feature
flags. Never contains runtime state. Increment `configVersion` on any breaking change.

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "auth.user-login/config/v1",
  "title": "UserLoginCore Configuration",
  "type": "object",
  "required": [
    "configVersion",
    "maxFailedAttempts",
    "lockoutDurationMinutes",
    "rateLimitWindowSeconds",
    "rateLimitMaxAttempts",
    "maxEventAgeSeconds"
  ],
  "additionalProperties": false,
  "properties": {
    "configVersion": {
      "type": "integer",
      "description": "Configuration schema version. Must equal 1 for this release. Increment on breaking changes.",
      "example": 1
    },
    "maxFailedAttempts": {
      "type": "integer",
      "minimum": 1,
      "description": "Number of consecutive failed login attempts before the account is locked.",
      "example": 5
    },
    "lockoutDurationMinutes": {
      "type": "integer",
      "minimum": 1,
      "description": "Duration in minutes that an account remains locked after reaching maxFailedAttempts.",
      "example": 30
    },
    "rateLimitWindowSeconds": {
      "type": "integer",
      "minimum": 1,
      "description": "Length of the sliding rate-limit window in seconds.",
      "example": 300
    },
    "rateLimitMaxAttempts": {
      "type": "integer",
      "minimum": 1,
      "description": "Maximum number of login attempts permitted within rateLimitWindowSeconds for a single identifier.",
      "example": 10
    },
    "maxEventAgeSeconds": {
      "type": "integer",
      "minimum": 1,
      "description": "Maximum age of an incoming event in seconds. Events older than this value are rejected as expired.",
      "example": 300
    },
    "notifyOnSuspiciousLogin": {
      "type": "boolean",
      "description": "When true, the core emits a SEND_SECURITY_NOTIFICATION action when a successful login follows recent failed attempts (failedLoginAttempts >= 1 at time of success).",
      "default": true
    }
  }
}
```

**Config fields summary:**

| Field | Type | Required | Description | Default / Example |
|---|---|---|---|---|
| `configVersion` | integer | ✅ | Must match compiled version (1) | `1` |
| `maxFailedAttempts` | integer | ✅ | Failed attempts before account lock | `5` |
| `lockoutDurationMinutes` | integer | ✅ | Minutes an account remains locked | `30` |
| `rateLimitWindowSeconds` | integer | ✅ | Rate-limit sliding window width | `300` |
| `rateLimitMaxAttempts` | integer | ✅ | Max attempts per window per identifier | `10` |
| `maxEventAgeSeconds` | integer | ✅ | Max event age before rejection | `300` |
| `notifyOnSuspiciousLogin` | boolean | ❌ | Notify on success after prior failures | `true` |

---

### 3.2 State Snapshot Schema

Runtime state injected by the Imperative Shell before each core invocation. The core never fetches
state itself. All fields are read-only inside the core.

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "auth.user-login/state-snapshot/v1.0.0",
  "title": "UserLoginCore State Snapshot",
  "type": "object",
  "required": [
    "snapshotId",
    "currentTime",
    "account",
    "rateLimitState",
    "processedEventIds"
  ],
  "additionalProperties": false,
  "properties": {
    "snapshotId": {
      "type": "string",
      "format": "uuid",
      "description": "Unique identifier for this state snapshot. Used for audit traceability."
    },
    "currentTime": {
      "type": "string",
      "format": "date-time",
      "description": "Injected current UTC time. The core must never read system time directly."
    },
    "account": {
      "type": "object",
      "description": "Current state of the account being authenticated. Loaded by the shell before calling the core.",
      "required": ["accountId", "identifier", "status", "failedLoginAttempts"],
      "additionalProperties": false,
      "properties": {
        "accountId": {
          "type": "string",
          "format": "uuid",
          "description": "Unique identifier for the account."
        },
        "identifier": {
          "type": "string",
          "format": "email",
          "description": "Email address used as the login identifier."
        },
        "status": {
          "type": "string",
          "enum": ["ACTIVE", "LOCKED", "DISABLED"],
          "description": "Current account status."
        },
        "failedLoginAttempts": {
          "type": "integer",
          "minimum": 0,
          "description": "Number of consecutive failed login attempts since the last successful login."
        },
        "lockedAt": {
          "type": ["string", "null"],
          "format": "date-time",
          "description": "UTC timestamp when the account was locked. Null if the account is not locked."
        },
        "lastLoginAt": {
          "type": ["string", "null"],
          "format": "date-time",
          "description": "UTC timestamp of the most recent successful login. Null if the account has never logged in."
        }
      }
    },
    "rateLimitState": {
      "type": "object",
      "description": "Current rate-limit state for the requesting identifier, pre-loaded by the shell.",
      "required": ["identifier", "attemptsInWindow", "windowStartedAt"],
      "additionalProperties": false,
      "properties": {
        "identifier": {
          "type": "string",
          "description": "The email address for which this rate-limit state applies."
        },
        "attemptsInWindow": {
          "type": "integer",
          "minimum": 0,
          "description": "Number of login attempts (successful or failed) recorded in the current window."
        },
        "windowStartedAt": {
          "type": "string",
          "format": "date-time",
          "description": "UTC timestamp when the current rate-limit window started."
        }
      }
    },
    "processedEventIds": {
      "type": "array",
      "items": { "type": "string", "format": "uuid" },
      "description": "Set of recently processed eventIds from the dedup cache. Used for idempotency checking. The shell loads only the relevant window (e.g. last 10 minutes)."
    }
  }
}
```

**State fields summary:**

| Field | Type | Required | Description | Provided by |
|---|---|---|---|---|
| `snapshotId` | string (uuid) | ✅ | Snapshot traceability ID | Shell before core call |
| `currentTime` | string (date-time) | ✅ | Injected UTC time | Shell before core call |
| `account.accountId` | string (uuid) | ✅ | Account unique identifier | `auth.account-store` |
| `account.identifier` | string (email) | ✅ | Login email address | `auth.account-store` |
| `account.status` | string (enum) | ✅ | `ACTIVE` / `LOCKED` / `DISABLED` | `auth.account-store` |
| `account.failedLoginAttempts` | integer | ✅ | Consecutive failure count | `auth.account-store` |
| `account.lockedAt` | string (date-time) \| null | ❌ | Lock timestamp if locked | `auth.account-store` |
| `account.lastLoginAt` | string (date-time) \| null | ❌ | Last successful login time | `auth.account-store` |
| `rateLimitState.identifier` | string | ✅ | Identifier for rate-limit scope | `auth.rate-limit-store` |
| `rateLimitState.attemptsInWindow` | integer | ✅ | Attempt count in current window | `auth.rate-limit-store` |
| `rateLimitState.windowStartedAt` | string (date-time) | ✅ | Window start time | `auth.rate-limit-store` |
| `processedEventIds` | string[] | ✅ | Recent event IDs for dedup check | Shell (loaded from dedup cache) |

---

### 3.3 Input Event / Command Schema

The incoming event submitted by the API layer. `LOGIN_ATTEMPT` is the only event type handled by
this core. Use a discriminated union if additional event types are introduced in a future version.

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "auth.user-login/input-event/v1.0.0",
  "title": "UserLoginCore Input Event",
  "oneOf": [
    {
      "title": "LOGIN_ATTEMPT",
      "type": "object",
      "required": [
        "eventId",
        "traceId",
        "correlationId",
        "eventType",
        "timestamp",
        "actor",
        "payload"
      ],
      "additionalProperties": false,
      "properties": {
        "eventId": {
          "type": "string",
          "format": "uuid",
          "description": "Globally unique event identifier. Serves as the idempotency key. Must be UUID v4."
        },
        "traceId": {
          "type": "string",
          "description": "Distributed trace identifier. Propagated from the upstream HTTP request context."
        },
        "correlationId": {
          "type": "string",
          "description": "Business correlation ID. Typically the request session or browser fingerprint used to group related attempts."
        },
        "eventType": {
          "type": "string",
          "const": "LOGIN_ATTEMPT",
          "description": "Discriminator field. Must be exactly 'LOGIN_ATTEMPT'."
        },
        "timestamp": {
          "type": "string",
          "format": "date-time",
          "description": "Event creation time in UTC ISO 8601. Must not be older than Config.maxEventAgeSeconds."
        },
        "actor": {
          "type": "object",
          "required": ["actorId", "actorType"],
          "additionalProperties": false,
          "description": "Identity of the entity submitting the event. For login attempts, actorType is always ANONYMOUS.",
          "properties": {
            "actorId": {
              "type": "string",
              "description": "A stable client identifier (e.g. browser fingerprint or device ID). Not a user ID — the user is not yet authenticated."
            },
            "actorType": {
              "type": "string",
              "enum": ["ANONYMOUS", "SERVICE"],
              "description": "ANONYMOUS for user-initiated logins; SERVICE for automated test harnesses or internal integrations."
            }
          }
        },
        "payload": {
          "type": "object",
          "required": ["identifier", "passwordVerificationResult"],
          "additionalProperties": false,
          "description": "Login-attempt-specific payload.",
          "properties": {
            "identifier": {
              "type": "string",
              "format": "email",
              "description": "Email address the user is attempting to authenticate as. Must match StateSnapshot.account.identifier."
            },
            "passwordVerificationResult": {
              "type": "boolean",
              "description": "Result of the password hash comparison performed by auth.credential-verifier before calling this core. True = password matched. False = password did not match. The core never performs the hash comparison itself."
            },
            "clientMeta": {
              "type": "object",
              "description": "Optional metadata about the requesting client. Passed through to the CREATE_SESSION action. Not evaluated by the core.",
              "additionalProperties": false,
              "properties": {
                "userAgent": {
                  "type": "string",
                  "description": "HTTP User-Agent string."
                },
                "ipAddress": {
                  "type": "string",
                  "description": "Client IP address. Handle per applicable privacy regulation."
                }
              }
            }
          }
        }
      }
    }
  ]
}
```

**Input event fields summary:**

| Field | Type | Required | Description |
|---|---|---|---|
| `eventId` | string (uuid) | ✅ | Idempotency key; must be UUID v4 |
| `traceId` | string | ✅ | Distributed trace propagation |
| `correlationId` | string | ✅ | Business correlation linkage |
| `eventType` | `"LOGIN_ATTEMPT"` | ✅ | Discriminator; only valid value is `LOGIN_ATTEMPT` |
| `timestamp` | string (date-time) | ✅ | Event creation time UTC |
| `actor.actorId` | string | ✅ | Stable client identifier (not a user ID) |
| `actor.actorType` | `"ANONYMOUS"` \| `"SERVICE"` | ✅ | Login attempts are `ANONYMOUS` |
| `payload.identifier` | string (email) | ✅ | Email address being authenticated |
| `payload.passwordVerificationResult` | boolean | ✅ | Pre-computed hash comparison result |
| `payload.clientMeta.userAgent` | string | ❌ | Passed through to session; not evaluated |
| `payload.clientMeta.ipAddress` | string | ❌ | Passed through to session; not evaluated |

---

### 3.4 Functional Result Schema

The output of the core function. Returned to the Imperative Shell. The shell reads `actions` and
executes each in priority order.

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "auth.user-login/functional-result/v1.0.0",
  "title": "UserLoginCore Functional Result",
  "type": "object",
  "required": [
    "resultId",
    "eventId",
    "traceId",
    "verdict",
    "decision",
    "reason",
    "actions",
    "telemetry",
    "auditLog"
  ],
  "additionalProperties": false,
  "properties": {
    "resultId": {
      "type": "string",
      "format": "uuid",
      "description": "Unique identifier for this result object."
    },
    "eventId": {
      "type": "string",
      "format": "uuid",
      "description": "Echo of InputEvent.eventId. Links this result back to its input event."
    },
    "traceId": {
      "type": "string",
      "description": "Echo of InputEvent.traceId for distributed trace continuity."
    },
    "verdict": {
      "type": "string",
      "enum": ["SUCCESS", "FAILURE"],
      "description": "Top-level outcome. SUCCESS = the core completed without internal error (even if decision is REJECTED). FAILURE = the core encountered an unrecoverable condition. Note: PARTIAL is intentionally omitted here because a login module produces only binary SUCCESS/FAILURE outcomes."
    },
    "decision": {
      "type": "string",
      "enum": [
        "APPROVED",
        "REJECTED",
        "REJECT_DUPLICATE",
        "REJECT_INVALID",
        "ABANDON"
      ],
      "description": "The specific decision the core reached. APPROVED = login allowed. REJECTED = login denied for a known business reason. REJECT_DUPLICATE = idempotent repeat. REJECT_INVALID = schema or invariant failure. ABANDON = unrecoverable internal error."
    },
    "rejectionReason": {
      "type": ["string", "null"],
      "enum": [
        "INVALID_CREDENTIALS",
        "ACCOUNT_LOCKED",
        "ACCOUNT_DISABLED",
        "RATE_LIMIT_EXCEEDED",
        "DUPLICATE_EVENT",
        "SCHEMA_INVALID",
        "STATE_MISSING",
        "TIMESTAMP_EXPIRED",
        "UNKNOWN_EVENT_TYPE",
        "CONFIG_VERSION_MISMATCH",
        "IDENTIFIER_MISMATCH",
        null
      ],
      "description": "Specific rejection reason for internal use, audit, and logging. MUST NOT be exposed directly to the client. Null when decision is APPROVED."
    },
    "reason": {
      "type": "string",
      "description": "Human-readable explanation of the decision. For APPROVED: a brief confirmation. For all rejections: a description safe for internal logs. Must never be the string returned to the end user."
    },
    "actions": {
      "type": "array",
      "description": "Ordered list of Action objects the Imperative Shell must execute. Empty for REJECT_DUPLICATE. Ordered by priority: CRITICAL first, then HIGH, NORMAL, LOW.",
      "items": { "$ref": "#/$defs/Action" }
    },
    "telemetry": {
      "type": "object",
      "required": ["durationMs", "stepsExecuted"],
      "additionalProperties": false,
      "properties": {
        "durationMs": {
          "type": "integer",
          "description": "Total core execution duration in milliseconds (measured outside the core; injected by shell)."
        },
        "stepsExecuted": {
          "type": "array",
          "items": { "type": "string" },
          "description": "Ordered list of pipeline step names that ran to completion or early exit."
        },
        "evaluatedChecks": {
          "type": "integer",
          "description": "Number of domain checks evaluated before reaching a verdict."
        }
      }
    },
    "auditLog": {
      "type": "array",
      "description": "Immutable ordered record of every pipeline step executed by the core. One entry per step.",
      "items": {
        "type": "object",
        "required": ["step", "outcome", "timestamp"],
        "additionalProperties": false,
        "properties": {
          "step": {
            "type": "string",
            "description": "Pipeline step name (e.g. SCHEMA_VALIDATION, ACCOUNT_STATUS_CHECK)."
          },
          "outcome": {
            "type": "string",
            "description": "Step outcome (e.g. PASS, FAIL, DUPLICATE, LOCKED, DISABLED, RATE_LIMITED, APPROVED)."
          },
          "detail": {
            "type": ["string", "null"],
            "description": "Optional additional context for the step outcome. For internal use only."
          },
          "timestamp": {
            "type": "string",
            "format": "date-time",
            "description": "StateSnapshot.currentTime at the point this step was evaluated."
          }
        }
      }
    }
  },
  "$defs": {
    "Action": {
      "type": "object",
      "required": ["actionType", "priority", "parameters"],
      "additionalProperties": false,
      "properties": {
        "actionType": {
          "type": "string",
          "enum": [
            "CREATE_SESSION",
            "RECORD_FAILED_LOGIN_ATTEMPT",
            "RESET_FAILED_LOGIN_COUNTER",
            "EMIT_AUDIT_EVENT",
            "EMIT_METRIC",
            "SEND_SECURITY_NOTIFICATION",
            "LOCK_ACCOUNT",
            "REJECT_LOGIN"
          ],
          "description": "The type of side effect the Imperative Shell must execute."
        },
        "priority": {
          "type": "string",
          "enum": ["CRITICAL", "HIGH", "NORMAL", "LOW"],
          "description": "Execution priority hint. Shell executes CRITICAL first, then HIGH, NORMAL, LOW."
        },
        "parameters": {
          "type": "object",
          "description": "Action-type-specific parameters. See Action Type Registry in Section 5."
        },
        "idempotencyKey": {
          "type": ["string", "null"],
          "description": "Stable key the Shell uses to deduplicate action execution. Format: {eventId}-{actionType}."
        },
        "reason": {
          "type": ["string", "null"],
          "description": "Why this action was generated. For audit and shell-side logging."
        }
      }
    }
  }
}
```

---

## 4. Decision Logic

### Decision Pipeline

The core processes every `LOGIN_ATTEMPT` event through this fixed, ordered pipeline. Each step may
produce an early exit. Steps are never skipped. The pipeline terminates at the first early-exit
condition; otherwise it proceeds through all nine steps.

| Step | Name | Description | Early exit decision |
|---|---|---|---|
| 1 | `SCHEMA_VALIDATION` | Validate `InputEvent` against schema `auth.user-login/input-event/v1.0.0`. Validate `Config.configVersion == 1`. | `REJECT_INVALID` / `ABANDON` |
| 2 | `TIMESTAMP_CHECK` | Compute age = `currentTime - InputEvent.timestamp` in seconds. If age > `Config.maxEventAgeSeconds`, reject. | `REJECT_INVALID` |
| 3 | `IDEMPOTENCY_CHECK` | Check `InputEvent.eventId` against `StateSnapshot.processedEventIds`. If found, return duplicate result. | `REJECT_DUPLICATE` |
| 4 | `IDENTIFIER_CONSISTENCY_CHECK` | Verify `InputEvent.payload.identifier == StateSnapshot.account.identifier`. If mismatch, the shell loaded the wrong account. | `REJECT_INVALID` |
| 5 | `ACCOUNT_STATUS_CHECK` | Check `StateSnapshot.account.status`. If `DISABLED`, reject immediately. If `LOCKED`, evaluate lock expiry against `currentTime`. | `REJECTED` |
| 6 | `RATE_LIMIT_CHECK` | Check `StateSnapshot.rateLimitState.attemptsInWindow`. If >= `Config.rateLimitMaxAttempts`, reject. | `REJECTED` |
| 7 | `CREDENTIAL_EVALUATION` | Evaluate `InputEvent.payload.passwordVerificationResult`. If `false`, prepare rejection. | `REJECTED` |
| 8 | `VERDICT_CREATION` | All prior steps passed. Decision is `APPROVED`. Determine if suspicious-login notification applies. | — |
| 9 | `ACTION_AND_AUDIT_CREATION` | Assemble ordered action list and audit log entries for all steps executed. | — |

### Decision Matrix

> **Verdict enum note:** This module uses domain-specific verdicts `SUCCESS` and `FAILURE` instead
> of the standard template verdicts (`ALLOW | DENY | RETRY | NOOP | ERROR`). This is an intentional
> adaptation for the authentication domain, where `SUCCESS`/`FAILURE` map directly to the login
> outcome semantics expected by callers. When creating Yang contracts for other domains, use the
> standard template verdicts unless a domain-specific override is explicitly justified here.

| Condition | `decision` | `rejectionReason` | `verdict` |
|---|---|---|---|
| `InputEvent` fails schema validation | `REJECT_INVALID` | `SCHEMA_INVALID` | `FAILURE` |
| `Config.configVersion` ≠ `1` | `ABANDON` | `CONFIG_VERSION_MISMATCH` | `FAILURE` |
| `InputEvent.timestamp` age > `maxEventAgeSeconds` | `REJECT_INVALID` | `TIMESTAMP_EXPIRED` | `FAILURE` |
| `InputEvent.eventId` found in `processedEventIds` | `REJECT_DUPLICATE` | `DUPLICATE_EVENT` | `SUCCESS` |
| `payload.identifier` ≠ `account.identifier` | `REJECT_INVALID` | `IDENTIFIER_MISMATCH` | `FAILURE` |
| `account.status == DISABLED` | `REJECTED` | `ACCOUNT_DISABLED` | `FAILURE` |
| `account.status == LOCKED` and lock has not expired | `REJECTED` | `ACCOUNT_LOCKED` | `FAILURE` |
| `rateLimitState.attemptsInWindow >= rateLimitMaxAttempts` | `REJECTED` | `RATE_LIMIT_EXCEEDED` | `FAILURE` |
| `passwordVerificationResult == false` | `REJECTED` | `INVALID_CREDENTIALS` | `FAILURE` |
| All checks pass, `passwordVerificationResult == true` | `APPROVED` | `null` | `SUCCESS` |

### Lock Expiry Evaluation (Step 5 — LOCKED path)

When `account.status == LOCKED`:

1. If `account.lockedAt` is null → treat as `REJECT_INVALID` with reason `STATE_MISSING` (invariant violation; locked account must have a `lockedAt` timestamp).
2. Compute `lockAgeMinutes = (currentTime - account.lockedAt) in minutes`.
3. If `lockAgeMinutes < Config.lockoutDurationMinutes` → lock is still active. Decision: `REJECTED`, reason: `ACCOUNT_LOCKED`.
4. If `lockAgeMinutes >= Config.lockoutDurationMinutes` → lock has expired. The core does **not** unlock the account itself. The core treats an expired lock the same as a missing lock: it proceeds to Step 6 with the existing account state. The shell is responsible for resetting the account status via a separate housekeeping workflow. The core notes the expired lock in the audit log.

### Suspicious Login Notification (Step 8 — APPROVED path)

When decision is `APPROVED` and `Config.notifyOnSuspiciousLogin == true`:
- If `StateSnapshot.account.failedLoginAttempts >= 1` at the time of the snapshot → add `SEND_SECURITY_NOTIFICATION` action to the result.
- This signals the shell to notify the account holder that a successful login followed previous failures.

---

## 5. Actions for the Imperative Shell

The core never executes side effects. All side effects are returned as Action objects. The
Imperative Shell reads and executes them in priority order. Actions with equal priority may be
parallelised unless a sequential dependency is noted in `reason`.

### Action Type Registry

| Action type | Priority | When emitted | Description | Key parameters | Idempotency key |
|---|---|---|---|---|---|
| `REJECT_LOGIN` | `HIGH` | Any `REJECTED` or `REJECT_INVALID` decision | Signals the API layer to return a rejection response. Contains the internal reason for logging; does not contain the client-facing message (the API layer produces that). | `rejectionReason`, `eventId` | `{eventId}-REJECT` |
| `RECORD_FAILED_LOGIN_ATTEMPT` | `HIGH` | `REJECTED` with `INVALID_CREDENTIALS` | Increments the failed-attempt counter for the account and records the attempt timestamp. | `accountId`, `attemptTimestamp` | `{eventId}-RECORD_FAIL` |
| `LOCK_ACCOUNT` | `HIGH` | `REJECTED` with `INVALID_CREDENTIALS` when `failedLoginAttempts + 1 >= maxFailedAttempts` | Locks the account after the configured failed-attempt threshold is reached. | `accountId`, `lockedAt` | `{eventId}-LOCK_ACCOUNT` |
| `CREATE_SESSION` | `CRITICAL` | `APPROVED` | Signals `auth.session-manager` to create a new authenticated session. | `accountId`, `clientMeta`, `expiresInSeconds` | `{eventId}-SESSION` |
| `RESET_FAILED_LOGIN_COUNTER` | `HIGH` | `APPROVED` | Resets `failedLoginAttempts` to 0 for the account. Executed after a successful login. | `accountId` | `{eventId}-RESET` |
| `SEND_SECURITY_NOTIFICATION` | `NORMAL` | `APPROVED` when prior failures exist and `notifyOnSuspiciousLogin == true` | Notifies the account holder that a successful login occurred after previous failures. | `accountId`, `loginTimestamp`, `clientMeta` | `{eventId}-NOTIFY` |
| `EMIT_AUDIT_EVENT` | `HIGH` | All outcomes | Emits a structured audit record to `platform.audit-log`. | `eventId`, `decision`, `rejectionReason`, `accountId`, `snapshotId`, `traceId`, `timestamp` | `{eventId}-AUDIT` |
| `EMIT_METRIC` | `NORMAL` | All outcomes | Emits an observability metric to `platform.metrics`. | `metricName`, `value`, `labels` | — |

### Action Sets by Decision Path

| Decision | Actions emitted (in priority order) |
|---|---|
| `APPROVED` (no prior failures) | `CREATE_SESSION` (CRITICAL), `RESET_FAILED_LOGIN_COUNTER` (HIGH), `EMIT_AUDIT_EVENT` (HIGH), `EMIT_METRIC` (NORMAL) |
| `APPROVED` (prior failures exist, notify enabled) | `CREATE_SESSION` (CRITICAL), `RESET_FAILED_LOGIN_COUNTER` (HIGH), `EMIT_AUDIT_EVENT` (HIGH), `SEND_SECURITY_NOTIFICATION` (NORMAL), `EMIT_METRIC` (NORMAL) |
| `REJECTED` — `INVALID_CREDENTIALS` below lockout threshold | `REJECT_LOGIN` (HIGH), `RECORD_FAILED_LOGIN_ATTEMPT` (HIGH), `EMIT_AUDIT_EVENT` (HIGH), `EMIT_METRIC` (NORMAL) |
| `REJECTED` — `INVALID_CREDENTIALS` reaches lockout threshold | `REJECT_LOGIN` (HIGH), `RECORD_FAILED_LOGIN_ATTEMPT` (HIGH), `LOCK_ACCOUNT` (HIGH), `EMIT_AUDIT_EVENT` (HIGH), `EMIT_METRIC` (NORMAL) |
| `REJECTED` — `ACCOUNT_LOCKED` | `REJECT_LOGIN` (HIGH), `EMIT_AUDIT_EVENT` (HIGH), `EMIT_METRIC` (NORMAL) |
| `REJECTED` — `ACCOUNT_DISABLED` | `REJECT_LOGIN` (HIGH), `EMIT_AUDIT_EVENT` (HIGH), `EMIT_METRIC` (NORMAL) |
| `REJECTED` — `RATE_LIMIT_EXCEEDED` | `REJECT_LOGIN` (HIGH), `EMIT_AUDIT_EVENT` (HIGH), `EMIT_METRIC` (NORMAL) |
| `REJECT_INVALID` | `EMIT_AUDIT_EVENT` (HIGH), `EMIT_METRIC` (NORMAL) |
| `REJECT_DUPLICATE` | *(empty — no side effects on duplicate)* |
| `ABANDON` | `EMIT_AUDIT_EVENT` (HIGH) |

### Action Parameter Schemas

**`CREATE_SESSION` parameters:**

```json
{
  "accountId": "<string:uuid>",
  "expiresInSeconds": "<integer — shell reads from $ENV_SESSION_EXPIRY_SECONDS>",
  "clientMeta": {
    "userAgent": "<string|null>",
    "ipAddress": "<string|null>"
  }
}
```

**`RECORD_FAILED_LOGIN_ATTEMPT` parameters:**

```json
{
  "accountId": "<string:uuid>",
  "attemptTimestamp": "<string:date-time — equals StateSnapshot.currentTime>"
}
```

**`RESET_FAILED_LOGIN_COUNTER` parameters:**

```json
{
  "accountId": "<string:uuid>"
}
```

**`LOCK_ACCOUNT` parameters:**

```json
{
  "accountId": "<string:uuid>",
  "lockedAt": "<string:date-time — equals StateSnapshot.currentTime>"
}
```

**`REJECT_LOGIN` parameters:**

```json
{
  "rejectionReason": "<enum — the rejectionReason value from FunctionalResult>",
  "eventId": "<string:uuid>"
}
```

**`SEND_SECURITY_NOTIFICATION` parameters:**

```json
{
  "accountId": "<string:uuid>",
  "loginTimestamp": "<string:date-time — equals StateSnapshot.currentTime>",
  "clientMeta": {
    "userAgent": "<string|null>",
    "ipAddress": "<string|null>"
  }
}
```

**`EMIT_AUDIT_EVENT` parameters:**

```json
{
  "eventId": "<string:uuid>",
  "decision": "<enum — from FunctionalResult.decision>",
  "rejectionReason": "<enum|null — from FunctionalResult.rejectionReason>",
  "accountId": "<string:uuid>",
  "snapshotId": "<string:uuid>",
  "traceId": "<string>",
  "timestamp": "<string:date-time — StateSnapshot.currentTime>"
}
```

**`EMIT_METRIC` parameters:**

```json
{
  "metricName": "<string — see Section 10 for defined metric names>",
  "value": 1,
  "labels": {
    "decision": "<enum>",
    "rejectionReason": "<enum|null>",
    "accountStatus": "<enum>"
  }
}
```

---

## 6. Idempotency

**Idempotency key field:** `InputEvent.eventId`
**Dedup cache field:** `StateSnapshot.processedEventIds`
**Detection strategy:** Exact UUID match — `InputEvent.eventId` is searched in `StateSnapshot.processedEventIds` at Step 3.

**On duplicate event detected (eventId already in processedEventIds):**

| Result field | Value |
|---|---|
| `decision` | `REJECT_DUPLICATE` |
| `rejectionReason` | `DUPLICATE_EVENT` |
| `verdict` | `SUCCESS` |
| `reason` | `"Duplicate event detected. eventId already processed. No side effects produced."` |
| `actions` | Empty array — zero side effects |

**Behavior guarantee:** Processing the same `eventId` a second (or nth) time always produces a
`REJECT_DUPLICATE` result with an empty action array. The shell must not execute any action for a
previously completed event. The shell is responsible for adding the `eventId` to the dedup cache
after the first successful execution of the action list.

**Cache TTL:** The shell maintains the dedup cache with a TTL of at least `2 × maxEventAgeSeconds`
to ensure that any event that passes the timestamp check cannot later appear as a non-duplicate.
For `maxEventAgeSeconds = 300`, the minimum dedup cache TTL is 600 seconds (10 minutes).

**Note on `REJECT_DUPLICATE` verdict:** The verdict is `SUCCESS` (not `FAILURE`) because the
system has not failed — the event was simply already processed. Returning `SUCCESS` allows the
caller to treat repeated submissions as a safe, non-error condition.

---

## 7. Invariants

Invariants are conditions the core assumes to be true at all times. If any invariant is violated,
the core emits the stated result immediately and does not proceed further.

| ID | Invariant | Violation result |
|---|---|---|
| I-01 | `InputEvent.eventId` must be a valid UUID v4. | `REJECT_INVALID` / `SCHEMA_INVALID` |
| I-02 | `StateSnapshot.currentTime` must be a valid UTC ISO 8601 timestamp. | `REJECT_INVALID` / `STATE_MISSING` |
| I-03 | `InputEvent.timestamp` must not be older than `Config.maxEventAgeSeconds` relative to `StateSnapshot.currentTime`. | `REJECT_INVALID` / `TIMESTAMP_EXPIRED` |
| I-04 | `Config.configVersion` must equal `1`. Any other value indicates a version mismatch. | `ABANDON` / `CONFIG_VERSION_MISMATCH` |
| I-05 | `StateSnapshot.account` must be present and contain all required fields. | `REJECT_INVALID` / `STATE_MISSING` |
| I-06 | `StateSnapshot.account.status` must be one of `ACTIVE`, `LOCKED`, `DISABLED`. | `REJECT_INVALID` / `STATE_MISSING` |
| I-07 | If `StateSnapshot.account.status == LOCKED`, then `StateSnapshot.account.lockedAt` must not be null. | `REJECT_INVALID` / `STATE_MISSING` |
| I-08 | `InputEvent.payload.identifier` must equal `StateSnapshot.account.identifier`. A mismatch indicates the shell loaded the wrong account record. | `REJECT_INVALID` / `IDENTIFIER_MISMATCH` |
| I-09 | `InputEvent.eventType` must equal `"LOGIN_ATTEMPT"`. Any other value is an unknown event type. | `REJECT_INVALID` / `UNKNOWN_EVENT_TYPE` |
| I-10 | The `actions` array in the result must never contain an action type not defined in the Action Type Registry (Section 5). | Internal assertion — triggers `ABANDON` if violated |
| I-11 | The `auditLog` must contain exactly one entry for each pipeline step executed. Steps must not be silently skipped. | Internal assertion — triggers `ABANDON` if violated |
| I-12 | The core must never access system time directly. All time comparisons use `StateSnapshot.currentTime`. | Enforced at design time; violation is a code defect |

---

## 8. Errors and Edge Cases

| Error / Edge Case | Trigger condition | `decision` | `rejectionReason` | `verdict` | Actions emitted |
|---|---|---|---|---|---|
| Invalid input schema | `InputEvent` fails JSON Schema validation | `REJECT_INVALID` | `SCHEMA_INVALID` | `FAILURE` | `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| Config version mismatch | `Config.configVersion` ≠ `1` | `ABANDON` | `CONFIG_VERSION_MISMATCH` | `FAILURE` | `EMIT_AUDIT_EVENT` |
| Expired timestamp | `InputEvent.timestamp` age > `maxEventAgeSeconds` | `REJECT_INVALID` | `TIMESTAMP_EXPIRED` | `FAILURE` | `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| Duplicate event | `eventId` found in `processedEventIds` | `REJECT_DUPLICATE` | `DUPLICATE_EVENT` | `SUCCESS` | *(none)* |
| Identifier mismatch | `payload.identifier` ≠ `account.identifier` | `REJECT_INVALID` | `IDENTIFIER_MISMATCH` | `FAILURE` | `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| Unknown event type | `InputEvent.eventType` is not `"LOGIN_ATTEMPT"` | `REJECT_INVALID` | `UNKNOWN_EVENT_TYPE` | `FAILURE` | `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| Missing state | `StateSnapshot.account` missing required fields | `REJECT_INVALID` | `STATE_MISSING` | `FAILURE` | `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| Locked account — lock active | `account.status == LOCKED` and `lockAgeMinutes < lockoutDurationMinutes` | `REJECTED` | `ACCOUNT_LOCKED` | `FAILURE` | `REJECT_LOGIN`, `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| Locked account — missing `lockedAt` | `account.status == LOCKED` but `account.lockedAt == null` (invariant I-07) | `REJECT_INVALID` | `STATE_MISSING` | `FAILURE` | `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| Disabled account | `account.status == DISABLED` | `REJECTED` | `ACCOUNT_DISABLED` | `FAILURE` | `REJECT_LOGIN`, `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| Rate limit exceeded | `rateLimitState.attemptsInWindow >= rateLimitMaxAttempts` | `REJECTED` | `RATE_LIMIT_EXCEEDED` | `FAILURE` | `REJECT_LOGIN`, `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| Wrong password | `passwordVerificationResult == false` | `REJECTED` | `INVALID_CREDENTIALS` | `FAILURE` | `REJECT_LOGIN`, `RECORD_FAILED_LOGIN_ATTEMPT`, `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| Wrong password — at lockout threshold | `passwordVerificationResult == false` and `failedLoginAttempts + 1 >= maxFailedAttempts` | `REJECTED` | `INVALID_CREDENTIALS` | `FAILURE` | `REJECT_LOGIN`, `RECORD_FAILED_LOGIN_ATTEMPT`, `LOCK_ACCOUNT`, `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| Successful login with prior failures | `passwordVerificationResult == true` and `failedLoginAttempts >= 1` | `APPROVED` | `null` | `SUCCESS` | `CREATE_SESSION`, `RESET_FAILED_LOGIN_COUNTER`, `EMIT_AUDIT_EVENT`, `SEND_SECURITY_NOTIFICATION` (if enabled), `EMIT_METRIC` |
| Valid login — clean account | `passwordVerificationResult == true` and `failedLoginAttempts == 0` | `APPROVED` | `null` | `SUCCESS` | `CREATE_SESSION`, `RESET_FAILED_LOGIN_COUNTER`, `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |

> **Note on `RECORD_FAILED_LOGIN_ATTEMPT` and account locking:** The core emits
> `RECORD_FAILED_LOGIN_ATTEMPT` for every `INVALID_CREDENTIALS` rejection. If the failed
> attempt reaches the configured lockout threshold (`failedLoginAttempts + 1 >= maxFailedAttempts`),
> the core also emits a `LOCK_ACCOUNT` action. The shell does not decide whether locking is needed;
> it only executes the returned Action objects.

---

## 9. Test Cases

Each row is a directly executable test case. All inputs and expected outputs are derivable from the
schemas and decision matrix in Sections 3 and 4.

| ID | Scenario | Input summary | State summary | Config summary | Expected `decision` | Expected `rejectionReason` | Expected `verdict` | Expected actions |
|---|---|---|---|---|---|---|---|---|
| T-01 | Valid login — clean account | `eventType: LOGIN_ATTEMPT`, `passwordVerificationResult: true`, valid schema | `status: ACTIVE`, `failedLoginAttempts: 0`, rate limit clear, eventId not in dedup cache | Default config | `APPROVED` | `null` | `SUCCESS` | `CREATE_SESSION`, `RESET_FAILED_LOGIN_COUNTER`, `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| T-02 | Valid login — prior failures, notify enabled | `passwordVerificationResult: true` | `status: ACTIVE`, `failedLoginAttempts: 2`, rate limit clear | `notifyOnSuspiciousLogin: true` | `APPROVED` | `null` | `SUCCESS` | `CREATE_SESSION`, `RESET_FAILED_LOGIN_COUNTER`, `EMIT_AUDIT_EVENT`, `SEND_SECURITY_NOTIFICATION`, `EMIT_METRIC` |
| T-03 | Valid login — prior failures, notify disabled | `passwordVerificationResult: true` | `status: ACTIVE`, `failedLoginAttempts: 2`, rate limit clear | `notifyOnSuspiciousLogin: false` | `APPROVED` | `null` | `SUCCESS` | `CREATE_SESSION`, `RESET_FAILED_LOGIN_COUNTER`, `EMIT_AUDIT_EVENT`, `EMIT_METRIC` (no notification) |
| T-04 | Wrong password | `passwordVerificationResult: false` | `status: ACTIVE`, `failedLoginAttempts: 1`, rate limit clear | Default config | `REJECTED` | `INVALID_CREDENTIALS` | `FAILURE` | `REJECT_LOGIN`, `RECORD_FAILED_LOGIN_ATTEMPT`, `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| T-05 | Wrong password reaches lockout threshold | `passwordVerificationResult: false` | `status: ACTIVE`, `failedLoginAttempts: 4`, rate limit clear | `maxFailedAttempts: 5` | `REJECTED` | `INVALID_CREDENTIALS` | `FAILURE` | `REJECT_LOGIN`, `RECORD_FAILED_LOGIN_ATTEMPT`, `LOCK_ACCOUNT`, `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| T-06 | Account locked — active lock | `passwordVerificationResult: true` | `status: LOCKED`, `lockedAt: 5 minutes ago`, rate limit clear | `lockoutDurationMinutes: 30` | `REJECTED` | `ACCOUNT_LOCKED` | `FAILURE` | `REJECT_LOGIN`, `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| T-07 | Account locked — expired lock (lock age ≥ duration) | `passwordVerificationResult: true` | `status: LOCKED`, `lockedAt: 35 minutes ago` | `lockoutDurationMinutes: 30` | `APPROVED` | `null` | `SUCCESS` | `CREATE_SESSION`, `RESET_FAILED_LOGIN_COUNTER`, `EMIT_AUDIT_EVENT`, `EMIT_METRIC` (core proceeds; audit notes expired lock) |
| T-08 | Account disabled | `passwordVerificationResult: true` | `status: DISABLED` | Default config | `REJECTED` | `ACCOUNT_DISABLED` | `FAILURE` | `REJECT_LOGIN`, `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| T-09 | Rate limit exceeded | Valid event | `status: ACTIVE`, `attemptsInWindow: 10` | `rateLimitMaxAttempts: 10` | `REJECTED` | `RATE_LIMIT_EXCEEDED` | `FAILURE` | `REJECT_LOGIN`, `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| T-10 | Duplicate event | Same `eventId` as T-01 | `eventId` present in `processedEventIds` | Default config | `REJECT_DUPLICATE` | `DUPLICATE_EVENT` | `SUCCESS` | *(none)* |
| T-11 | Expired timestamp | `timestamp: (maxEventAgeSeconds + 1) seconds ago` | Valid state | `maxEventAgeSeconds: 300` | `REJECT_INVALID` | `TIMESTAMP_EXPIRED` | `FAILURE` | `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| T-12 | Schema validation failure — missing `eventId` | `eventId` field absent | Any | Default config | `REJECT_INVALID` | `SCHEMA_INVALID` | `FAILURE` | `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| T-13 | Schema validation failure — invalid `eventType` | `eventType: "LOGOUT_ATTEMPT"` | Any | Default config | `REJECT_INVALID` | `UNKNOWN_EVENT_TYPE` | `FAILURE` | `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| T-14 | Config version mismatch | Valid event | Valid state | `configVersion: 99` | `ABANDON` | `CONFIG_VERSION_MISMATCH` | `FAILURE` | `EMIT_AUDIT_EVENT` |
| T-15 | Missing state — `account` absent | Valid event | `account` field missing from snapshot | Default config | `REJECT_INVALID` | `STATE_MISSING` | `FAILURE` | `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| T-16 | Identifier mismatch | `payload.identifier: a@example.com` | `account.identifier: b@example.com` | Default config | `REJECT_INVALID` | `IDENTIFIER_MISMATCH` | `FAILURE` | `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| T-17 | Locked account — `lockedAt` is null (invariant I-07 violation) | Valid event | `status: LOCKED`, `lockedAt: null` | Default config | `REJECT_INVALID` | `STATE_MISSING` | `FAILURE` | `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |
| T-18 | `clientMeta` passed through to `CREATE_SESSION` action | `passwordVerificationResult: true`, `clientMeta: { userAgent: "Mozilla/5.0", ipAddress: "203.0.113.1" }` | `status: ACTIVE`, `failedLoginAttempts: 0`, rate limit clear | Default config | `APPROVED` | `null` | `SUCCESS` | `CREATE_SESSION` (with `clientMeta` in parameters), `RESET_FAILED_LOGIN_COUNTER`, `EMIT_AUDIT_EVENT`, `EMIT_METRIC` |

---

## 10. Observability and Audit

### Telemetry Fields

| Field | Type | Description | When emitted |
|---|---|---|---|
| `telemetry.durationMs` | integer | Total core execution time in ms (measured by the shell wrapping the core call) | Always |
| `telemetry.stepsExecuted` | string[] | Ordered list of pipeline step names that ran | Always |
| `telemetry.evaluatedChecks` | integer | Count of domain checks evaluated before verdict | Always |

### Audit Log

The `auditLog` field in `FunctionalResult` is an immutable, ordered record of every pipeline step.
One entry per step. It is the authoritative compliance and debugging trace.

**Required audit entries by pipeline step:**

| Audit `step` | Required for | Expected `outcome` values |
|---|---|---|
| `SCHEMA_VALIDATION` | All events | `PASS`, `FAIL` |
| `TIMESTAMP_CHECK` | All events that pass schema | `PASS`, `FAIL` |
| `IDEMPOTENCY_CHECK` | All events that pass timestamp | `PASS`, `DUPLICATE` |
| `IDENTIFIER_CONSISTENCY_CHECK` | All events that pass idempotency | `PASS`, `FAIL` |
| `ACCOUNT_STATUS_CHECK` | All events that pass identifier check | `PASS`, `LOCKED`, `LOCKED_EXPIRED`, `DISABLED` |
| `RATE_LIMIT_CHECK` | All events that pass account status | `PASS`, `RATE_LIMITED` |
| `CREDENTIAL_EVALUATION` | All events that pass rate limit | `PASS`, `FAIL` |
| `VERDICT_CREATION` | All events that reach this step | `APPROVED`, `REJECTED`, `REJECT_INVALID`, `REJECT_DUPLICATE`, `ABANDON` |
| `ACTION_CREATION` | All events that reach this step | `COMPLETE` |

### Metrics to Emit

| Metric name | Type | Labels | Description |
|---|---|---|---|
| `user_login_attempts_total` | counter | `decision`, `rejection_reason`, `account_status` | Total login attempts processed |
| `user_login_duration_ms` | histogram | `decision` | Core execution duration distribution |
| `user_login_failures_total` | counter | `rejection_reason` | Total failed login decisions |
| `user_login_sessions_created_total` | counter | — | Total sessions created (APPROVED decisions) |
| `user_login_duplicate_events_total` | counter | — | Total duplicate events detected |

### Security Audit Retention

The `EMIT_AUDIT_EVENT` action must be consumed by `platform.audit-log` and retained for the
duration specified by the applicable data-retention policy. Audit events are append-only and must
not be modified or deleted by the shell or any downstream consumer.

---

## 11. Imperative Shell Responsibilities

### 11.1 Before Calling the Core

The Imperative Shell must complete all of the following before calling `LoginCore`:

- [x] Load and validate `LoginConfig` from the configuration store. Verify `configVersion` matches the expected value (`1`).
- [x] Assemble `LoginStateSnapshot`: fetch `account` from the account store, `rateLimitState` from the rate-limit store, `processedEventIds` from the idempotency cache, and inject current UTC time as `currentTime`.
- [x] Validate or normalize `LoginAttemptEvent`: confirm required fields are present and `eventType` is `LOGIN_ATTEMPT`.
- [x] Perform the password hash comparison externally (via `auth.credential-verifier`) and inject the boolean result into `InputEvent.payload.passwordVerificationResult`. The raw password and hash must never reach the core.
- [x] Generate or propagate `traceId` and `correlationId` for observability.
- [x] Ensure no raw credentials, password hashes, or secret tokens are passed into the core.

### 11.2 After Calling the Core

The Imperative Shell must execute the following after receiving `LoginResult` from the core:

- [x] Execute each returned `Action` object in the specified priority order.
- [x] Enforce idempotency keys: use `Action.idempotencyKey` to prevent duplicate side effects if an action is retried.
- [x] Persist the audit log: send all `EMIT_AUDIT_EVENT` actions to `platform.audit-log`. Must not be suppressed.
- [x] Emit telemetry: send `EMIT_METRIC` actions to `platform.metrics`.
- [x] Execute session creation: send `CREATE_SESSION` action to `auth.session-manager`. Return the generated session token to the caller.
- [x] Handle retries: if an action fails transiently, retry with exponential backoff; do not re-evaluate business logic.
- [x] Do not interpret or re-evaluate the `decision` or `verdict` fields. The core's decision is final.

### 11.3 What the Shell Must Never Do

- Must not perform the password hash comparison after the core has received input.
- Must not create a session without a `CREATE_SESSION` action returned by the core.
- Must not modify the `FunctionalResult` before executing actions.
- Must not suppress or swallow `EMIT_AUDIT_EVENT` actions.
- Must not expose `rejectionReason` or internal reason codes directly to the end-user API response.

---

## 12. Source Traceability

Records where the technical contract elements in this Yang Core Module originated.

| Source | Type | Section / block | Contract element derived |
|---|---|---|---|
| `examples/user-login/user_login_intent.md` | Yin Page | §6 Domain Logic / Business Rules | Decision pipeline rules: lockout thresholds, rate-limit behavior, credential verification model |
| `examples/user-login/user_login_intent.md` | Yin Page | §7 Workflows | Login attempt workflow steps; error flow paths for locked, disabled, and rate-limited accounts |
| `examples/user-login/user_login_intent.md` | Yin Page | §10 Roles, Permissions, Privacy, and Safety | Security constraints: no credential exposure in results, audit retention requirement, shell responsibility boundaries |
| `Docs/03_Yin_Yang_Contracts.md` | Framework Document | Functional Core / Imperative Shell | Core signature pattern, action object model, idempotency anchor convention |
| `Templates/yang/yang-core-module/03_yang_template.md` | Yang Template | All sections | Document structure, required contract elements, and Pre-Flight Gap-Check format |

> This is a framework example document. There are no external master documents, issue tickets, or production code references. In a real project, this table would reference the product's master specification, linked issue tracker items, and any existing code or schema files from which the contract was derived.

---

## 13. Yin/Yang Trace Map

Maps every product requirement from the paired Yin document to its technical contract location
in this Yang document. All rows must be filled before code generation begins.

| Yin Requirement (Domain / Workflow) | Yang Contract Location | Test Case |
|---|---|---|
| Module validates credentials and checks account status before allowing login | Decision Pipeline Steps 5, 7; Decision Matrix rows `INVALID_CREDENTIALS`, `ACCOUNT_LOCKED`, `ACCOUNT_DISABLED` | T-01, T-04, T-05, T-07 |
| Account is temporarily locked after repeated failed attempts | Decision Pipeline Step 7; Config field `maxFailedAttempts`; Actions `RECORD_FAILED_LOGIN_ATTEMPT` and `LOCK_ACCOUNT`; Invariant I-07 | T-04, T-05 |
| Locked account is released after the lockout duration elapses | Decision Pipeline Step 5 — Lock Expiry Evaluation; Config field `lockoutDurationMinutes` | T-07 |
| Disabled accounts can never log in | Decision Pipeline Step 5 — `DISABLED` path; Decision Matrix row `ACCOUNT_DISABLED` | T-08 |
| Rate limiting prevents brute-force attacks | Decision Pipeline Step 6; Config fields `rateLimitWindowSeconds`, `rateLimitMaxAttempts`; State Snapshot `rateLimitState` | T-09 |
| Successful login creates a session | Action `CREATE_SESSION`; Action Sets table — APPROVED paths | T-01, T-02, T-03, T-07 |
| Failed-attempt counter is reset on successful login | Action `RESET_FAILED_LOGIN_COUNTER` | T-01, T-02 |
| Security notification is sent when a login succeeds after prior failures | Action `SEND_SECURITY_NOTIFICATION`; Config field `notifyOnSuspiciousLogin`; Decision Pipeline Step 8 | T-02, T-03 |
| Every login decision is audited | `FunctionalResult.auditLog`; Invariant I-11; Action `EMIT_AUDIT_EVENT`; Section 10 Audit Log | T-01 through T-18 |
| Duplicate login events produce no side effects | Section 6 Idempotency; Decision Pipeline Step 3; Decision Matrix row `REJECT_DUPLICATE` | T-10 |
| Failure reasons must not be disclosed to the client | `FunctionalResult.rejectionReason` — internal only; Action `REJECT_LOGIN` carries internal reason only; Yin security note | T-04, T-05, T-07, T-08 |
| The core never performs the password hash comparison | `InputEvent.payload.passwordVerificationResult` — injected boolean; Core never calls a hash function | Architectural constraint — no dedicated test case needed |
| Current time is injected, never read from system clock | `StateSnapshot.currentTime`; Invariant I-12 | T-10 (time injection verified in timestamp-check test) |
| All configuration thresholds are adjustable without code changes | Section 3.1 Configuration Schema — all threshold fields are config-driven | T-05, T-06, T-08, T-10 |
| `clientMeta` (userAgent, ipAddress) is passed through to session creation | `InputEvent.payload.clientMeta`; `CREATE_SESSION` action parameters | T-18 |

---

## 14. Open Questions / Contract Gaps

None for this example. All contract-critical login decision behavior is specified.

---

## 15. Pre-Flight Gap-Check

Run this checklist before submitting this document to an AI for code generation.
All 14 checks must pass. A failed check means the contract is incomplete — resolve the gap first.

- [x] **1. Configuration Schema complete?** Section 3.1 defines all required and optional config fields with types, constraints, and descriptions.
- [x] **2. State Snapshot Schema complete?** Section 3.2 defines `account`, `rateLimitState`, `processedEventIds`, and `currentTime` with all required sub-fields.
- [x] **3. Input Event Schema complete?** Section 3.3 defines the `LOGIN_ATTEMPT` discriminated-union event with all required and optional fields.
- [x] **4. Functional Result Schema complete?** Section 3.4 defines `verdict`, `decision`, `rejectionReason`, `reason`, `actions`, `telemetry`, and `auditLog` with full sub-schemas including the `Action` definition.
- [x] **5. Actions fully defined?** Section 5 lists all 7 action types with priority, trigger condition, key parameters, and idempotency key. No direct I/O inside the core.
- [x] **6. Idempotency defined?** Section 6 specifies the idempotency key field (`eventId`), the dedup cache field (`processedEventIds`), the detection strategy (exact UUID match), the duplicate result, and the minimum cache TTL.
- [x] **7. Errors and edge cases covered?** Section 8 covers: invalid schema, config mismatch, expired timestamp, duplicate event, identifier mismatch, unknown event type, missing state, locked account (active and expired lock), locked account with null `lockedAt`, disabled account, rate limit exceeded, wrong password, wrong password at lockout threshold, successful login with prior failures.
- [x] **8. Test cases present?** Section 9 provides 18 test cases covering: valid login (clean and with prior failures), notify enabled/disabled, wrong password, locked (active and expired), disabled, rate limited, duplicate, expired timestamp, schema failure, unknown event type, config mismatch, missing state, identifier mismatch, invariant violation, and clientMeta passthrough.
- [x] **9. Trace Map complete?** Section 13 maps all 15 Yin requirements to Yang contract locations and test case IDs. No empty cells.
- [x] **10. English only?** The entire Yang section is in English.
- [x] **11. No secrets present?** No API keys, passwords, tokens, or credential values appear anywhere in this document. `$ENV_SESSION_SECRET` and `$ENV_SESSION_EXPIRY_SECONDS` are referenced by name only.
- [x] **12. No direct I/O in core?** The core performs zero database writes, HTTP calls, file reads/writes, queue operations, email sends, or system time reads. All side effects are returned as Action objects for the Imperative Shell.
- [x] **13. Splice divider in place?** The `---` divider is present between the Yin and Yang sections, with the Splice note above it.
- [x] **14. All Yin sections present?** All 11 mandatory Yin sections are present and non-empty.

**All 14 checks must pass before this example is treated as complete.**

---

## 16. Implementation Handoff Notes

This example is a framework reference document, not a model-specific implementation handoff.

**Target AI model:** `Unknown`
**Target platform / execution environment:** `Unknown`
**Model reference provided:** `No`
**Platform reference provided:** `No`
**Handoff mode:** `Universal Markdown if used as implementation context`

Rules:

- Do not claim model-optimized output unless the matching model reference is provided and used.
- Do not claim platform-optimized output unless the matching platform reference is provided and used.
- If no references are provided, use Universal Markdown fallback.

---

## 17. Summary

`UserLoginCore` defines the deterministic login-decision contract for email-and-password authentication. It receives configuration, injected account and rate-limit state, and a `LOGIN_ATTEMPT` event. It produces a structured result containing the decision, reason, Action objects, telemetry, and audit log.

The Functional Core performs no I/O, does not compare password hashes, does not create sessions, does not write account state, and does not emit logs directly. Those side effects are represented as Action objects for the Imperative Shell.

All login outcomes, lockout behavior, duplicate handling, audit expectations, and security boundaries are explicitly defined and testable.
