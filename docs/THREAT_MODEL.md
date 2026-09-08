# Threat Model

Last updated: 2026-09-09

## Assets

High-value assets:

- raw audio recordings;
- source transcripts;
- English canonical transcripts;
- user vocabulary;
- manual notes;
- account/session credentials if added;
- subscription entitlements;
- temporary cloud audio if added;
- provider/service secrets.

## Trust boundaries

1. User ↔ mobile app
2. React Native/TypeScript ↔ native module
3. Mobile app ↔ local filesystem/database
4. Mobile app ↔ cloud control plane (future)
5. Cloud control plane ↔ transcription provider/worker (future)
6. Repository/CI ↔ deployment environments

## Threats

### Local device loss/theft
Risk: another person gains device access.

Controls:
- app-private storage;
- platform device protections;
- consider optional app lock later only if user demand justifies it;
- do not claim file-level encryption yet.

### Malicious/buggy native integration
Risk: audio is corrupted or copied unsafely.

Controls:
- small native boundary;
- bounded buffers;
- recording-first priority;
- native tests;
- physical-device QA.

### Path traversal/model archive abuse
Risk: downloaded model archive writes outside intended directory.

Controls:
- validate archive entries;
- canonical path checks;
- checksum;
- partial install state.

### Sensitive logging
Risk: transcripts/audio appear in logs/crash reports.

Controls:
- redaction policy;
- content-free diagnostics;
- review third-party crash tooling before adoption.

### Transcript prompt injection
Risk: recorded speech contains instructions designed to manipulate AI.

Controls:
- transcript always treated as untrusted evidence;
- separate system/user/evidence channels;
- retrieval-grounded answering;
- no tool execution based solely on transcript text.

### Unauthorized cloud upload
Risk: app uploads without explicit user intent.

Controls:
- cloud action requires explicit Improve Transcript flow;
- no silent fallback from local to cloud;
- clear scope before upload.

### Cross-user cloud data exposure
Risk: broken authorization reveals another user's audio/result.

Controls:
- row-level authorization;
- signed private object access;
- ownership tests;
- deny-by-default policies.

### Duplicate processing/billing
Risk: retries create duplicate expensive jobs.

Controls:
- idempotency keys;
- unique job constraints;
- job state machine;
- bounded retry.

### Provider compromise/retention
Risk: third-party processor exposes or retains data unexpectedly.

Controls:
- vendor review;
- narrow uploads;
- segment-level Improve;
- verified retention contract;
- processor list;
- user disclosure.

### Repository secret leak
Risk: public repo exposes credentials.

Controls:
- no secrets committed;
- CI secret store;
- secret scanning;
- rotate immediately after suspected exposure.

## Abuse cases

TransVoice must not become a covert surveillance tool.

Do not add:
- silent background recording;
- boot-triggered microphone capture;
- phone-call interception;
- hidden recording indicators.

## Residual risks requiring future review

- file-level encryption;
- biometric/app lock;
- E2E encrypted sync;
- cloud provider choice;
- diarization identity privacy;
- account recovery;
- billing fraud;
- server incident response.

These should be addressed only when the corresponding feature exists.
