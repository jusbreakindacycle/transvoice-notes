# TransVoice Notes — Codex Workflow Conventions

This file provides reusable project-level workflow prompts for Codex. `MASTER_PROMPT.md` remains the product constitution; `AGENTS.md` defines repository-wide agent behavior.

These `/...` forms are project conventions. If the Codex client recognizes a command natively, use it. If it does not, paste/type the same text as an ordinary prompt; the semantics below still apply.

---

## `/goal` — set the active engineering goal

### Purpose

Keep a session focused on one outcome rather than a list of attractive tasks.

### Usage

```text
/goal <one outcome>
```

Example:

```text
/goal Prove whether local English/Filipino/Taglish transcription can deliver an almost-immediate Live Draft and an accurate Final Pass on target iOS and Android devices without compromising recording reliability.
```

### Required response

Codex should restate:

```text
ACTIVE GOAL
<goal>

SUCCESS CRITERIA
- <observable result>
- <observable result>

CURRENT PHASE
<phase>

OUT OF SCOPE
- <items explicitly not required to achieve this goal>

EVIDENCE REQUIRED
- <tests / measurements / inspection needed>
```

### Rules

- One active goal at a time.
- The goal must fit the currently allowed phase.
- Do not silently expand a goal into adjacent product work.
- If a new user request changes the goal, explicitly replace or amend it.
- Completing many tasks does not count as success if the goal was not proven.

---

## `/scope-mvp` — challenge a proposed feature before building it

### Purpose

Prevent feature creep and architecture theater while keeping important differentiation.

### Usage

```text
/scope-mvp <feature, service, dependency, infrastructure idea, or abstraction>
```

### Evaluation questions

Codex must answer:

1. What user problem does this solve?
2. Is that problem part of the local MVP or the currently allowed phase?
3. Can the core product succeed without it?
4. Does it improve one of the primary differentiators: Taglish fidelity, critical meaning, recording reliability, personal vocabulary, local privacy, or usable memory/search?
5. What complexity does it introduce?
6. Does it require native code, cloud infrastructure, account identity, billing, or new permissions?
7. What privacy/security risk does it create?
8. What performance/storage/battery cost does it create?
9. What is the smallest simpler alternative?
10. What evidence would justify adding it now?

### Required classification

Return exactly one:

- `MUST_HAVE` — MVP/core differentiation fails without it.
- `SHOULD_HAVE` — valuable and low enough risk, but MVP can technically exist without it.
- `RESEARCH_FIRST` — decision depends on evidence not yet available.
- `POST_MVP` — useful but should not delay the local MVP.
- `REJECT_YAGNI` — no current evidence-backed need.

### Required output

```text
SCOPE DECISION: <classification>

User problem:
...

Why now / why not now:
...

Smallest acceptable version:
...

Risks:
...

Evidence needed:
...

Phase placement:
...
```

### Examples

```text
/scope-mvp Kubernetes
```

Expected direction: `REJECT_YAGNI` while the product is local-first and has no measured orchestration need.

```text
/scope-mvp My Vocabulary
```

Expected direction: `MUST_HAVE` or `SHOULD_HAVE` depending on the current phase because user-approved vocabulary directly addresses names, technical terms, and Taglish adaptation.

```text
/scope-mvp vector database
```

Expected direction: `POST_MVP` or `RESEARCH_FIRST` until SQLite FTS is proven insufficient.

---

## `/delegate` — use subagents deliberately

### Usage

```text
/delegate <task>
```

The root agent should choose only the relevant reviewers from:

- Product / Scope Reviewer
- Mobile Platform Reviewer
- Speech / Language Reviewer
- Privacy / Security Reviewer
- QA / Adversarial Reviewer
- Performance Reviewer

### Delegation contract

Each delegated task must define:

```text
OBJECTIVE
...

SCOPE
...

FILES / AREAS
...

DO NOT CHANGE
...

EVIDENCE TO RETURN
...

OUTPUT
findings + risks + recommendation
```

