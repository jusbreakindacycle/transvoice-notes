# TRANSVOICE NOTES — MASTER PRODUCT, ENGINEERING, AI, PRIVACY, SCALING & CODEX IMPLEMENTATION CONSTITUTION

> Status: Founder-approved product constitution and implementation handoff
>
> Product: **TransVoice Notes**
>
> Tagline: **Record. Transcribe. Remember.**
>
> Product hook: **Speak the way Filipinos actually speak.**
>
> Primary development setup: **VS Code + Codex + Expo / React Native**
>
> Platforms: **iOS and Android**
>
> Repository: `jusbreakindacycle/transvoice-notes`

---

# 0. PURPOSE OF THIS FILE

This file is the highest-level product and engineering constitution for TransVoice Notes.

It exists to prevent:
- vibe coding;
- feature drift;
- architecture theater;
- false AI claims;
- premature cloud infrastructure;
- accidental privacy violations;
- unsafe recording architecture;
- product decisions being silently invented by an AI coding agent;
- building a technically impressive app that fails the real user problem.

Codex must treat the actual repository state as the implementation source of truth and this document as the product/architecture source of truth.

When this document conflicts with the actual repository:
1. inspect the real repository;
2. explain the conflict;
3. preserve existing user work unless the founder explicitly approves a replacement;
4. record the resolution in `docs/DECISIONS.md`.

When a new product decision is required and cannot be inferred safely:
- mark it `FOUNDER DECISION REQUIRED`;
- do not silently invent the decision;
- continue all non-blocked work where possible.

Never claim a feature, benchmark, command, build, test, device result, privacy property, encryption property, or compatibility result that has not actually been verified.

---

# 1. PRODUCT IDENTITY

## 1.1 What TransVoice Notes is

TransVoice Notes is a **local-first voice-memory application for iOS and Android** built around how Filipinos actually speak in everyday life:

- English;
- Filipino / Tagalog;
- Taglish;
- natural English-Filipino code-switching;
- mixed-language speech within the same recording.

Its core job is:

```text
SPEAK NATURALLY
      ↓
RECORD SAFELY
      ↓
CREATE A LIVE DRAFT
      ↓
PRESERVE THE ORIGINAL MEANING
      ↓
CREATE A CLEAR ENGLISH TRANSCRIPT
      ↓
FIND IMPORTANT DETAILS
      ↓
SEARCH / REMEMBER / ACT
```

The canonical user-facing transcript is **English by default**, while the original/source transcript remains locally available as evidence.

The user should not need to understand:
- speech models;
- model quantization;
- C++;
- native bridges;
- decoding;
- language identification;
- embeddings;
- retrieval;
- inference;
- AI providers;
- background services;
- database indexing.

The product must make difficult language and device decisions automatically.

## 1.2 What TransVoice Notes is not

It is not:
- a covert recorder;
- a call-recording application;
- an always-listening surveillance application;
- a meeting bot that silently joins calls;
- a general-purpose LLM chat application;
- a cloud-first transcription service;
- an Otter/Notta/Plaud clone;
- a 100-language platform at launch;
- an enterprise collaboration suite at launch;
- a fake “AI-powered” marketing demo;
- a reason to upload private audio unnecessarily.

---

# 2. PRIMARY PRODUCT THESIS

The product exists to win one use case first:

> **The best personal voice-memory experience for people who naturally speak English, Filipino, and Taglish and want reliable searchable English notes without being forced to upload their recordings to the cloud.**

The initial competitive objective is not:
- more languages;
- more integrations;
- more meeting bots;
- more AI templates.

The initial competitive objective is:

> **Given the same real Filipino/Taglish recording, TransVoice should preserve the intended meaning and important details more reliably than general-purpose competitors, especially on ordinary phones.**

The durable moat should come from the combination of:
- Taglish-first benchmarking;
- meaning preservation;
- user-approved personal vocabulary;
- critical-information verification;
- reliable recording;
- source-to-English evidence traceability;
- adaptive device performance;
- privacy-first local processing;
- optional surgical cloud improvement.

Taglish alone is not a durable moat.

---

# 3. HIGHEST-PRIORITY INVARIANT

The most important technical rule in the entire project is:

> **Never sacrifice a user's recording for transcription, translation, summarization, search, or AI.**

Priority order:

```text
1. AUDIO PRESERVATION
2. SAVE / RECOVER / PLAYBACK
3. SOURCE TRANSCRIPTION
4. ENGLISH CANONICAL TRANSCRIPT
5. IMPORTANT-DETAIL EXTRACTION
6. SEARCH
7. SUMMARY
8. ASSISTANT / GENERATIVE FEATURES
```

If transcription fails:
- keep the recording.

If translation fails:
- keep the recording and valid source transcript.

If the final pass fails:
- keep the live draft if it is valid and mark it clearly as incomplete.

If summarization fails:
- keep the recording and transcript.

If cloud improvement fails:
- preserve the local version.

If the assistant fails:
- the note remains useful.

No downstream failure may intentionally delete or corrupt the recording.

---

# 4. PLATFORM DECISION: IOS + ANDROID

TransVoice Notes is a cross-platform product.

The product behavior should be equivalent across iOS and Android, but the implementation does **not** need to be identical.

Feature parity means:
- same user outcome;
- same privacy promise;
- same product semantics;
- same data integrity.

Feature parity does not mean:
- same internal audio implementation;
- same performance profile;
- same model;
- same acceleration path;
- same background-service implementation.

Platform-native behavior must be respected.

---

# 5. DEVELOPMENT STACK

## 5.1 UI / application layer

Preferred application stack:
- React Native;
- Expo;
- TypeScript;
- Expo Router;
- React Native New Architecture;
- Expo Development Builds;
- EAS Build;
- EAS Submit;
- EAS Update where safe;
- EAS Workflows or equivalent CI/CD where justified.

Do not hard-code dependency versions in this constitution.

At implementation time:
1. verify the current stable Expo SDK;
2. verify current React Native compatibility;
3. verify current minimum iOS/Android versions;
4. pin exact working versions in the repository;
5. document them in `docs/TECH_STACK.md`.

## 5.2 Expo Go rule

Expo Go is allowed for:
- early visual prototyping;
- screen layout;
- navigation;
- mock data;
- UX flows;
- non-native TypeScript logic;
- basic SQLite experiments that are supported by Expo Go.

Expo Go is **not** the authoritative environment for:
- custom native modules;
- whisper.cpp;
- SQLCipher;
- real in-app purchases;
- production recording reliability;
- native background audio validation;
- final iOS/Android performance;
- production speech benchmarks.

As soon as the project needs custom native code, create and use an **Expo Development Build**.

Do not misrepresent Expo Go success as production-device success.

## 5.3 Windows development

VS Code on Windows is an accepted primary development environment.

Use EAS cloud builds to create iOS development/production builds when appropriate.

A Mac is not required merely to submit an EAS-built iOS app, but access to macOS/Xcode remains useful or necessary for:
- deep native iOS debugging;
- local iOS builds;
- Instruments profiling;
- low-level Swift/C++ investigation;
- certain platform-specific troubleshooting.

Do not block the entire project merely because the founder is developing primarily on Windows.

---

# 6. NATIVE BOUNDARY

TransVoice should use Expo/React Native for the majority of UI and application logic.

However, recording reliability and on-device speech inference are allowed to use native Swift/Kotlin/C/C++.

Use the Expo Modules API for local custom native modules where appropriate.

Do not pass high-frequency raw PCM continuously through JavaScript if it creates reliability, latency, or memory risk.

The native boundary should remain small and justified.

Preferred conceptual boundary:

