# TransVoice Notes — Codex Agent Operating Rules

This file defines how Codex and any delegated subagents must work inside this repository.

## Instruction priority

1. The user's current explicit instruction.
2. `MASTER_PROMPT.md` — product and engineering constitution.
3. `docs/PROJECT_STATE.md` — current factual phase/state once it exists.
4. This `AGENTS.md` — repository-wide operating rules.
5. `CODEX.md` — reusable workflow conventions and command-like prompts.
6. More-specific nested `AGENTS.md` files, when they do not conflict with higher-priority product rules.

If instructions conflict, identify the conflict and follow the highest-priority instruction. Do not silently reinterpret a founder-approved product decision.

## Required startup behavior

Before substantial work:

- read `MASTER_PROMPT.md` completely;
- read `docs/PROJECT_STATE.md` if it exists;
- inspect `git status`, current branch, remotes, and recent history;
- inspect the actual files relevant to the requested task;
- determine the currently allowed phase;
- state the task goal and success criteria in plain language;
- keep the change within the current phase unless the user explicitly changes scope.

Do not assume repository state from an earlier session.

## Root-agent ownership

The root Codex agent owns:

- final interpretation of the user request;
- scope and phase compliance;
- architecture decisions within approved boundaries;
- integration of subagent findings;
- final file edits unless delegation is clearly safer;
- verification strategy;
- truthful completion reporting.

Subagents advise, investigate, review, test, or implement isolated work. They do not independently redefine the product constitution.

## Subagent delegation

Use subagents when parallel work can materially improve speed or quality. Do not delegate trivial edits.

Preferred reviewer roles:

1. **Product / Scope Reviewer** — MVP necessity, YAGNI, product coherence.
2. **Mobile Platform Reviewer** — iOS/Android lifecycle, permissions, background behavior, native boundaries.
3. **Speech / Language Reviewer** — whisper.cpp, Taglish, source transcript, English normalization, vocabulary, model/data licensing.
4. **Privacy / Security Reviewer** — threat model, local/cloud boundaries, secrets, uploads, retention, data exposure.
5. **QA / Adversarial Reviewer** — failure cases, race conditions, regressions, unsupported assumptions.
6. **Performance Reviewer** — RAM, CPU, battery, thermal behavior, queues, backpressure, low-end devices.

Delegate aggressively for cross-cutting or risky changes, especially:

- recording engine changes;
- native module changes;
- speech/model changes;
- canonical-English logic;
- cloud Improve Transcript;
- authentication/billing;
- database migrations;
- privacy/security-sensitive behavior;
- release-critical changes.

For small UI copy, spacing, or isolated reversible edits, the root agent may work alone.

## Agent ownership rules

- Give each subagent a narrow question, file area, or review objective.
- Avoid multiple agents editing the same files concurrently.
- Prefer review-only delegation when overlap would create merge risk.
- The root agent reconciles contradictory findings.
- A subagent may not commit, push, merge, change remotes, delete branches, or alter product scope unless the user explicitly authorizes that exact action.
- Subagents must report evidence, uncertainties, files inspected, and tests actually run.
- A subagent result is not automatically accepted; the root agent validates it before integration.

## Adversarial QA rule

For any non-trivial feature or architectural change, perform an adversarial review before declaring completion.

The adversarial reviewer should ask:

- How can this lose or corrupt a recording?
- What happens after process death, backgrounding, interruption, or low storage?
- What happens when transcription is missing, slow, wrong, or unavailable?
- Can uncertainty, negation, names, dates, amounts, or responsibility be reversed?
- Can user edits be overwritten?
- Can duplicate actions create double writes, double jobs, or double charges?
- Can queues grow without bounds?
- Can private transcript/audio content leak into logs, analytics, crash reports, or cloud requests?
- Can untrusted transcript text manipulate downstream AI behavior?
- Is the implementation claiming something that was never physically tested?

High-risk findings must be fixed, explicitly accepted as limitations, or recorded as blockers/risks before phase completion.

## Goal discipline

Every significant task must have one concise goal with observable success criteria.

Use the `/goal` convention described in `CODEX.md` when the client supports it. If the client does not recognize `/goal` as a native command, treat the same text as a normal project instruction.

The active goal must never override:

- the current phase boundary;
- recording-first reliability;
- privacy rules;
- evidence requirements;
- explicit user instructions.

## MVP scope discipline

Before adding a major feature, infrastructure component, dependency, table, service, or abstraction, run the `/scope-mvp` reasoning contract in `CODEX.md`.

Classify the proposal as exactly one of:

- `MUST_HAVE`
- `SHOULD_HAVE`
- `RESEARCH_FIRST`
- `POST_MVP`
- `REJECT_YAGNI`

A proposal classified `POST_MVP` or `REJECT_YAGNI` must not be implemented unless the user explicitly overrides the classification.

## Anti-architecture-theater rule

Knowing distributed-system concepts is required; deploying them prematurely is not.

Do not add Kubernetes, Kafka, sharding, service discovery, distributed locks, Saga, CQRS, event sourcing, multi-region active-active, Redis, queues, API gateways, or microservices unless the current measured workload or failure mode requires them and the current phase allows them.

Prefer the smallest system that can be tested and understood.

## Recording-first rule

Whenever performance, memory, CPU, battery, transcription, UI updates, or background work compete with audio preservation:

**recording wins.**

Speech work may be slowed, deferred, dropped from the live queue, or re-run from saved audio. Audio writing must not be blocked to preserve an intelligence feature.

## Evidence and verification

Never report:

- a command passed if it was not run;
- a device test passed if it was not physically performed;
- a privacy/encryption property that is not implemented and verified;
- Taglish quality without benchmark evidence;
- performance numbers that were not measured.

Use the evidence statuses defined by `MASTER_PROMPT.md`.

Run tests proportional to the change. Do not create meaningless tests solely to increase test count.

## Git safety

Unless the user explicitly requests otherwise:

- do not commit automatically;
- do not push automatically;
- do not change remotes;
- do not force-push;
- do not delete branches;
- do not rewrite history;
- do not merge pull requests.

When the user explicitly authorizes a commit/push for a task, that authorization applies only to the requested scope.

## Communication

Use concise, plain English by default.

For long tasks, give short progress updates after meaningful milestones. Report blockers with the smallest actionable explanation.

At the end of a phase, use the completion format required by `MASTER_PROMPT.md` and stop.
