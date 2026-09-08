# Architecture Decision Records

Last updated: 2026-09-09

## ADR-001 — iOS and Android are first-class product platforms

- Status: Accepted
- Context: The product is intended for personal use first but may become a consumer product.
- Decision: Design product contracts for iOS and Android from the beginning.
- Consequences: Shared UI/domain logic is preferred, while recording/background behavior may remain platform-native.

## ADR-002 — Expo + React Native + TypeScript for the application layer

- Status: Accepted, implementation version pending Phase 1 verification
- Context: The founder uses VS Code and wants fast cross-platform iteration.
- Decision: Use Expo/React Native/TypeScript unless Phase 1 discovers a blocking native limitation.
- Consequences: Expo Go is limited to prototype-compatible work. Development Builds become the real test environment once native modules are needed.

## ADR-003 — One authoritative microphone capture path

- Status: Accepted
- Context: Competing microphone consumers risk instability and data loss.
- Decision: Recording, metering, and transcription derive from one authoritative capture pipeline.
- Consequences: Audio writing outranks speech processing. Speech may catch up from saved audio.

## ADR-004 — Live Draft and Final Transcript are different states

- Status: Accepted
- Context: The product requires near-immediate text and strong accuracy.
- Decision: Use a fast provisional Live Draft plus a higher-accuracy final source pass.
- Consequences: Draft text may visibly change. UI must communicate provisional status.

## ADR-005 — Preserve source transcript and canonical English separately

- Status: Accepted
- Context: Direct translation can lose negation, uncertainty, names, or other evidence.
- Decision: Store source/mixed-language transcript as evidence and derive English canonical text separately.
- Consequences: Additional text storage is accepted because traceability is a product requirement.

## ADR-006 — whisper.cpp is the primary multilingual candidate, not a guaranteed production selection

- Status: Accepted
- Context: whisper.cpp supports iOS/Android, local inference, quantization, VAD, and a permissive license.
- Decision: Benchmark whisper.cpp in Phase 2 behind a replaceable transcription abstraction.
- Consequences: No Taglish or low-end-device claim is allowed before measurements.

## ADR-007 — Vosk Filipino is not the commercial product foundation

- Status: Accepted
- Context: The currently listed Filipino Vosk model is CC BY-NC-SA 4.0.
- Decision: It may be used only for research/benchmarking within license constraints unless separate commercial rights are obtained.
- Consequences: Avoid architectural dependence on that model.

## ADR-008 — Local-first, accountless core

- Status: Accepted
- Context: Recording and local note value should not require identity or cloud infrastructure.
- Decision: Free local use requires no account.
- Consequences: Authentication is postponed until a feature actually needs identity.

## ADR-009 — Cloud processing requires explicit user action

- Status: Accepted
- Context: Private audio should not leave the device by default.
- Decision: Cloud processing occurs only through an explicit Improve Transcript action.
- Consequences: Local failure never silently triggers upload.

## ADR-010 — My Vocabulary learns only with user approval

- Status: Accepted
- Context: Personal vocabulary can improve recognition but can also reveal sensitive information.
- Decision: Do not silently learn terms from recordings.
- Consequences: Corrections may trigger a "Remember this?" prompt.

## ADR-011 — Critical Meaning Check is a first-class quality metric

- Status: Accepted
- Context: WER can hide serious semantic errors.
- Decision: Separately test names, money, dates, times, negation, uncertainty, responsibility, and technical terms.
- Consequences: Benchmarks and UI must include high-impact detail review.

## ADR-012 — SQLite/FTS before semantic/vector infrastructure

- Status: Accepted
- Context: Local title/transcript search does not initially require embeddings or a vector database.
- Decision: Use SQLite + FTS first.
- Consequences: Vector search remains evidence-gated.

## ADR-013 — Managed cloud before distributed infrastructure

- Status: Accepted
- Context: The local MVP has no backend load.
- Decision: If cloud features begin, start with a managed control plane and narrow workers/providers.
- Consequences: No Kubernetes, sharding, Kafka, microservices, or multi-region design without measured need.

## ADR-014 — Repository license remains undecided

- Status: Accepted
- Context: The repository is public and may contain commercially differentiating implementation later.
- Decision: Do not add an open-source license automatically.
- Consequences: Licensing strategy requires an explicit founder decision.

## ADR-015 — Project state is factual state, not higher-level policy

- Status: Accepted
- Context: `PROJECT_STATE.md` can become stale and should not override repository operating policy.
- Decision: Root instruction precedence is: current explicit user instruction → MASTER_PROMPT → root AGENTS → nested AGENTS → PROJECT_STATE factual state → CODEX workflow conventions.
- Consequences: `AGENTS.md` must reflect this precedence.