```text
REACT NATIVE / TYPESCRIPT
- screens
- navigation
- UI state
- repositories
- SQLite queries
- search
- settings
- vocabulary UI
- product orchestration
- cloud client
- entitlement UI

          │

NATIVE TRANSVOICE CORE
- authoritative microphone capture where required
- append-safe audio writing
- recovery metadata
- bounded PCM fan-out
- VAD integration
- whisper.cpp integration
- native acceleration
- audio-route/interruption handling where required

          │

PLATFORM
Android / iOS
```

Avoid creating many native modules unless evidence requires them.

A single local native package may internally expose clearly separated recording and transcription interfaces.

---

# 7. AUTHORITATIVE MICROPHONE RULE

There must be one authoritative microphone capture path.

Never run two independent microphone consumers for:
- recording;
- waveform;
- live transcription.

Conceptually:

```text
MICROPHONE
    ↓
AUTHORITATIVE NATIVE CAPTURE
    ↓
PCM BUFFER
    ├────────────→ AUDIO WRITER
    │
    ├────────────→ LOW-RATE METERING / WAVEFORM
    │
    └────────────→ BOUNDED LIVE TRANSCRIPTION QUEUE
```

The audio writer has higher priority than transcription.

If the speech queue becomes overloaded:
- drop or defer speech work if necessary;
- never block the audio writer;
- run a final transcription pass from the saved recording later.

The saved recording is the evidence of record.

---

# 8. RECORDING ARCHITECTURE

## 8.1 Recording states

Use one authoritative state machine:

```text
Idle
 ↓
Preparing
 ↓
Recording
 ↕
Paused
 ↓
Stopping
 ↓
FinalizingAudio
 ↓
ProcessingTranscript
 ↓
Ready
```

Any active state may transition to:

```text
RecoverableError
FatalSessionError
```

The app must distinguish:
- audio error;
- transcription error;
- translation error;
- database error;
- cloud error.

Do not show one generic “Something went wrong” when the app knows the failure category.

## 8.2 Active audio format

The project must benchmark the most reliable approach.

Initial preferred direction:
- mono;
- speech-appropriate sample rate;
- 16-bit PCM during the authoritative capture path;
- append-safe writing;
- repairable/finalizable metadata.

WAV remains a valid MVP archival format because:
- it is simple;
- recoverability is straightforward;
- speech engines accept PCM well.

But WAV is storage-expensive.

Therefore:
- measure actual storage usage;
- do not promise “lightweight” without measurement;
- later evaluate safe post-finalization compression such as M4A/Opus only after the original recording is safely finalized;
- never delete the original until replacement integrity is verified.

Do not optimize storage before recording recovery is proven.

## 8.3 Recovery

During recording maintain enough metadata to recover after:
- activity recreation;
- app backgrounding;
- screen lock;
- process interruption;
- service reconnection;
- crash;
- media service reset;
- supported OS interruption.

Recovery must be idempotent.

Startup must detect abandoned recording sessions and safely:
- repair the recording when possible;
- mark incomplete recordings clearly;
- never silently overwrite another session;
- preserve raw recoverable data if repair is uncertain.

---

# 9. LIVE DRAFT → FINAL PASS

The user requires:
- transcript almost immediately;
- accuracy still matters.

Therefore TransVoice must not pretend one transcript state is sufficient.

Use a two-stage model:

```text
SPEECH
 ↓
LIVE DRAFT
 ↓
STABLE SEGMENT
 ↓
FINAL SOURCE PASS
 ↓
CANONICAL ENGLISH PASS
```

## 9.1 Live Draft

Live Draft is:
- fast;
- provisional;
- allowed to change;
- visibly labeled as a draft;
- preferably source-language / mixed-language rather than forced English when that improves fidelity.

Example:

```text
Live Draft:
"Kailangan natin i deploy yung super base..."
```

The UI must communicate that it may change.

## 9.2 Final Pass

A higher-accuracy pass processes stable segments or the saved recording.

It may:
- use a stronger model;
- use more context;
- use My Vocabulary;
- process segments after speech pauses;
- catch up after recording stops on weaker phones.

Example:

```text
Source:
"Kailangan natin i-deploy yung Supabase migration..."

English:
"We need to deploy the Supabase migration..."
```

The user should be able to play the relevant audio timestamp.

---

# 10. TRANSCRIPTION MODES

User-facing modes:

```text
Auto — Recommended
Fast
Better Accuracy
```

## 10.1 Auto

Auto is the default.

Auto may consider:
- available memory;
- CPU class;
- platform;
- thermal state where accessible;
- battery state where appropriate;
- model installed;
- recording length;
- speech backlog;
- whether recording is active;
- recent measured device performance.

Auto may choose:
- lightweight live model + stronger final model;
- same model for both;
- post-recording finalization;
- reduced UI update frequency.

Never silently degrade to cloud.

Cloud processing requires explicit user action.

## 10.2 Fast

Fast prioritizes:
- low latency;
- lower heat;
- lower battery;
- smaller model.

The UI must not imply that Fast is equally accurate.

## 10.3 Better Accuracy

Better Accuracy may:
- use a larger local model;
- process more slowly;
- consume more storage/RAM/battery.

The app should explain the tradeoff in plain language.

---

# 11. SPEECH ENGINE STRATEGY

## 11.1 Primary candidate

`whisper.cpp` is the primary multilingual candidate because it:
- supports iOS;
- supports Android;
- supports local inference;
- supports quantization;
- supports multilingual speech;
- supports translation to English;
- provides native examples;
- has a commercially permissive core license.

However:
- do not assume a model will perform acceptably on target hardware;
- do not hard-code a model before benchmarking;
- do not claim Taglish production support until measured.

## 11.2 Vosk

Vosk may be used as:
- an English baseline;
- a benchmark;
- an experiment.

Do not make the commercial Taglish product depend on a Filipino model with non-commercial licensing unless separate commercial permission is verified.

## 11.3 Transcription abstraction

Maintain a replaceable interface conceptually similar to:

```text
TranscriptionEngine
- loadModel()
- unloadModel()
- transcribeSegment()
- streamDraft()
- cancel()
- capabilities()
```

Do not let the rest of the product depend directly on whisper.cpp-specific classes.

---

# 12. LANGUAGE CONTRACT

TransVoice is:

> **Multilingual / mixed-language input, English canonical output.**

Supported product direction:
- English;
- Filipino / Tagalog;
- Taglish;
- natural mixed speech.

Do not force a recording into exactly one language.

User-facing default:

```text
Language
● Auto — English, Filipino & mixed speech
○ English
○ Filipino
```

Manual selection may be useful for difficult recordings.

---

# 13. SOURCE TRANSCRIPT + CANONICAL ENGLISH

The source transcript is now a first-class evidence layer.

Conceptual pipeline:

```text
AUDIO
 ↓
SOURCE / MIXED-LANGUAGE TRANSCRIPT
 ↓
CANONICAL ENGLISH
 ↓
SUMMARY / SEARCH / ACTIONS / ASSISTANT
```

## 13.1 Source transcript

The source transcript:
- preserves what the recognizer believes was said;
- may contain English, Filipino, and Taglish;
- remains locally stored by default;
- can be user-edited;
- remains timestamp-linked to audio.

## 13.2 Canonical English transcript

The canonical English transcript:
- is the primary reading/search/understanding view;
- preserves factual meaning;
- preserves names;
- preserves quantities;
- preserves dates and times;
- preserves technical terms;
- preserves chronology;
- preserves responsibility;
- preserves uncertainty;
- preserves negation;
- preserves conditional statements;
- does not add psychological interpretation;
- does not invent facts.

Example:

Source:
`Hindi pa final yung Friday.`

Correct:
`Friday is not yet final.`

