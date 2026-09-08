# Product Specification

Last updated: 2026-09-09

## Product summary

TransVoice Notes is a local-first voice-memory app for iOS and Android designed around natural Filipino communication: English, Filipino/Tagalog, Taglish, and mixed-language speech.

The primary user outcome is not "AI transcription." It is:

> Capture speech safely, preserve what was actually said, turn it into clear English, and make it easy to search, review, and remember.

## Core audience

Initial audience:

- people in the Philippines who naturally code-switch between English and Filipino;
- students recording lectures or study notes;
- professionals recording meetings, interviews, ideas, and reminders;
- users on ordinary Android phones as well as iPhones;
- privacy-conscious users who do not want every recording uploaded by default.

The product should remain understandable to non-technical users.

## Core jobs to be done

1. **Capture:** Record a conversation, lecture, meeting, idea, reminder, or interview reliably.
2. **Understand:** See an almost-immediate Live Draft while speaking when the device can support it.
3. **Preserve meaning:** Retain a timestamped source-language/mixed-language transcript and audio evidence.
4. **Normalize:** Produce an English canonical transcript without inventing certainty, deadlines, assignments, names, or facts.
5. **Review critical information:** Highlight important names, amounts, dates, times, deadlines, negation, uncertainty, decisions, and responsibilities.
6. **Remember:** Search notes and jump back to the relevant audio timestamp.
7. **Improve:** Optionally request cloud-based transcript improvement for a section or whole recording.
8. **Adapt:** Learn user-approved vocabulary corrections such as names, companies, technical terms, or local places.

## Primary product promise

**Speak the way Filipinos actually speak.**

The product should handle language mixing as normal behavior rather than as an error state.

## Non-negotiable requirements

### Audio first
Audio preservation has higher priority than transcription, translation, summary, search, and assistant features.

### No required account
The local product must work without registration.

### Local-first
Recording, playback, local storage, search, and supported local transcription should work without a permanent internet connection after required local assets are installed.

### Explicit cloud use
Cloud processing must never happen silently. The user explicitly chooses **Improve Transcript**.

### Evidence preservation
The original audio and source transcript remain available so English normalization can be audited.

### Meaning preservation
Canonical English must preserve:

- negation;
- uncertainty;
- conditional language;
- names;
- numbers;
- amounts;
- dates;
- times;
- deadlines;
- technical terms;
- responsibilities;
- chronology;
- decisions.

### User edits are authoritative
Automatic processing must never silently overwrite a user-approved correction.

## Transcription modes

### Auto — Recommended
The app chooses a device-appropriate strategy using measured capability.

### Fast
Prioritizes low latency and resource use.

### Better Accuracy
May use a larger model or longer post-processing.

The UI must explain tradeoffs plainly.

## Live Draft vs Final Transcript

The product intentionally separates speed from finality:

- **Live Draft:** fast, provisional, may remain Taglish/Filipino, can change.
- **Final Source Transcript:** higher-accuracy transcript tied to timestamps.
- **Canonical English:** meaning-preserving English representation derived from source evidence.

## My Vocabulary

Users can add vocabulary manually or approve detected corrections.

Examples:

- `Supabase`
- a colleague's name;
- a school name;
- a barangay/city;
- technical terms;
- project-specific jargon.

The app should never silently store vocabulary learned from private speech.

## Critical Meaning Check

A transcript is not considered trustworthy merely because its overall word error rate is low.

The app should separately review high-impact details such as:

- ₱15,000 vs ₱50,000;
- Friday vs Thursday;
- "not approved" vs "approved";
- "maybe Friday" vs "Friday";
- "Mark could handle it" vs "Mark will handle it."

Important details should remain tied to source evidence.

## MVP boundary

The local MVP includes:

- onboarding;
- local recording;
- recovery;
- playback;
- note library;
- local storage;
- local search;
- local model management;
- Live Draft where feasible;
- final source transcript;
- canonical English where locally feasible;
- My Vocabulary;
- Critical Meaning Check;
- local summary/action extraction;
- export;
- privacy/security UX.

The local MVP does **not** require:

- cloud account;
- subscription;
- sync;
- team collaboration;
- meeting bots;
- web dashboard;
- Kubernetes;
- microservices;
- semantic vector search;
- multi-region infrastructure.

## Future paid model

Preferred direction:

### Free
No account required. Local recording and core local use remain useful.

### Pro
Potential one-time unlock for advanced local features.

### Plus / Cloud
Subscription only for genuine recurring services such as cloud Improve Transcript, cross-device sync, encrypted backup, or expensive cloud processing.

Pricing is not yet decided.

## Success criteria

The product is successful when users can trust three things:

1. **My recording will still be there.**
2. **The app will not silently turn uncertainty into certainty.**
3. **I can find and understand what mattered later.**
