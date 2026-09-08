# Privacy Design

Last updated: 2026-09-09

This document is a design baseline, not legal advice and not yet a final privacy policy.

## Default privacy model

The local MVP is designed around:

- no required account;
- no advertising;
- no behavioral tracking;
- no required cloud AI;
- no automatic audio upload;
- no automatic transcript upload;
- app-private local storage;
- explicit export;
- explicit cloud Improve action only when introduced.

## Local data

Potential local data includes:

- audio recordings;
- source transcript;
- English canonical transcript;
- user edits;
- vocabulary;
- summaries;
- important details;
- manual notes;
- model metadata;
- settings.

Do not log raw content.

## Cloud Improve

When introduced, Cloud Improve must require explicit user action.

Before upload the user must be able to understand:

- what audio range is being uploaded;
- why it is being uploaded;
- that local audio remains authoritative;
- that cloud processing has different privacy characteristics;
- the provider/retention behavior that has actually been verified.

Prefer segment-level upload when only part of a transcript needs improvement.

Do not claim zero retention unless supported by current contractual/provider evidence.

## My Vocabulary

Vocabulary remains local by default.

Do not silently learn words from recordings.

A correction may be stored only after user approval.

## Recording consent

TransVoice must not:

- record secretly;
- auto-record from boot;
- hide microphone use;
- record phone calls;
- bypass OS privacy indicators.

For Philippine users, Republic Act No. 4200 is a relevant legal risk for secretly recording private communications. Product UX must not imply a universal right to record merely because the user is a participant.

Users remain responsible for applicable consent requirements, workplace/school policy, institutional rules, and local law.

## Philippine data protection baseline

If TransVoice later processes personal data through its own cloud services, the project must review current obligations under the Philippine Data Privacy Act and National Privacy Commission issuances.

Before public cloud launch:

- map personal data flows;
- conduct/update a Privacy Impact Assessment;
- document processors/vendors;
- create retention/deletion rules;
- create incident-response procedures;
- document security controls.

NPC guidance requires breach notification in specified cases within 72 hours after knowledge or reasonable belief that a notifiable breach has occurred.

## Diagnostics

If diagnostics are added:

Allowed examples:

- app version;
- OS version;
- device model;
- model version;
- error category;
- timing/performance counters.

Not allowed by default:

- full transcript;
- raw audio;
- vocabulary contents;
- manual notes;
- API credentials.

Prefer opt-in diagnostic submission.

## Deletion

Local deletion should remove:

- DB metadata;
- audio;
- derived text/artifacts;
- associated local temp data.

If cloud data exists later, the UI must distinguish:

- delete locally;
- delete everywhere.

Cloud deletion must be verified rather than assumed.