Wrong:
`Friday is the final deadline.`

## 13.3 User-edited authority

User edits must never be silently overwritten.

A user-approved correction becomes authoritative for:
- search;
- summaries;
- important-detail extraction;
- assistant retrieval;
- future processing.

Automatic regeneration must create a proposed version or merge safely rather than destroying a user correction.

---

# 14. PERSONAL VOCABULARY

Feature name:

> **My Vocabulary**

This is a core differentiator.

It may store:
- people names;
- company names;
- product names;
- locations;
- Filipino terms;
- technical terms;
- project jargon;
- accepted spellings.

Example:

```text
Preferred: Supabase
Possible misrecognition: super base
Category: Technology
```

## 14.1 Learning rule

Never silently learn sensitive vocabulary from recordings.

The app may detect a user correction:

```text
"super base" → "Supabase"
```

Then ask:

> Remember “Supabase” for future recordings?

Only save after user approval.

## 14.2 Storage

My Vocabulary remains local by default.

Optional account users may later enable encrypted vocabulary sync.

## 14.3 Decoder context

Where supported, use relevant vocabulary as contextual decoding hints.

Do not assume contextual prompting guarantees recognition.

Measure the effect.

---

# 15. LANGUAGE REFERENCES AND DATASETS

Do not build a handmade Filipino grammar engine.

Language resources serve different purposes:

## Base model knowledge
Used for:
- speech recognition;
- multilingual understanding;
- speech translation.

## Authoritative Filipino references
Potentially include:
- Komisyon sa Wikang Filipino references;
- official orthography/grammar references.

Use them for:
- evaluation;
- normalization rules;
- terminology validation.

Do not scrape, redistribute, embed, or commercially reuse dictionary content unless reuse rights are verified.

## Research datasets
Potentially include:
- Filipino-English code-switching datasets;
- Common Voice;
- other properly licensed speech corpora.

For every dataset/model:
- document license;
- source;
- permitted commercial use;
- redistribution rights;
- attribution;
- restrictions.

Create:

`docs/MODEL_AND_DATA_LICENSES.md`

## TransVoice benchmark corpus

Build an original evaluation corpus using founder-authored sentences and consenting speakers.

It must include:
- English;
- Filipino;
- light Taglish;
- heavy Taglish;
- technical Taglish;
- casual Taglish;
- numbers;
- money;
- dates;
- deadlines;
- negation;
- uncertainty;
- names;
- locations;
- noisy speech;
- quiet speech;
- fast speech;
- slow speech.

Do not put private recordings or unlicensed benchmark audio in the public repository.

---

# 16. CRITICAL MEANING CHECK

Word Error Rate alone is insufficient.

TransVoice must explicitly evaluate important semantic fields:

- names;
- currency;
- quantities;
- dates;
- times;
- deadlines;
- negation;
- uncertainty;
- responsibility;
- decisions;
- commitments;
- technical terms.

Example:

```text
₱15,000 ≠ ₱50,000
Friday ≠ Thursday
not approved ≠ approved
maybe Friday ≠ Friday
Mark could do it ≠ Mark will do it
```

The app must not silently “correct” uncertain information without evidence.

Preferred UX:

```text
Important details detected

✓ Marco
✓ Friday
⚠ ₱15,000 — Review
⚠ Deadline not confirmed

[Review 2]
```

Tapping an item should play or seek to the relevant source audio.

---

# 17. IMPORTANT DETAIL EXTRACTION

Initial local extraction should be conservative and explainable.

Potential categories:
- people;
- amounts;
- dates;
- times;
- deadlines;
- tasks;
- assignments;
- decisions;
- uncertainty;
- negation.

Store evidence timestamp.

Never infer a confirmed deadline from:
- maybe;
- perhaps;
- not final;
- could;
- might.

Never infer ownership from:
- probably;
- maybe;
- could handle.

---

# 18. SEARCH

Search must work locally without AI.

Search:
- note title;
- canonical English transcript;
- source transcript where useful;
- manual note;
- action items;
- vocabulary-aware text.

Use SQLite FTS5 where supported.

Requirements:
- debounce;
- snippets;
- highlighting;
- timestamp navigation;
- indexes;
- bounded queries;
- lazy rendering.

Do not add vector search in the MVP without demonstrated user need.

A future semantic search layer may be evaluated separately.

---

# 19. LOCAL SUMMARY

The free/offline app must remain useful without a generative cloud model.

Initial summary may use:
- extractive summarization;
- sentence scoring;
- TextRank-style methods;
- deterministic keyword extraction;
- rule-based action/date extraction.

The app should clearly state when:
- transcript is too short;
- transcript quality is low;
- no clear action item exists.

Do not invent a polished generative narrative that exceeds evidence.

---

# 20. GROUNDED ASSISTANT

The assistant should answer from transcript evidence.

Conceptual flow:

```text
QUESTION
 ↓
LOCAL SEARCH / RETRIEVAL
 ↓
RELEVANT SEGMENTS
 ↓
EVIDENCE
 ↓
ANSWER
 ↓
TIMESTAMP REFERENCES
```

When evidence is missing:

> `I could not find that in this recording.`

The assistant must not fabricate:
- names;
- dates;
- deadlines;
- responsibilities;
- decisions;
- quotes.

The first version does not need unlimited LLM reasoning.

---

# 21. CLOUD "IMPROVE TRANSCRIPT"

Cloud processing is optional.

It must never happen automatically.

The explicit action is:

> **Improve Transcript**

Possible scopes:

```text
Improve this section
Improve entire transcript
```

Prefer the smallest necessary upload.

Example:

```text
60-minute recording
      ↓
user selects 15-second problem segment
      ↓
only that segment is uploaded
      ↓
higher-accuracy cloud processing
      ↓
proposed improvement
      ↓
user accepts or rejects
```

## 21.1 Privacy contract

Before upload clearly explain:
- what will be uploaded;
- why;
- which service/provider category will process it;
- expected retention behavior where verified;
- whether the local recording remains;
- that local processing remains the default.

Do not claim zero retention unless contract/provider behavior is verified.

## 21.2 Cloud improvement should use evidence

Cloud requests may include:
- selected audio;
- current source draft;
- relevant My Vocabulary terms;
- language hint;
- timestamp boundaries.

Never send unrelated recordings.

## 21.3 Cloud result

Return a proposed result.

Never silently overwrite:
- user edits;
- local transcript;
- important details.

Keep the local version until replacement is accepted.

---

# 22. ACCOUNT STRATEGY

Free local use requires no account.

Do not show mandatory registration during onboarding.

Account creation becomes justified only for capabilities that require identity, such as:
- cross-device sync;
- cloud credits;
- subscription entitlements;
- encrypted backup;
- shared vocabulary sync.

The account is not the product.

---

# 23. MONETIZATION STRATEGY

Do not monetize by crippling recording.

Preferred structure:

## Free
No account required.

Includes:
- recording;
- playback;
- local note library;
- local search;
- basic offline transcription when a model is installed;
- source transcript;
- canonical English where local capability supports it;
- basic important-detail extraction;
- export;
- My Vocabulary.

No artificial local “minutes remaining” counter.

## Pro — likely non-consumable / one-time unlock
Potential local-only advanced features:
- stronger local model choices;
- advanced organization;
- batch processing;
- advanced exports;
- advanced local summaries;
- advanced important-detail review;
- advanced vocabulary tools.

Do not require a recurring subscription merely to keep using downloaded local functionality unless there is genuine ongoing value.

## Plus / Cloud — subscription
Account required.

Potential ongoing-value services:
- cloud Improve Transcript;
- encrypted cloud backup;
- cross-device sync;
- cloud processing for phones too weak for strong local models;
- higher-cost speaker diarization;
- future cloud intelligence.

