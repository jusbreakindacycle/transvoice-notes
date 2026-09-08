# Competitive Benchmark Plan

Last updated: 2026-09-09

## Objective

Do not claim that TransVoice is "better" because its feature list sounds stronger.

Test the same recordings under controlled conditions against current competitor products.

## Initial comparison set

Where supported and available at benchmark time:

- Google Recorder / Pixel Recorder;
- Samsung Voice Recorder / Transcript Assist;
- Otter;
- Notta;
- Plaud;
- relevant local/offline Whisper mobile apps.

The exact comparison list must be refreshed at benchmark time because product capabilities change.

## Test corpus

Create a consented, controlled benchmark corpus.

Separate categories:

- English;
- Filipino;
- light Taglish;
- heavy Taglish;
- technical Taglish;
- casual Taglish;
- meeting-like speech;
- reminder/task speech;
- noisy room;
- quiet room;
- slow;
- fast.

Important content must include:

- Filipino names;
- Philippine place names;
- peso amounts;
- dates;
- times;
- uncertain deadlines;
- negation;
- conditional statements;
- responsibility assignments;
- software/technical jargon.

## Metrics

### Recognition quality
- WER or suitable text-error metric;
- names;
- numbers;
- money;
- dates;
- times;
- technical terms.

### Meaning quality
- negation preserved;
- uncertainty preserved;
- responsibilities preserved;
- decisions preserved;
- no unsupported certainty.

### Product behavior
- time to first transcript;
- time to final transcript;
- whether mixed languages require manual switching;
- source transcript availability;
- timestamp traceability;
- editability;
- search.

### Privacy/availability
- account required;
- internet required;
- audio uploaded by default;
- free-tier limits;
- supported hardware limitations.

## Blind review

Where practical, remove product names and ask reviewers to score transcripts without knowing which app produced them.

## Anti-cherry-picking rule

Do not:

- publish only examples where TransVoice wins;
- silently change competitor settings to make them worse;
- compare paid TransVoice against free competitor tiers without disclosure;
- compare different audio recordings;
- use unverified marketing claims as measured results.

## Result format

| Sample | Category | Product | General error | Critical meaning | Time to result | Privacy/cloud | Notes |
|---|---|---|---|---|---|---|---|

## Claim gate

"Better Taglish transcription" may only be used publicly after:

- representative corpus exists;
- methodology is documented;
- relevant competitors are tested;
- critical-meaning failures are included;
- results are reproducible;
- limitations are disclosed.
