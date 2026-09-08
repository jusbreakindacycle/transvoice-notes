# TransVoice Notes

**Record. Transcribe. Remember.**

TransVoice Notes is an early-stage local-first iOS and Android voice-memory app being built for natural English, Filipino, Tagalog, and Taglish speech.

The product goal is simple: preserve the recording first, create a useful live draft quickly, produce a more accurate source transcript, turn that into clear English without changing the speaker's meaning, and make the result searchable and useful as personal memory.

> Status: **Pre-implementation / Phase 0 foundation**

## Current product direction

TransVoice Notes is intended to:

- record reliably even when speech/AI features fail;
- work without an account for local use;
- support iOS and Android;
- use Expo + React Native + TypeScript for most UI/application logic;
- use a small native boundary for recording and on-device speech where required;
- treat English, Filipino/Tagalog, Taglish, and mixed speech as first-class input;
- preserve a timestamped source transcript;
- show an English canonical transcript by default;
- learn user-approved vocabulary corrections locally;
- flag important details such as names, amounts, dates, times, deadlines, negation, and uncertainty;
- keep cloud processing optional and explicit.

## Not production-ready

Nothing in this repository should currently be interpreted as a verified product capability.

There is not yet:

- an Expo application;
- production recording code;
- a speech engine integration;
- a local database implementation;
- a backend;
- an account system;
- billing;
- verified Taglish accuracy;
- verified physical-device performance.

Capabilities become claimable only after implementation and evidence.

## Product principle

```text
RELIABLE AUDIO
     ↓
TRACEABLE SOURCE TRANSCRIPT
     ↓
MEANING-PRESERVING ENGLISH
     ↓
IMPORTANT DETAILS
     ↓
SEARCHABLE PERSONAL MEMORY
```

If transcription fails, the recording must remain usable.

If English normalization fails, the source transcript and audio must remain available.

If AI fails, the note must still be useful.

## Development approach

The project uses a phase-gated workflow. See:

- `MASTER_PROMPT.md` — product and engineering constitution;
- `AGENTS.md` — repository-wide Codex agent rules;
- `CODEX.md` — reusable `/goal`, `/scope-mvp`, delegation, verification, and adversarial-review conventions;
- `docs/PHASES.md` — implementation phases;
- `docs/PROJECT_STATE.md` — current factual status;
- `docs/RISK_REGISTER.md` — known product and engineering risks.

Codex should be used primarily for implementation, local builds, native integration, tests, and device-facing engineering. Product research, architecture, risk analysis, and evidence review should remain explicit rather than improvised during coding.

## Repository status

The repository intentionally has no open-source license yet. Do not assume permission to reuse or redistribute the code beyond what copyright law otherwise allows.

## Current next step

Complete the local development-environment preflight documented in `docs/TECH_STACK.md`, then mark Phase 0 complete only when those local facts are verified.

After Phase 0 is complete, the next implementation phase is:

**Phase 1 — Expo cross-platform scaffold.**