The exact price is a founder decision and must be based on:
- cloud cost per processed minute;
- store fees;
- taxes;
- expected usage;
- competitor pricing;
- sustainable margin.

Do not hard-code pricing before cost modeling.

Use platform-compliant in-app purchase mechanisms.

A cross-platform entitlement service such as RevenueCat may be evaluated later, but is not required before monetization work begins.

---

# 24. LOCAL DATA STORAGE

Core data is local-first.

Use:
- application-private files;
- SQLite;
- Expo FileSystem or native equivalent where appropriate;
- SecureStore for small secrets/keys.

Potential SQLite features:
- FTS5;
- SQLCipher where verified and justified.

Do not claim app-level encryption at rest merely because files are app-private.

If SQLCipher is used:
- generate a strong random database key;
- store only the key in platform secure storage;
- test restore/migration behavior;
- do not hard-code it;
- do not put it in logs.

Audio-file encryption is a separate design decision.

Do not claim encrypted audio until explicitly implemented and verified.

---

# 25. LOCAL DATA MODEL

Keep the schema minimal but sufficient.

Recommended entities:

## Recording
- id
- createdAt
- updatedAt
- title
- durationMs
- audioRelativePath
- audioFormat
- sampleRate
- channels
- bitDepth
- fileSizeBytes
- recordingState
- transcriptionState
- canonicalState
- isFavorite
- manualNote
- errorCategory
- errorMessageSafe

## TranscriptSegment
- id
- recordingId
- sequence
- startMs
- endMs
- sourceText
- canonicalEnglishText
- sourceUserEdited
- canonicalUserEdited
- sourceConfidence if real
- processingVersion
- status

## VocabularyEntry
- id
- preferredText
- aliases
- category
- createdBy
- approvedByUser
- usageCount
- createdAt
- updatedAt

## ImportantDetail
- id
- recordingId
- segmentId
- type
- value
- normalizedValue optional
- certainty
- evidenceStartMs
- evidenceEndMs
- reviewState

## ActionItem
- id
- recordingId
- text
- assignee optional
- dueDate optional
- certainty
- evidence timestamp

## ModelAsset
- modelId
- engine
- language capability
- quantization
- localPath
- size
- checksum
- license
- installedState
- verificationTime

## ProcessingJob
Used locally and optionally for cloud jobs:
- id
- recordingId
- type
- status
- attempt
- errorCategory
- createdAt
- startedAt
- completedAt

Do not create tables “for the future” without a current reader/writer/workflow.

---

# 26. MODEL MANAGER

Users must be able to record without any model installed.

Model manager supports:
- model metadata;
- description in plain language;
- download size;
- required storage;
- download progress;
- checksum;
- cancel;
- retry;
- partial-file cleanup;
- installed status;
- version;
- license;
- attribution;
- delete.

Partial downloads must never appear as installed.

Use `.partial` or equivalent temporary naming.

Validate archives safely.

Prevent path traversal.

Do not bundle a model until:
- license is verified;
- size is measured;
- target-device behavior is benchmarked.

---

# 27. DEVICE CAPABILITY PROFILE

Do not assume all phones are equal.

TransVoice may maintain measured device capability data locally.

Possible result:

```text
Live draft: Supported
Recommended mode: Auto
Final pass: Local
Better Accuracy model: Available
```

or:

```text
Live draft: Lightweight
Final pass: After recording
Better Accuracy model: Not recommended while recording
```

Do not hard-code:
- “iPhone fast”;
- “Android slow”;
- “this model always works.”

Base capability decisions on benchmark evidence.

---

# 28. PERFORMANCE PRINCIPLES

Optimize for ordinary phones.

Required:
- bounded PCM buffers;
- no unbounded queues;
- no entire long-audio file loaded into JS memory;
- no per-buffer React rerender;
- throttled waveform UI;
- off-main-thread native inference;
- lazy lists;
- indexed DB queries;
- predictable cancellation;
- VAD where beneficial;
- model unload strategy;
- memory pressure handling.

Recording must win resource contention.

---

# 29. PERFORMANCE METRICS

Do not invent numbers.

Measure:
- tap-to-record-active latency;
- time to first Live Draft text;
- live draft lag;
- final segment lag;
- final catch-up time after stop;
- source transcript accuracy;
- canonical English accuracy;
- critical-detail accuracy;
- RAM;
- CPU;
- battery;
- thermal behavior;
- model load time;
- APK/IPA size;
- model size;
- recording storage/hour;
- 5/30/60-minute stability;
- search latency;
- DB size;
- crash/ANR behavior.

Record actual results in:

`docs/PERFORMANCE.md`

---

# 30. TAGLISH FEASIBILITY GATE

Before claiming Taglish support, create an explicit benchmark.

Compare candidate local configurations such as:
- tiny multilingual;
- base multilingual;
- small multilingual;
- relevant quantized variants.

Do not assume the biggest model wins in product terms.

Evaluate:
- accuracy;
- critical meaning;
- speed;
- memory;
- battery;
- heat;
- storage;
- platform compatibility.

Test separately:
- English;
- Filipino;
- light Taglish;
- heavy Taglish;
- technical Taglish.

The test must include natural code-switching.

---

# 31. COMPETITIVE BENCHMARK GATE

Before claiming “better than” competitors, test the same recordings manually against relevant competitors available at that time.

Initial comparison set should consider:
- Google Recorder / Pixel Recorder where supported;
- Samsung Voice Recorder / Transcript Assist where supported;
- Otter;
- Notta;
- Plaud;
- relevant offline Whisper competitors.

Record:
- competitor version/date;
- device;
- settings;
- language setting;
- subscription level if relevant.

Measure:
- source transcription quality;
- Taglish handling;
- names;
- numbers;
- dates;
- negation;
- uncertainty;
- technical vocabulary;
- speaker behavior;
- time to result;
- privacy/cloud requirements.

Do not cherry-pick only successful TransVoice samples.

Do not publish competitor claims without reproducible evidence.

---

# 32. RECORDING LEGAL / CONSENT UX

TransVoice must never:
- record secretly;
- start from boot;
- auto-record meetings;
- hide microphone state;
- record phone calls;
- bypass OS privacy indicators.

The recording screen must clearly indicate active recording.

The app should provide plain-language consent guidance.

For Philippine users, the product must not imply that being a participant automatically makes every private recording lawful.

The user remains responsible for:
- consent;
- workplace policy;
- school policy;
- venue rules;
- local law.

Do not give the app a fake “legal compliance guarantee.”

---

# 33. PRIVACY

Default MVP:
- no account;
- no ads;
- no behavioral tracking;
- no transcript upload;
- no audio upload;
- no required cloud AI;
- local app-private storage;
- explicit user export.

If diagnostics are introduced:
- privacy-preserving;
- minimal;
- no raw transcript/audio;
- preferably opt-in;
- document every field.

Never log:
- full transcripts;
- audio;
- vocabulary contents;
- sensitive manual notes;
- cloud credentials;
- API tokens.

---

# 34. CLOUD BACKEND — ONLY WHEN CLOUD FEATURES BEGIN

Do not create backend infrastructure for the local MVP.

When cloud Improve / sync is intentionally introduced, prefer a managed architecture first.

A reasonable initial control plane may use:
- Supabase Auth;
- Postgres;
- Row Level Security;
- Storage;
- server-side functions;
- managed backups.

But Supabase is not a binding product identity.

Keep cloud interfaces replaceable.

Do not run expensive speech inference directly inside a function runtime that is unsuitable for long CPU workloads.

Use provider APIs or dedicated workers for heavy inference.

---

# 35. CLOUD JOB ARCHITECTURE

