# Model and Data License Register

Last updated: 2026-09-09

This file records licensing status separately from technical suitability.

A technically good model/dataset must not be integrated commercially if rights are unclear.

## Verified candidates

### OpenAI Whisper

- Purpose: upstream multilingual speech model family
- Code license: MIT
- Model weights: MIT
- Status: `VERIFIED` for license identity
- Technical production suitability: `RESEARCH_REQUIRED`

Official upstream repository states that both code and model weights are released under MIT.

### whisper.cpp

- Purpose: on-device C/C++ inference for Whisper-family models
- License: MIT
- Platforms documented upstream: iOS and Android among others
- Relevant capabilities documented upstream: quantization, VAD, CPU/GPU paths, mobile examples
- Status: `VERIFIED` for license/platform documentation
- Production suitability: `RESEARCH_REQUIRED` pending Phase 2 benchmark

### Mozilla Common Voice

- Purpose: possible evaluation/training speech data where relevant locale data exists
- License: Common Voice terms make dataset contributions available under CC0, subject to current Mozilla Data Collective distribution terms
- Status: `VERIFIED` for stated CC0 dataset license model
- Filipino/Taglish usefulness: `RESEARCH_REQUIRED`

Do not mirror/repackage datasets contrary to current distribution terms.

## Restricted / unsuitable commercial dependency

### Vosk Filipino model

Model:
`vosk-model-tl-ph-generic-0.6`

Current model listing:

- size: approximately 320 MB;
- language: Filipino/Tagalog;
- listed license: CC BY-NC-SA 4.0.

Status:
`ACCEPTED_LIMITATION`

Decision:
Do not use this model as the commercial product foundation unless separate commercial rights are obtained.

It may be evaluated for research only within license constraints.

## Unverified research resource

### FilSwitch or other Filipino-English code-switching datasets

Status:
`RESEARCH_REQUIRED`

Reason:
A dataset page may be publicly accessible without granting clear commercial training/redistribution rights.

Rule:
Do not train or ship a commercial model derived from any such dataset until:

- license is explicitly identified;
- redistribution rights are understood;
- commercial use is allowed;
- required attribution/notice is recorded.

## Language references

Potential authoritative references include materials from the Komisyon sa Wikang Filipino.

Use them as linguistic/orthographic references unless specific reuse rights allow embedding or redistribution.

Public access is not assumed to equal commercial redistribution permission.

## Original TransVoice benchmark corpus

Preferred strategy:

- founder-authored prompts;
- consented recordings;
- explicit contributor release/terms;
- no private real-world conversations;
- no third-party copyrighted scripts without permission.

Keep benchmark audio private if it creates privacy, licensing, or commercial-moat concerns.

## Required entry fields for future assets

Every model/dataset added later must record:

- exact name;
- source;
- version/hash;
- purpose;
- license;
- commercial-use status;
- redistribution status;
- attribution;
- data provenance;
- known restrictions;
- verification date;
- implementation phase.
