# Detection & Provenance Check

Both synthetic audio artifacts were generated with **ElevenLabs** (free tier) and tested against three independent detection methods: two acoustic/neural pattern detectors and one metadata-based provenance check.

## Artifacts Tested

| Attempt | Voice | Style | File |
|---|---|---|---|
| 1 | Nathan | Natural Narrator | `Artifacts/01_elevenlabs_nathan-narrator_AI-GENERATED.mp3` |
| 2 | Lauren | Empathetic and Encouraging | `Artifacts/02_elevenlabs_lauren-empathetic_AI-GENERATED.mp3` |

## Detection Methods

1. **humantext.pro**, https://humantext.pro/ai-voice-detector: acoustic/neural pattern analysis, browser-based, no signup
2. **UncovAI**, https://uncovai.com/audio-detection: spectral, prosodic, and formant transition analysis, returns a calibrated probability score
3. **Content Credentials Verify**, https://verify.contentauthenticity.org: C2PA content credential check (reads embedded cryptographic metadata rather than analyzing the waveform)

## Results

| Detector | Method | Nathan | Lauren |
|---|---|---|---|
| humantext.pro | Acoustic pattern analysis | 100%, "likely AI-generated" | 100%, "likely AI-generated" |
| UncovAI | Spectral/prosodic/formant analysis | 99% probability, verdict "AI Generated" | 99% probability, verdict "AI Generated" |
| Content Credentials (C2PA) | Embedded metadata | Confirmed: issued by **Eleven Labs Inc.**, AI tool "ElevenLabs," content summary "This audio was generated with an AI tool." Timestamped Aug 10, 2026, 4:33 PM CDT | Same result, valid C2PA credential issued by Eleven Labs Inc. |

Both files were caught by all three methods, with no disagreement between detectors and no false negatives.

## Findings

**All three agreed, but not all are equal evidence.** The acoustic detectors (humantext.pro, UncovAI) inferred their verdict from the waveform, spectral artifacts, prosody, formant transitions, and returned a confidence score (100%, 99%) with no explanation of which cues triggered it. The C2PA check is stronger: it reads a cryptographically signed credential ElevenLabs embeds by default, naming the issuer and tool directly, no inference required. A more adversarial artifact (screen-recorded or re-encoded output) would likely strip that metadata, leaving only the acoustic detectors, which give a probability, not proof.

**Voice/style had no effect on detectability.** Nathan (narrator) and Lauren (empathetic) were flagged identically across all three tools, suggesting detection keys on the ElevenLabs engine's underlying synthesis signature rather than surface-level tone.

## Takeaway

Provenance metadata (C2PA) is the more reliable, explainable signal of the three, but it depends entirely on the generating tool choosing to embed it, and on that metadata surviving any downstream processing (re-encoding, screen recording, platform upload). Acoustic detectors are more robust to that kind of stripping, since they analyze the audio itself, but they trade that robustness for opacity: a confidence score with no stated reasoning.
