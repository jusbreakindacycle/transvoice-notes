# Architecture

Last updated: 2026-09-09

## Architecture objective

Use the smallest architecture that can preserve audio reliably, process English/Filipino/Taglish speech locally where feasible, and keep the product maintainable across iOS and Android.

The architecture must not become complex merely to look production-grade.

## High-level structure

```text
React Native / Expo / TypeScript
- screens
- navigation
- application state
- repositories
- SQLite access
- settings
- search
- vocabulary UI
- transcript review UI
- cloud client when introduced

           │
           ▼

Small native TransVoice boundary
- authoritative microphone capture where required
- incremental audio writing
- recording recovery metadata
- bounded PCM fan-out
- VAD integration
- whisper.cpp integration
- platform acceleration
- native interruption/audio-route handling

           │
           ▼

iOS / Android platform APIs
```

## One authoritative microphone path

There must not be separate microphone consumers for waveform, saved audio, and transcription.

```text
MICROPHONE
    ↓
AUTHORITATIVE CAPTURE
    ↓
PCM
    ├──> high-priority audio writer
    ├──> throttled waveform/metering
    └──> bounded speech queue
```

If speech processing falls behind, speech work is slowed, dropped from the live queue, or recovered from saved audio later. The audio writer must not wait for AI.

## App layer

Preferred:

- React Native;
- Expo;
- TypeScript;
- Expo Router;
- Expo Development Builds;
- EAS tooling where useful.

Expo Go is a UI/prototype environment, not the production validation environment for native speech/recording features.

## Native boundary

Native code is justified for functionality where JavaScript would create unacceptable reliability, latency, or memory risk.

Candidate implementation languages:

- Kotlin for Android-specific code;
- Swift for iOS-specific code;
- C/C++ for whisper.cpp or common native inference code.

Prefer Expo Modules API for local native-module integration where appropriate.

Do not create a broad "universal native engine" abstraction before concrete repeated needs exist.

## Speech architecture

Primary candidate:

`whisper.cpp` behind a replaceable `TranscriptionEngine` concept.

Required conceptual capabilities:

- load/unload model;
- Live Draft;
- final segment transcription;
- cancel;
- model capability metadata;
- timestamps;
- error category.

Do not expose whisper.cpp-specific types through the app domain layer.

## Two-pass transcription

```text
Audio segment
   ↓
Live Draft — fast/provisional
   ↓
Final Source Pass — higher accuracy
   ↓
Canonical English — meaning preserving
```

A weaker device may defer the final pass until recording stops.

## Storage architecture

### Files
App-private storage contains:

- recording audio;
- recovery metadata;
- local speech models;
- temporary exports;
- temporary model downloads.

Audio must not live only in cache.

### Database
SQLite is the local source for metadata and text.

Use FTS5 for full-text search if supported by the selected Expo SQLite configuration.

### Secrets
Use platform-backed secure storage for small secrets or encryption keys.

Do not put full audio/transcripts into SecureStore.

## Core data boundaries

Recommended entities are defined in `MASTER_PROMPT.md`.

Persist only structures with a clear current workflow.

Do not add a vector database or remote search service until SQLite FTS is demonstrably insufficient.

## iOS/Android parity

Product semantics should match, but native implementation details may differ.

Android concerns include:

- microphone foreground service;
- notification behavior;
- while-in-use microphone restrictions;
- manufacturer battery controls.

iOS concerns include:

- AVAudioSession;
- background audio capability;
- interruptions;
- route changes;
- native performance/Apple acceleration.

## Cloud boundary

No backend is required for the local MVP.

When Cloud Improve is introduced:

```text
App
 ↓
authentication/entitlement
 ↓
rate/quota/cost check
 ↓
temporary signed upload
 ↓
async improve job
 ↓
worker/provider
 ↓
validated proposed result
 ↓
user accept/reject
 ↓
temporary cloud audio cleanup
```

Provider credentials never belong in the mobile app.

## Reliability principles

- bounded queues;
- structured cancellation;
- idempotent recording stop/finalization;
- user edits never silently overwritten;
- local result survives cloud failure;
- no unbounded retries;
- database and filesystem divergence handled explicitly.

## Architecture decisions that remain research-gated

- exact recording file format after MVP;
- exact whisper.cpp model/quantization;
- whether local English normalization is model-based or deterministic/hybrid;
- whether SQLCipher is justified;
- speaker diarization approach;
- cloud provider and backend;
- cross-device sync design.

These are not to be guessed during implementation.
