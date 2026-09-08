# Risk Register

Last updated: 2026-09-09

Status values: `OPEN`, `VALIDATING`, `MITIGATED`, `ACCEPTED_LIMITATION`, `CLOSED`.

| ID | Category | Risk | Impact | Likelihood | Mitigation / validation | Status |
|---|---|---|---|---|---|---|
| R-001 | Recording | Process/background interruption corrupts or loses audio | Critical | Medium | Incremental writing, recovery metadata, idempotent finalization, physical-device tests | OPEN |
| R-002 | Recording | Speech processing blocks audio writer | Critical | Medium | One capture path, bounded speech queue, audio priority, post-recording catch-up | OPEN |
| R-003 | Recording | Long PCM/WAV recordings consume excessive storage | High | High | Measure bytes/hour, warn on low storage, evaluate verified post-finalization compression later | OPEN |
| R-004 | Recording | Android manufacturer battery controls terminate long recording | High | Medium | Foreground microphone service, device-specific QA, user guidance where required | OPEN |
| R-005 | Recording | iOS interruption/route change leaves session inconsistent | High | Medium | AVAudioSession interruption/route handling, physical-device tests | OPEN |
| R-006 | Speech | Tiny/base models are too inaccurate for natural Taglish | Critical | Medium/High | Phase 2 benchmark, model ladder, personal vocabulary, final pass, optional cloud improvement later | VALIDATING |
| R-007 | Speech | Better model is too slow/hot for ordinary Android phones | Critical | High | Capability profiles, Live Draft/final split, quantization, VAD, measured fallback | VALIDATING |
| R-008 | Speech | Names/technical terms are repeatedly misrecognized | High | High | My Vocabulary, contextual prompting where supported, correction learning with approval | OPEN |
| R-009 | Language | English normalization reverses negation or uncertainty | Critical | Medium | Preserve source, critical-meaning tests, evidence-linked review | OPEN |
| R-010 | Language | Dates/amounts/responsibilities are altered while transcript appears generally accurate | Critical | Medium | Critical Meaning Check; separate benchmark metrics | OPEN |
| R-011 | Licensing | Filipino Vosk model cannot support commercial product use under current license | High | High | Do not depend on it commercially without separate permission | MITIGATED |
| R-012 | Licensing | Taglish research dataset license is absent/unclear | High | Medium | Treat as research-only until explicit rights verified; build original benchmark corpus | OPEN |
| R-013 | Licensing | Dictionary/reference content is publicly readable but not redistributable | High | Medium | Use as reference only until reuse terms verified | OPEN |
| R-014 | Product | Competitors add stronger Taglish support | High | Medium | Build moat around evidence, adaptation, critical meaning, low-end performance, privacy | OPEN |
| R-015 | Product | Users refuse large model downloads | Medium | High | Optional models, plain-language size/performance choices, app useful without model | OPEN |
| R-016 | Product | "Almost immediate" text conflicts with accuracy expectations | High | High | Explicit Live Draft vs Final Pass semantics | MITIGATED |
| R-017 | Privacy | Sensitive audio/transcript leaks through logs/analytics | Critical | Medium | No raw content logging; minimal diagnostics; review crash-report fields | OPEN |
| R-018 | Privacy | User misunderstands recording consent obligations | High | Medium | Clear consent/legal UX; no covert recording | OPEN |
| R-019 | Privacy | Cloud provider retains uploaded audio longer than promised | Critical | Medium | Verify contracts/retention before launch; do not claim zero retention without evidence | OPEN |
| R-020 | Security | Service/provider secret is embedded in mobile app | Critical | Medium | Keep privileged keys server-side; threat-model review | OPEN |
| R-021 | Security | Transcript content prompt-injects downstream AI | High | Medium | Treat transcript as untrusted data; isolate system instructions; evidence-grounded assistant | OPEN |
| R-022 | Cloud | Duplicate Improve requests cause duplicate compute or charges | High | Medium | Idempotency keys, job uniqueness, bounded retries, entitlement ledger | OPEN |
| R-023 | Cloud | Cloud transcription becomes financially unsustainable | Critical | Medium | Per-user quotas/cost limits, cost telemetry, segment-level Improve, measured pricing | OPEN |
| R-024 | Cloud | Backend complexity is introduced before value is validated | High | High | Phase gate; no backend until Phase 10 | MITIGATED |
| R-025 | Data | DB row exists but audio file is missing, or reverse | High | Medium | Reconciliation paths and explicit repair/error state | OPEN |
| R-026 | Data | Auto-regeneration overwrites user corrections | Critical | Medium | User edit flags, proposed versions, merge/accept flow | OPEN |
| R-027 | Performance | Raw PCM is copied excessively through JS bridge | High | Medium | Keep high-frequency capture/inference native; expose throttled events | OPEN |
| R-028 | Tooling | Expo Go is mistaken for production-native validation | High | Medium | Development Build required for native/speech/real IAP testing | MITIGATED |
| R-029 | Tooling | Windows environment lacks required Android/EAS prerequisites | High | Unknown | Local Phase 0 preflight | VALIDATING |
| R-030 | Repository | Public repository unintentionally exposes commercially sensitive benchmark data or secrets | High | Medium | No benchmark audio/private data/secrets; license decision explicit | OPEN |

## Closure rule

A risk is not `CLOSED` because code exists. It closes only when the relevant evidence has been executed and recorded.