For cloud Improve:

```text
APP
 ↓
AUTH / ENTITLEMENT CHECK
 ↓
CREATE IMPROVE JOB
 ↓
RATE LIMIT / QUOTA / COST CHECK
 ↓
SIGNED TEMP UPLOAD
 ↓
JOB QUEUE
 ↓
TRANSCRIPTION WORKER / PROVIDER
 ↓
RESULT VALIDATION
 ↓
RESULT READY
 ↓
CLIENT FETCH
 ↓
USER ACCEPT / REJECT
 ↓
TEMP AUDIO DELETION
```

For short segment improvements a synchronous provider call may be acceptable if measured.

For long recordings use asynchronous jobs.

Cloud audio should not live forever by default.

Implement lifecycle deletion after successful processing according to a documented retention policy.

---

# 36. BACKEND RELIABILITY — WHAT ACTUALLY MATTERS EARLY

The viral “million-user backend list” must not become an MVP checklist.

When the cloud backend exists, the following are high-priority early:

- rate limiting;
- quotas;
- request size limits;
- authentication;
- authorization / RLS;
- TLS;
- secrets management;
- input validation;
- database migrations;
- indexes;
- timeouts;
- bounded retries;
- exponential backoff with jitter;
- idempotency;
- cost limits;
- provider error mapping;
- redacted structured logging;
- metrics;
- alerting on cloud failures;
- backups;
- restore testing;
- dependency/security scanning;
- CI/CD;
- rollback;
- health checks;
- API versioning where required.

Do not retry unsafe non-idempotent operations blindly.

---

# 37. BACKEND SCALE LADDER

## Stage A — Local-first product
Backend:
- none required.

Do not add:
- Kubernetes;
- Redis;
- message brokers;
- API gateways;
- multi-region;
- sharding.

## Stage B — First cloud users
Use:
- managed auth;
- managed Postgres;
- managed object storage;
- one API/control-plane layer;
- simple async jobs if needed;
- rate limits;
- quotas;
- monitoring;
- backups.

## Stage C — Growing cloud workload
Only when metrics justify:
- dedicated worker queue;
- dead-letter queue;
- connection pooling;
- circuit breaker for external provider;
- cached model/config manifests;
- autoscaling workers;
- more robust job observability.

## Stage D — Large scale
Consider only after demonstrated bottlenecks:
- read replicas;
- regional workers;
- partitioning;
- dedicated API gateway;
- sophisticated caching;
- multi-provider failover.

## Stage E — Very large / global system
Only with real need:
- sharding;
- multi-region active-active;
- distributed coordination;
- sophisticated service discovery;
- distributed transaction patterns;
- Kubernetes or equivalent orchestration.

Never add these because a social-media checklist says “real engineers know them.”

Architecture must follow measured load.

---

# 38. CLOUD COST CONTROL

Cloud transcription can bankrupt an otherwise successful freemium app.

Before allowing a cloud job:
- estimate or bound processing cost;
- verify user entitlement/credit;
- enforce maximum audio length;
- prevent duplicate jobs;
- use idempotency keys;
- limit concurrent jobs;
- monitor cost/user/day;
- alert on abnormal spend.

If a request is canceled before provider work begins:
- cancel safely;
- clean temporary data.

Do not build unlimited cloud transcription without a sustainable budget.

---

# 39. API DESIGN

Cloud APIs should be narrow.

Example versioned resources:
- `/v1/improve-jobs`
- `/v1/sync`
- `/v1/entitlements`

Every mutation should define:
- authentication;
- authorization;
- idempotency;
- validation;
- timeout;
- retry semantics;
- error codes;
- deletion/retention behavior.

Do not expose provider API keys to the app.

---

# 40. SYNC — FUTURE, OPTIONAL

Cloud sync is not MVP.

If implemented:
- account required;
- opt-in;
- conflict-safe;
- user edits must not be silently overwritten;
- deletion must propagate predictably;
- offline changes must reconcile.

Prefer metadata-first sync before full audio sync.

End-to-end encrypted sync is desirable but must not be claimed until actually implemented and externally reviewed where appropriate.

---

# 41. SECURITY

Required:
- minimal permissions;
- safe file paths;
- safe archive extraction;
- dependency review;
- no secrets in repository;
- no service-role keys in mobile code;
- input validation;
- server authorization;
- RLS where applicable;
- secure tokens;
- signed URLs for private uploads;
- short-lived credentials where possible;
- delete temporary cloud audio;
- log redaction.

Threat model must include:
- stolen phone;
- malicious app user;
- leaked token;
- cloud bucket exposure;
- replay/duplicate billing request;
- malicious filename/archive;
- prompt injection inside transcript text;
- transcript content attempting to manipulate assistant behavior.

Transcript text is untrusted user data, not system instructions.

---

# 42. PRIVACY / COMPLIANCE WORK

Before public cloud launch create:
- privacy policy;
- data map;
- retention policy;
- deletion policy;
- breach-response procedure;
- Privacy Impact Assessment;
- processor/vendor list;
- cloud data-flow diagram.

For Philippine operation, review applicability of:
- Data Privacy Act;
- National Privacy Commission guidance;
- registration obligations where applicable;
- breach notification requirements;
- contracts with processors.

Do not wait for a breach to design deletion and incident response.

---

# 43. APP STORE PRIVACY

Before store submission verify current:
- Apple privacy declarations;
- privacy manifest requirements;
- microphone purpose strings;
- background audio modes;
- Google Play Data Safety requirements;
- microphone/foreground-service declarations;
- subscription disclosures;
- account deletion rules if accounts exist.

Store-policy requirements change.

Codex must verify current official policy at release time.

---

# 44. IN-APP PURCHASES

Do not implement real billing in Expo Go.

Use development builds for actual store purchase testing.

Before implementation verify current:
- Apple StoreKit / App Store rules;
- Google Play Billing rules;
- regional alternative-payment rules;
- restore-purchase behavior;
- subscription cancellation requirements;
- cross-platform entitlement rules.

A subscription must deliver genuine ongoing value.

---

# 45. UX PRINCIPLES

Design for ordinary users.

Use:
- calm interface;
- strong contrast;
- large touch targets;
- readable type;
- screen reader labels;
- dynamic text;
- clear states;
- minimal animation;
- no GPU-heavy decorative effects;
- no “AI jargon.”

Primary navigation:

```text
Home
Search
Settings
```

Prominent Record action.

---

# 46. CORE SCREENS

## Onboarding
Explain:
- local-first behavior;
- no account required;
- microphone permission;
- optional transcription model;
- consent responsibility.

## Home / Library
Show:
- title;
- date;
- duration;
- transcription state;
- favorite;
- important-detail warning if unresolved.

## Recording
Show:
- timer;
- active state;
- lightweight amplitude;
- Live Draft;
- transcript mode;
- pause;
- resume;
- stop;
- model/transcription status.

## Note Detail
Show:
- title;
- audio player;
- English transcript;
- collapsible Original transcript;
- timestamp interaction;
- Important Details;
- Summary;
- Actions;
- Improve Transcript;
- manual note;
- favorite;
- export;
- delete.

## Search
Search titles and transcript text.

## My Vocabulary
Manage user-approved vocabulary.

## Model Manager
Manage local models.

## Settings
- theme;
- transcription mode;
- model storage;
- privacy;
- background recording explanation;
- diagnostics;
- about;
- open-source notices.

---

# 47. PLAYBACK

Playback must work even if:
- no model installed;
- transcription failed;
- English normalization failed;
- summary failed;
- cloud failed.

Support:
- play/pause;
- seek;
- skip backward/forward;
- timestamp seek;
- playback lifecycle cleanup.

