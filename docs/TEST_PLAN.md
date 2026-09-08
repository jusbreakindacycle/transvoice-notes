# Test Plan

Last updated: 2026-09-09

## Testing principle

Test the highest-cost failures first.

For TransVoice Notes the highest-cost failure is data loss, followed by semantic meaning reversal.

A pretty UI with weak recording recovery is not acceptable.

## Test layers

### TypeScript unit tests

Planned coverage:

- search normalization;
- transcript mapping;
- summary scoring;
- action extraction;
- important-detail extraction;
- vocabulary mappings;
- state reducers;
- retry/idempotency helpers;
- canonical-English test fixtures where logic is deterministic.

### Database tests

- insert/read/update/delete;
- migrations;
- foreign-key behavior;
- transcript ordering;
- FTS;
- deletion cascade behavior;
- user-edit preservation;
- database/filesystem reconciliation metadata.

### Native recording tests

- recording-state transitions;
- duplicate start prevention;
- idempotent stop;
- PCM/writer behavior;
- header/finalization;
- recovery metadata;
- queue backpressure;
- low-storage behavior;
- cancellation.

### Native speech tests

- model load/unload;
- checksum failure;
- missing model;
- interrupted model download;
- Live Draft;
- final pass;
- timestamp ordering;
- cancellation;
- VAD interaction;
- model memory cleanup.

### End-to-end UI tests

- onboarding;
- permission denial;
- record;
- pause;
- resume;
- stop;
- background/lock;
- note detail;
- playback;
- source/English toggle;
- edit transcript;
- approve vocabulary;
- search;
- timestamp jump;
- export;
- delete.

## Physical-device matrix

### Android

At minimum test:

- low-end/older Android class where available;
- a representative mid-range Android;
- a higher-end Android if available.

Critical scenarios:

- 5-minute;
- 30-minute;
- 60-minute;
- screen on;
- screen locked;
- app foreground/background;
- battery saver;
- low storage;
- wired/Bluetooth route where available;
- interruption;
- noisy/quiet environment.

### iOS

Test:

- oldest practical supported iPhone available;
- a mid-generation iPhone;
- a recent iPhone where available.

Repeat the same language and recording scenarios.

## Language matrix

Separate metrics for:

- English;
- Filipino/Tagalog;
- light Taglish;
- heavy Taglish;
- technical Taglish;
- casual Taglish.

Do not collapse these into one multilingual score.

## Critical Meaning suite

Every benchmark must contain adversarial examples for:

- names;
- amounts;
- numbers;
- dates;
- times;
- negation;
- uncertainty;
- responsibilities;
- decisions;
- technical terms.

Example:

Source:
`Hindi pa confirmed kung Friday.`

Fail:
`It is confirmed for Friday.`

This must count as a severe semantic failure regardless of WER.

## Failure matrix

Explicitly test:

- microphone denied;
- microphone already in use;
- recording interruption;
- audio route change;
- backgrounding;
- screen lock;
- process interruption;
- low storage;
- DB write failure;
- audio file missing;
- DB row missing;
- model missing;
- corrupt model;
- model download interruption;
- Live Draft backlog;
- final transcription failure;
- canonical English failure;
- export failure;
- cloud timeout/429/5xx when cloud exists;
- duplicate Improve request when cloud exists.

## Verification statuses

For every claim distinguish:

- automated test;
- manual test;
- physical-device test;
- not performed.

Do not convert "expected to work" into "verified."
