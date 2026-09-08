# Project Phases

Last updated: 2026-09-09

The phase boundaries are mandatory unless the founder explicitly changes them.

## Phase 0 — Repository + Product + Architecture Foundation

Create factual control documents, architecture, risks, benchmark strategy, current tech-stack research, and local environment preflight.

No product source code.

**Current status:** IN PROGRESS — repository research/documentation can be completed remotely, while local Windows/Android/EAS tooling remains unverified.

## Phase 1 — Expo Cross-Platform Scaffold

Build the cross-platform application shell:

- current stable Expo;
- TypeScript;
- Expo Router;
- design system;
- Home;
- Search;
- Settings;
- Record entry;
- mock Note Detail;
- accessibility basics;
- EAS/Development Build setup.

No production speech engine.

## Phase 2 — Speech + Audio Feasibility Spike

Prove or disprove the central technical assumption before too much product code exists.

Benchmark candidate on-device configurations for:

- English;
- Filipino;
- Taglish;
- Live Draft latency;
- final-pass accuracy;
- critical-meaning preservation;
- memory;
- CPU;
- battery;
- thermal behavior;
- model size;
- iOS and Android compatibility.

Outcome must be one of:

- FEASIBLE;
- FEASIBLE WITH LIMITATIONS;
- NOT YET FEASIBLE.

## Phase 3 — Local Data + Storage

Implement:

- SQLite;
- migrations;
- FTS;
- repositories;
- settings;
- file layout;
- secure small-secret storage;
- model metadata.

## Phase 4 — Production Recording Engine

Implement recording independently from transcription.

Must prove:

- authoritative microphone path;
- incremental writing;
- pause/resume;
- background/lock behavior;
- recovery;
- low-storage behavior;
- idempotent stop;
- audio remains playable.

## Phase 5 — Library + Playback

Make the app useful without speech:

- note list;
- rename;
- favorite;
- delete;
- manual note;
- playback;
- seek;
- recovery UI.

## Phase 6 — Model Manager + Live Draft + Final Source Transcript

Productionize local speech:

- model install/remove;
- checksum;
- partial download handling;
- Live Draft;
- final source pass;
- timestamps;
- editing;
- capability profiles.

## Phase 7 — Canonical English + My Vocabulary + Critical Meaning

Implement core differentiation:

- meaning-preserving English;
- source/English toggle;
- user-approved vocabulary;
- correction memory;
- important-detail extraction;
- critical-detail review.

## Phase 8 — Search + Summary + Grounded Assistant

Implement:

- FTS;
- snippets;
- timestamp jump;
- local summary;
- actions;
- grounded Q&A;
- no-evidence fallback.

No vector database unless evidence justifies it.

## Phase 9 — Export + Privacy + Security + Accessibility

Finish a trustworthy local MVP:

- TXT/Markdown/audio export;
- privacy UX;
- deletion;
- threat model controls;
- accessibility audit;
- diagnostics;
- storage management.

A public local-MVP candidate may exist after this phase.

## Phase 10 — Optional Cloud Improve

Only after the local product is stable.

Add:

- backend decision;
- auth/entitlement;
- signed temporary uploads;
- improve jobs;
- rate limits;
- quotas;
- idempotency;
- provider abstraction;
- retries;
- retention/deletion controls;
- privacy impact update.

## Phase 11 — Account + Monetization

Only after product value and cloud costs are measured.

Implement store-compliant entitlements, restore flows, optional account, and paid tiers.

Free local use remains accountless.

## Phase 12 — Hardening + Competitive Benchmark

Run long recordings, failures, low storage, battery/thermal tests, and the formal competitor benchmark.

Fix critical problems and document limitations.

## Phase 13 — Release + Portfolio

Prepare:

- release checklist;
- screenshots;
- README;
- demo flow;
- architecture diagram;
- measured performance;
- privacy explanation;
- benchmark method;
- store metadata;
- changelog;
- portfolio case study.

## Rule

At the end of each phase, update `docs/PROJECT_STATE.md`, verification evidence, decisions, and risks, then stop before the next phase.