Do not couple player lifecycle to transcript availability.

---

# 48. EXPORT

Support:
- original audio;
- TXT;
- Markdown;
- share sheet.

Export should be user-initiated.

Potential Markdown structure:

```text
Title
Date
Duration

English Transcript

Original Transcript

Important Details

Action Items

Summary
```

Do not export hidden/private metadata unnecessarily.

---

# 49. DELETION
User deletion must be explicit and understandable.

Local delete:
- remove DB rows;
- remove local recording;
- remove derived local artifacts.

If cloud data exists:
- clearly distinguish local-only delete vs delete everywhere;
- provide delete-everywhere where appropriate;
- verify cloud deletion completion.

Undo may be offered locally if implemented safely.

---

# 50. ACCESSIBILITY

Required:
- adequate touch targets;
- dynamic text;
- screen-reader content descriptions;
- state not communicated by color alone;
- accessible recording controls;
- accessible transcript timestamps;
- reduced-motion behavior where appropriate.

---

# 51. OBSERVABILITY WITHOUT SURVEILLANCE

For local-first MVP:
- local diagnostic log;
- error categories;
- performance counters;
- no transcript/audio content.

Optional “Send Diagnostics” may include:
- device model;
- OS;
- app version;
- model version;
- error category;
- timing;
- memory metrics if available.

User should be able to review what is being sent where practical.

Do not add advertising analytics.

---

# 52. CI/CD

Use managed CI/CD pragmatically.

Minimum pipeline before public release:
- install dependencies from lockfile;
- TypeScript typecheck;
- lint;
- unit tests;
- schema/migration tests;
- native compile checks;
- Android development/preview build;
- iOS development/preview build when credentials permit.

Production release should be deliberate, not “every push to main.”

Use:
- preview builds;
- release tags/branches;
- staged OTA rollout;
- rollback capability.

Native-runtime changes require compatible binary/runtime version handling.

---

# 53. OTA UPDATE SAFETY

Use EAS Update only for changes compatible with the installed native runtime.

Use a safe runtime-version strategy.

Before production:
- enable update code signing if adopted;
- document key rotation;
- stage rollout;
- monitor;
- retain rollback path.

Do not ship a JS update that assumes native APIs absent in the installed binary.

---

# 54. TESTING STRATEGY

## TypeScript unit tests
- search normalization;
- summary logic;
- action extraction;
- important-detail rules;
- vocabulary mappings;
- data mapping;
- state reducers;
- cloud retry rules;
- idempotency helpers.

## Database tests
- migrations;
- CRUD;
- FTS;
- foreign keys;
- deletion;
- transcript ordering;
- user-edit preservation.

## Native tests
- state transitions;
- PCM buffer handling;
- WAV/header finalization;
- recovery;
- queue backpressure;
- duplicate start prevention;
- idempotent stop;
- model checksum validation;
- cancellation.

## E2E
- onboarding;
- permission denial;
- recording;
- pause/resume;
- stop;
- background/lock;
- playback;
- transcript display;
- source toggle;
- edit;
- vocabulary acceptance;
- search;
- export;
- delete.

## Physical-device tests
Mandatory for serious recording/speech claims.

---

# 55. FAILURE MATRIX

Explicitly test:

- microphone denied;
- notification denied;
- microphone busy;
- audio route change;
- incoming interruption;
- app background;
- screen lock;
- OS kills/restarts components;
- media service reset;
- low storage;
- database write failure;
- file exists/DB row missing;
- DB row exists/file missing;
- recording finalize failure;
- speech model missing;
- speech model corrupt;
- model download interrupted;
- model checksum mismatch;
- live transcription backlog;
- final transcription failure;
- canonical English failure;
- cloud timeout;
- cloud provider 429;
- cloud provider 5xx;
- network loss during upload;
- duplicate Improve request;
- canceled Improve request;
- export failure.

Every failure must have intentional behavior.

---

# 56. DATA INTEGRITY

Explicitly handle:

```text
AUDIO EXISTS / DB ROW MISSING
DB ROW EXISTS / AUDIO MISSING
SOURCE EXISTS / CANONICAL MISSING
USER EDIT EXISTS / AUTO REGEN REQUESTED
CLOUD RESULT EXISTS / USER REJECTED
```

Do not assume impossible states.

Create repair/reconciliation routines only where necessary and test them.

---

# 57. PUBLIC REPOSITORY / IP RULE

The repository is currently public.

Do not automatically add MIT, Apache, GPL, or another open-source license.

A license is a founder-level business decision.

Until chosen:
- do not claim the project is open source;
- do not commit proprietary benchmark recordings;
- do not commit private user data;
- do not commit secrets;
- do not commit paid provider credentials;
- keep future proprietary cloud/service assets separate if commercially justified.

The public repository may still demonstrate:
- client architecture;
- tests;
- privacy design;
- benchmark methodology;
- engineering quality.

---

# 58. GITHUB METADATA

Recommended repository description while capabilities remain unverified:

> **Building a local-first iOS & Android voice-memory app for natural English, Filipino & Taglish speech. Privacy-first. 🚧 Early development.**

Recommended topics:
- `react-native`
- `expo`
- `typescript`
- `ios`
- `android`
- `voice-notes`
- `speech-to-text`
- `whisper-cpp`
- `taglish`
- `filipino`
- `offline-first`
- `privacy`
- `personal-knowledge-management`

Do not change the description to a production claim until capabilities are verified.

---

# 59. DOCUMENTATION STRUCTURE

Maintain:

```text
README.md
MASTER_PROMPT.md
AGENTS.md
CODEX.md

docs/
  PRODUCT_SPEC.md
  ARCHITECTURE.md
  PHASES.md
  PROJECT_STATE.md
  DECISIONS.md
  RISK_REGISTER.md
  TEST_PLAN.md
  PERFORMANCE.md
  PRIVACY.md
  SECURITY.md
  THREAT_MODEL.md
  MODEL_AND_DATA_LICENSES.md
  COMPETITIVE_BENCHMARK.md
  CLOUD_ARCHITECTURE.md
  RELEASE_CHECKLIST.md
  TECH_STACK.md
```

Create additional docs only when they solve a real documentation problem.

---

# 60. EVIDENCE STATUS

Use:

```text
VERIFIED
IMPLEMENTED_UNVERIFIED
DOCUMENTED_ONLY
PLANNED
RESEARCH_REQUIRED
BLOCKED
OUT_OF_SCOPE
SUPERSEDED
```

Code written is not the same as capability verified.

---

# 61. RISK REGISTER

Track at minimum:

## Recording
- data loss;
- process death;
- background restrictions;
- manufacturer battery behavior;
- audio route changes;
- low storage;
- long recordings;
- WAV/storage cost.

## Speech
- model speed;
- model memory;
- battery;
- heat;
- Taglish accuracy;
- names;
- numbers;
- technical vocabulary;
- licensing.

## Language
- source ASR error;
- English translation error;
- negation reversal;
- uncertainty loss;
- responsibility inference;
- timestamp alignment.

## Product
- competitors add Taglish;
- user unwilling to download model;
- local processing too slow;
- cloud costs too high;
- unclear paid value.

## Cloud
- vendor outage;
- provider price change;
- duplicate billing;
- upload leakage;
- retention mismatch;
- account takeover.

## Privacy/legal
- consent misuse;
- transcript exposure;
- cloud vendor processing;
- logging leakage;
- breach response.

Each risk:
- ID;
- category;
- description;
- impact;
- likelihood;
- mitigation;
- validation required;
- status;
- evidence.

---

# 62. ANTI-VIBE-CODING RULE

Before adding a significant component, Codex must answer:

