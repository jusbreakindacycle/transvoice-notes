# Performance Plan and Evidence

Last updated: 2026-09-09

## Current status

No TransVoice product performance has been measured yet.

All numbers remain `NOT VERIFIED` until the app exists and measurements are recorded.

## Metrics to measure

### Recording

- tap-to-record-active latency;
- dropped/failed audio writes;
- recording storage per hour;
- memory during 5/30/60-minute sessions;
- battery usage;
- thermal behavior;
- background/lock stability.

### Live Draft

- time to first text;
- average lag behind speech;
- worst observed lag;
- queue depth;
- queue drops/defer events;
- CPU;
- RAM;
- thermal behavior.

### Final Pass

- real-time factor;
- catch-up time after stop;
- model load time;
- memory peak;
- battery/thermal cost.

### Search/database

- search latency at 100 notes;
- search latency with hours of transcript text;
- DB size;
- FTS indexing time;
- note-detail load latency.

### App/package

- Android app size;
- iOS app size;
- local model size;
- total storage with model + representative recordings.

## Performance hierarchy

If resources are constrained:

1. preserve audio;
2. preserve DB consistency;
3. slow/defer Live Draft;
4. defer final pass;
5. defer normalization/summary.

Never block the recording writer merely to keep the transcript "live."

## Target-device principle

Do not create hard-coded device stereotypes.

The app may build capability profiles from measured behavior.

A device can legitimately run:

- fast Live Draft + same-model final pass;
- lightweight Live Draft + stronger final pass;
- no Live Draft + post-recording final pass.

The user outcome matters more than identical internals.

## Phase 2 evidence table

To be filled with real results:

| Device | OS | Model | Quantization | Language | Live first-text | Final RTF | Peak RAM | Battery/thermal | Critical meaning | Status |
|---|---|---|---|---|---:|---:|---:|---|---|---|
| NOT TESTED | | | | | | | | | | |

## Rule

Never publish "works on low-end phones," "real-time," "high accuracy," or a battery claim until this document contains reproducible evidence.