Use parallel read/review work when it saves time or increases confidence. Avoid concurrent edits to the same files.

The root agent owns the final decision.

---

## `/adversarial-review` — try to break the current solution

### Usage

```text
/adversarial-review <feature/change>
```

### Required attack areas

Check at least:

- data loss;
- race conditions;
- idempotency;
- process interruption;
- low storage;
- missing/corrupt model;
- queue/backpressure failure;
- user-edit preservation;
- language meaning reversal;
- privacy leakage;
- unauthorized cloud upload;
- duplicate cloud processing or billing;
- unsupported capability claims;
- iOS/Android divergence;
- rollback/migration safety when applicable.

### Result classifications

- `PASS`
- `PASS_WITH_LIMITATIONS`
- `CHANGES_REQUIRED`
- `BLOCKED`

Do not use `PASS` merely because unit tests passed.

---

## `/verify` — evidence before completion

### Usage

```text
/verify <task or phase>
```

Codex should list:

```text
AUTOMATED
- command → real result

MANUAL
- check → result / NOT PERFORMED

PHYSICAL DEVICE
- device/test → result / NOT PERFORMED

UNVERIFIED CLAIMS
- ...

EVIDENCE STATUS
- ...
```

A missing physical-device check must stay explicitly unverified when the feature depends on real microphone/background/performance behavior.

---

## `/phase` — work on exactly one project phase

### Usage

```text
/phase <number>
```

Equivalent session instruction:

```text
Read MASTER_PROMPT.md, AGENTS.md, CODEX.md, and docs/PROJECT_STATE.md if present.
Inspect the repository and Git state.
Work on PHASE <number> only.
Set one active goal for the phase.
Use /scope-mvp reasoning before introducing substantial new scope.
Delegate risky parallel research/review when it improves quality.
Run proportional verification.
Perform adversarial QA for non-trivial changes.
Update required project-state/risk/decision documentation.
Stop after the phase completion report.
```

---

# Default root-agent loop

For significant work, use this loop:

```text
1. INSPECT
   repository + current phase + evidence

2. GOAL
   define one measurable outcome

3. SCOPE
   challenge major additions with /scope-mvp

4. DELEGATE
   parallelize research/review when useful

5. IMPLEMENT
   smallest coherent change

6. VERIFY
   run real tests/checks

7. ADVERSARIAL REVIEW
   attempt to break assumptions and failure handling

8. REPAIR
   fix material findings or document a blocker/limitation

9. UPDATE STATE
   project state + risks + decisions + evidence

10. REPORT AND STOP
    phase completion report; do not silently start the next phase
```

Loop only while new evidence or failures justify another pass. Do not churn after acceptance criteria are met.

---

# Suggested delegation matrix

| Change | Product | Mobile | Speech | Security | QA | Performance |
|---|---:|---:|---:|---:|---:|---:|
| UI copy/layout | optional |  |  |  | optional |  |
| Recording engine |  | yes | optional | optional | yes | yes |
| whisper.cpp/model | optional | yes | yes | optional | yes | yes |
| Canonical English | yes |  | yes | optional | yes | optional |
| My Vocabulary | yes |  | yes | yes | yes |  |
| SQLite migration | optional |  |  | yes | yes | optional |
| Cloud Improve | yes | optional | yes | yes | yes | yes |
| Auth/billing | yes | optional |  | yes | yes | optional |
| Release | yes | yes | yes | yes | yes | yes |

`yes` means strongly preferred for non-trivial changes, not that every reviewer must edit code.

---

# Stop conditions

Stop and report instead of pretending success when:

- the current phase exit criteria cannot be met;
- required hardware/credentials are unavailable for a mandatory verification;
- model/data licensing is unresolved for a commercial dependency;
- a recording-safety risk remains uncontrolled;
- a privacy/security blocker would expose user data;
- the implementation requires a founder product decision not already authorized.

When some work is still safe and useful, complete that work before reporting the blocker.