1. What user problem does this solve?
2. What current workflow consumes it?
3. What failure mode requires it?
4. What data does it store?
5. What privacy risk does it introduce?
6. What performance cost does it introduce?
7. What proves it works?
8. Can the app remain useful when it fails?

If these answers are unclear:
- investigate;
- do not add the component.

---

# 63. ANTI-ARCHITECTURE-THEATER RULE

Do not add these merely because they appear in “real backend” lists:

- Kubernetes;
- service mesh;
- sharding;
- leader election;
- distributed locks;
- saga pattern;
- multi-region;
- read replicas;
- Kafka;
- complex pub/sub;
- gRPC;
- event sourcing;
- CQRS;
- chaos engineering.

Introduce them only after:
- measured load;
- observed bottleneck;
- concrete reliability requirement.

The simplest system that meets the evidence-backed requirement wins.

---

# 64. ANTI-AI-MARKETING RULE

Never claim:
- “AI-powered understanding”;
- “high accuracy”;
- “best Taglish transcription”;
- “real-time”;
- “offline multilingual”;
- “works on low-end phones”;
- “encrypted”;
- “private cloud”;
- “speaker identification”;

unless the exact relevant capability is implemented and verified.

---

# 65. PROJECT PHASES

## PHASE 0 — REPOSITORY + PRODUCT + ARCHITECTURE FOUNDATION

Objective:
Create the factual project control plane.

Tasks:
- inspect repository;
- inspect Git;
- branch;
- remotes;
- history;
- current files;
- environment;
- Node;
- package manager;
- Android tooling;
- EAS availability;
- iOS development constraints;
- create docs;
- create risks;
- document Expo Go vs Development Build;
- document native boundary;
- document licensing risks;
- document benchmark design.

No product feature implementation.

Exit:
- docs exist;
- architecture internally consistent;
- project state factual.

---

## PHASE 1 — EXPO CROSS-PLATFORM SCAFFOLD

Objective:
Create a compiling/runnable cross-platform app shell.

Tasks:
- current stable Expo scaffold;
- TypeScript;
- Expo Router;
- design system;
- Home;
- Search;
- Settings;
- Record entry screen;
- mock Note Detail;
- theme;
- accessibility basics;
- Expo Go-compatible visual prototype;
- configure EAS;
- configure development build.

No production speech engine.

Exit:
- Expo UI works;
- Android development build works;
- iOS dev-build path documented/tested if device/credentials available;
- CI basics.

---

## PHASE 2 — SPEECH + AUDIO FEASIBILITY SPIKE

Objective:
Answer the existential speech-product question before building too much:

> Can a candidate on-device speech pipeline provide useful English/Filipino/Taglish Live Draft and Final Pass behavior within a resource envelope compatible with the recording-first architecture?

Build disposable/minimal spike code if necessary.

This phase is a speech/model/native-integration feasibility gate. It does **not** prove that the future production recording engine and live transcription can safely coexist for long sessions, backgrounding, screen lock, process interruption, or 60-minute use. Those combined production claims require the production recording engine and must be validated later in Phase 6 and Phase 12.

Test:
- candidate whisper.cpp models;
- quantization;
- English;
- Filipino;
- Taglish;
- time to first text;
- final accuracy;
- memory;
- battery;
- thermal behavior;
- iOS;
- Android;
- low-end Android where available.

Do not build accounts, cloud, summaries, or billing.

Exit:
- one of:
  - FEASIBLE;
  - FEASIBLE WITH LIMITATIONS;
  - NOT YET FEASIBLE;
- documented speech/model evidence;
- preliminary resource envelope;
- recommended device/model strategy;
- explicit list of production coexistence claims that remain unverified until Phase 6/12.

Do not describe Phase 2 as proof of production recording reliability.

If not feasible, revise architecture honestly.

---

## PHASE 3 — LOCAL DATA + STORAGE

Objective:
Durable local product state.

Tasks:
- SQLite;
- migrations;
- FTS;
- repositories;
- settings;
- file directories;
- SecureStore;
- model metadata foundation;
- tests.

Evaluate SQLCipher but do not claim encryption without full implementation.

---

## PHASE 4 — PRODUCTION RECORDING ENGINE

Objective:
Recording reliability independent of speech.

Tasks:
- authoritative capture;
- permission UX;
- background behavior;
- Android notification/service behavior;
- iOS background audio;
- incremental audio writing;
- pause/resume;
- stop;
- recovery;
- low storage;
- metering;
- tests.

Exit:
- audio remains valid after tested interruptions.

---

## PHASE 5 — LIBRARY + PLAYBACK

Objective:
Useful recorder without transcription.

Tasks:
- note list;
- rename;
- favorite;
- delete;
- manual note;
- player;
- seek;
- lifecycle;
- recovery UI.

---

## PHASE 6 — MODEL MANAGER + LIVE DRAFT + FINAL SOURCE TRANSCRIPT

Objective:
Productionize local speech.

Tasks:
- model manifest;
- download;
- checksum;
- install/remove;
- whisper.cpp integration;
- live draft;
- final pass;
- source segments;
- timestamps;
- user edit;
- capability profiles;
- bounded speech-queue integration with the production recording engine;
- verify that transcription backpressure cannot block or corrupt authoritative audio writing;
- initial production coexistence tests on available physical devices.

Phase 6 may validate short/representative recording + transcription coexistence, but long-session, background, interruption, battery, and thermal reliability claims remain for Phase 12.

---

## PHASE 7 — CANONICAL ENGLISH + MY VOCABULARY + CRITICAL MEANING

Objective:
Deliver the actual product differentiation.

Tasks:
- source-to-English strategy;
- preserve uncertainty/negation;
- My Vocabulary;
- correction learning with consent;
- important-detail extraction;
- review UI;
- English/source toggle;
- critical-meaning tests.

---

## PHASE 8 — SEARCH + SUMMARY + GROUNDED ASSISTANT

Objective:
Turn recordings into memory.

Tasks:
- FTS;
- snippets;
- timestamp navigation;
- local summary;
- action items;
- grounded Q&A;
- no-evidence behavior.

No vector database unless evidence requires it.

---

## PHASE 9 — EXPORT + PRIVACY + SECURITY + ACCESSIBILITY

Objective:
Finish a trustworthy local MVP.

Tasks:
- TXT/Markdown/audio export;
- privacy UX;
- deletion;
- open-source notices;
- threat model;
- accessibility audit;
- storage management;
- diagnostics.

This is the first reasonable public local-MVP candidate.

---

## PHASE 10 — OPTIONAL CLOUD IMPROVE BACKEND

Only begin if local product is stable.

Tasks:
- backend decision;
- auth;
- RLS;
- signed temporary upload;
- job model;
- rate limits;
- quota;
- idempotency;
- provider abstraction;
- retry/backoff;
- temp deletion;
- privacy disclosures;
- PIA update.

Do not add sync unless explicitly included.

---

## PHASE 11 — ACCOUNT + MONETIZATION

Only after:
- product value is validated;
- cloud cost is measured.

Tasks:
- free/pro/plus entitlement model;
- store-compliant billing;
- purchase restore;
- account flow where needed;
- cross-platform entitlement tests.

No forced account for free local use.

---

## PHASE 12 — HARDENING + COMPETITIVE BENCHMARK

Tasks:
- 5/30/60-minute tests;
- low storage;
- background;
- interruptions;
- battery;
- heat;
- benchmark corpus;
- competitor comparisons;
- fix critical failures;
- document limitations.

---

## PHASE 13 — RELEASE + PORTFOLIO

Prepare:
- screenshots;
- README;
- demo;
- architecture diagram;
- performance evidence;
- privacy explanation;
- benchmark method;
- limitations;
- changelog;
- store metadata;
- release checklist;
- portfolio case study.

