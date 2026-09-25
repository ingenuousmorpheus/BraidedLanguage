# Braided Language — Human Language Pack Plan

Status: Planned subsystem
Purpose: provide the Google-Translate-style human-language experience inside Braided Language while sharing the same Braided Representation used by animal/marine communication.

## Goal

Human Language Pack should support:

- automatic language detection;
- text translation;
- speech-to-text;
- translated speech output;
- conversation mode;
- subtitles/transcripts;
- transliteration;
- locale/accent selection;
- downloadable/offline language packs where practical;
- confidence and fallback behavior;
- Android-first mobile use;
- phone ↔ PC hybrid inference.

## Architecture

```text
human speech / text
        ↓
language detection
        ↓
speech recognition (if audio)
        ↓
Braided Representation
        ↓
target-language generation
        ↓
text / subtitles / speech
```

The Human Language Pack is one branch of the larger system:

```text
BRAIDED LANGUAGE
├─ Human Language Pack
├─ Animal Communication Pack
├─ Marine / Dolphin-Whale Pack
├─ Braided Representation
└─ Echo Engine
```

## BL-HL-01 — Text Translation

- source-language auto-detect;
- source text input;
- target-language selection;
- translated text output;
- copy/share support;
- confidence / model provenance;
- literal vs natural mode.

Gate: common bilingual test sets produce acceptable semantic translations and errors are surfaced honestly.

## BL-HL-02 — Speech Translation

- microphone input;
- VAD;
- streaming STT;
- language detection;
- low-latency translation;
- local TTS;
- translated transcript.

Gate: two-way spoken translation works without manually stopping after every sentence.

## BL-HL-03 — Conversation Mode

Two-person mode:

```text
Speaker A
↓
detect language
↓
translate
↓
speak/display for B

Speaker B
↓
detect language
↓
translate
↓
speak/display for A
```

Include:
- speaker-turn detection;
- interruption handling;
- transcript;
- optional translated subtitles.

## BL-HL-04 — Downloadable Language Packs

Support installable language bundles when the chosen models/runtime allow it.

Each pack records:
- language / locale;
- text translation model;
- STT support;
- TTS voice support;
- transliteration support;
- approximate disk/RAM needs;
- offline capability;
- license.

Example logical packs:

```text
English ↔ Spanish
English ↔ French
English ↔ Japanese
English ↔ Arabic
English ↔ Mandarin
...
```

Avoid hard-coding pair-specific architecture if a multilingual model can cover many languages efficiently.

## BL-HL-05 — Transliteration / Script Support

Support:
- romanization/transliteration;
- original script preservation;
- pronunciation-friendly display;
- bidirectional text;
- non-Latin scripts;
- locale-specific punctuation and typography.

## BL-HL-06 — Translation Memory

Optional local-first memory for:
- repeated phrases;
- names;
- project/domain terminology;
- preferred translations;
- user corrections.

Never silently overwrite explicit user corrections.

## BL-HL-07 — Mobile UI

Primary mobile flow:

```text
[ AUTO DETECT ] → [ TARGET LANGUAGE ]

[ LISTEN ]

Original:
...

Translation:
...

[ Speak ] [ Copy ] [ Save ]
```

Conversation view:
- split-screen or alternating speaker cards;
- live text;
- translated text;
- confidence;
- speaker labels.

## BL-HL-08 — Braided Representation Bridge

Human translation should pass through the same semantic layer where useful so the project can later share meaning structures with:

- animal interpretation;
- marine research;
- unknown-signal analysis;
- game/AR translation.

This is the architectural reason the Human Language Pack belongs inside Braided Language rather than as a disconnected translator.

## BL-HL-09 — Offline / Hybrid Strategy

Phone-local where possible:
- VAD;
- language ID;
- lightweight STT;
- cached translation;
- basic TTS.

PC-hosted when needed:
- larger multilingual models;
- long-form speech;
- higher-quality TTS;
- research models.

If the host is unavailable, capability must degrade honestly instead of pretending the full translator is active.

## BL-HL-10 — Evaluation

Measure:
- semantic accuracy;
- word error rate for STT;
- latency;
- turn-taking accuracy;
- robustness to noise;
- transliteration correctness;
- TTS intelligibility;
- offline/online parity.

## Product rule

Human translation should feel as simple as a mainstream translator app, while Braided Language keeps the deeper shared semantic architecture underneath.

The user should not need to think about the intermediate representation unless they open Research/Details.
