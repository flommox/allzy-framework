---
id: "allzy.examples.auth.user-login.yin-page"
title: "User Login & Auth — Yin Page"
artifact_type: "Example"
document_type: "Yin Page"
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
  - yin
  - yin-page
  - user-login
  - authentication
  - allzy-framework
aliases: []
summary: "Example Yin Page for the User Login & Auth module. Demonstrates the full Yin Page format including domain rules, workflows, UI concepts, data definitions, roles, integrations, and scope boundaries."
retrieval_description: "Retrieve this example when learning how to write a Yin Page for an authentication or login module, or when looking for a filled Yin Page example demonstrating the full framework structure."
source:
  generated_from_template: "Templates/yin/yin-page/02_yin_template.md"
  framework_references:
    - "Docs/07_Metadata_Config_and_Retrieval_Conventions.md"
    - "Docs/08_Glossary_and_Terminology.md"
scope:
  domain: "authentication"
  module_id: "auth.user-login"
yin_yang:
  is_yin_yang_document: false
  yin_document: "allzy.examples.auth.user-login.yin-page"
  yang_document: "allzy.examples.auth.user-login.yang-core-module"
  paired_yin: "allzy.examples.auth.user-login.yin-page"
  paired_yang: "allzy.examples.auth.user-login.yang-core-module"
  paired_yang_file: "Examples/user-login/user_login_core_contract.md"
  combined_example_file: "Examples/user-login/user_login_full.md"
retrieval:
  retrieval_ready: true
  retrieval_confidence: "high"
  retrieval_priority: "supporting"
  preferred_retrieval_keys:
    - "auth.user-login"
    - "user-login-example"
    - "yin-page-example"
  excluded_from_retrieval: false
  exclusion_reason: ""
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