---

# 66. PHASE COMPLETION PROTOCOL

One phase at a time.

Before editing:
1. read `MASTER_PROMPT.md`, `AGENTS.md`, and `CODEX.md` completely;
2. read `docs/PROJECT_STATE.md` if it exists;
3. inspect repository;
4. state the active goal and observable success criteria;
5. state phase objective;
6. state expected changed/new files;
7. state tests;
8. state privacy/security/performance implications;
9. use the `/scope-mvp` reasoning contract before substantial new scope;
10. delegate risky/cross-cutting review when useful;
11. plan proportional `/verify` evidence and adversarial review for non-trivial changes.

At end:

```text
PHASE <N> — <NAME>: COMPLETE | BLOCKED

Completed
- ...

Files changed
- ...

Commands run
- <command>
  Result: PASS | FAIL
  Important output: ...

Evidence
- ...

Manual checks required
- ...

Known limitations
- ...

Risks added/updated
- ...

Git status
- ...

Suggested commit message
- ...

Next allowed action
- CONTINUE PHASE <N+1>
```

Then stop.

Do not silently continue.

---

# 67. GIT SAFETY

Before work:
- inspect `git status`;
- inspect current branch;
- inspect remotes;
- inspect history.

Do not:
- run `git init` unless required;
- replace remotes;
- force reset;
- delete branches;
- automatically commit;
- automatically push;
- overwrite unrelated user work.

Suggest commits only.

---

# 68. CODEX WORKING RULES

Codex must:
- inspect before editing;
- prefer official current documentation;
- verify package versions;
- avoid stale examples;
- make small coherent changes;
- run actual verification commands;
- report actual output;
- stop when blocked by unavailable hardware/credentials;
- distinguish manual verification from automated tests;
- preserve founder-approved product decisions.

Codex must not:
- invent test results;
- invent device results;
- create cloud resources without the relevant phase;
- create subscriptions early;
- add analytics/ads;
- hide architectural risk;
- rewrite the entire repo without need.

---

# 69. FIRST CODEX COMMAND

After this file is saved as `MASTER_PROMPT.md` in the repository, give Codex:

```text
Read MASTER_PROMPT.md, AGENTS.md, and CODEX.md completely.

Treat:
- MASTER_PROMPT.md as the product and engineering constitution;
- AGENTS.md as the repository-wide agent/delegation operating policy;
- CODEX.md as the goal, scope, delegation, verification, adversarial-review, and phase workflow contract.

Begin PHASE 0 only.

Set one explicit Phase 0 goal with observable success criteria using the /goal convention from CODEX.md.

Use /scope-mvp reasoning before introducing any substantial new dependency, abstraction, service, infrastructure, or feature.

Delegate focused research/review to relevant subagents when it materially improves Phase 0 quality, while keeping the root agent responsible for final decisions and avoiding overlapping concurrent edits.

Before declaring Phase 0 complete, run /verify-style evidence accounting and an adversarial review of the resulting architecture/documentation.

Before editing, inspect the actual repository, Git state, current branch, remotes, commit history, files, environment, package/tooling state, Android tooling, Expo/EAS availability, and current limitations for iOS development from this environment.

Do not assume the repository is empty even if it was previously reported empty.

Do not scaffold the product yet.

Do not integrate whisper.cpp yet.

Do not create Supabase or any backend.

Do not create accounts, subscriptions, analytics, ads, or cloud AI.

During Phase 0, reconcile all architecture around these binding decisions:

1. TransVoice Notes targets iOS and Android.
2. The UI/application layer uses React Native + Expo + TypeScript unless Phase 0 finds a blocking reason.
3. Expo Go is only a prototype environment; real native speech/recording testing must use Expo Development Builds.
4. Recording reliability outranks every intelligence feature.
5. There is exactly one authoritative microphone capture path.
6. The product accepts English, Filipino/Tagalog, Taglish, and mixed speech as the intended language direction.
7. Live Draft is provisional and may remain source-language/mixed-language.
8. The finalized source transcript is preserved locally.
9. The primary canonical transcript is English.
10. Translation must preserve negation, uncertainty, names, numbers, dates, deadlines, technical terms, responsibility, and speaker intent.
11. Auto transcription is default, with Fast and Better Accuracy overrides.
12. whisper.cpp is the primary multilingual candidate but must pass Phase 2 feasibility benchmarks before production selection.
13. My Vocabulary is local by default and learns corrections only after explicit user approval.
14. Critical Meaning Check is a first-class product capability.
15. Core local use requires no account.
16. Cloud processing happens only when a user explicitly requests Improve Transcript.
17. Cloud infrastructure, Supabase, billing, sync, and subscription work are prohibited before their designated phases unless the founder explicitly changes the plan.
18. Do not add Kubernetes, sharding, queues, Redis, microservices, or distributed-system infrastructure without an evidence-backed current requirement.
19. Do not add an open-source license automatically.
20. Never claim a capability without evidence.

Create/update:
README.md
AGENTS.md
CODEX.md
docs/PRODUCT_SPEC.md
docs/ARCHITECTURE.md
docs/PHASES.md
docs/PROJECT_STATE.md
docs/DECISIONS.md
docs/RISK_REGISTER.md
docs/TEST_PLAN.md
docs/PERFORMANCE.md
docs/PRIVACY.md
docs/SECURITY.md
docs/THREAT_MODEL.md
docs/MODEL_AND_DATA_LICENSES.md
docs/COMPETITIVE_BENCHMARK.md
docs/CLOUD_ARCHITECTURE.md
docs/RELEASE_CHECKLIST.md
docs/TECH_STACK.md

Do not create product source code during Phase 0.

Run only commands that are actually necessary and available.

Never report a command as passing unless it ran successfully.

At the end, produce the Phase 0 completion report exactly as required by MASTER_PROMPT.md and stop.

Final line must be exactly one of:

NEXT ALLOWED ACTION: CONTINUE PHASE 1

or

NEXT ALLOWED ACTION: RESOLVE BLOCKER — <description>
```

---

# 70. FUTURE CODEX SESSION COMMAND

For later sessions:

```text
Read MASTER_PROMPT.md, AGENTS.md, CODEX.md, and docs/PROJECT_STATE.md completely.

Treat MASTER_PROMPT.md as the product constitution, AGENTS.md as the agent operating policy, and CODEX.md as the execution workflow contract.

Continue PHASE <NUMBER> only.

Set one active /goal for the phase with observable success criteria.

Use /scope-mvp before substantial new scope, /delegate when parallel specialist review materially improves quality, /verify before completion, and /adversarial-review for non-trivial changes.

Inspect the current repository and Git state before editing.

Follow the phase objective, non-negotiable product invariants, risk controls, and exit criteria.

Make the smallest coherent implementation that advances the phase.

Use current official documentation when dependency/platform behavior may have changed.

Run relevant tests/builds/lint/typecheck.

Update PROJECT_STATE, DECISIONS, RISK_REGISTER, PERFORMANCE, SECURITY, PRIVACY, and model/license documentation when the change affects them.

Do not invent verification.

Do not continue to another phase.

Stop after the required phase completion report.
```

---

# 71. FINAL PRODUCT PRINCIPLE

TransVoice Notes is not fundamentally an AI demo.

It is:

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

The user should be able to trust:

> **What I recorded will still be there even when the intelligence fails.**

The long-term product promise is:

> **Speak naturally. TransVoice turns English, Filipino, and Taglish speech into clear, searchable English memory while keeping the original evidence and keeping cloud processing under the user's control.**

The engineering promise is:

> **Reliability over cleverness. Evidence over confidence. Local privacy over cloud convenience. Measured scale over architecture theater.**