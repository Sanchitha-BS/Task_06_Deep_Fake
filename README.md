# Task 06 Deep Fake

> **Synthetic Media Disclosure:** This repository contains AI-generated audio artifacts. Both audio files were produced using ElevenLabs (free tier) text-to-speech. No real person's voice or likeness was cloned or depicted, all output is a synthetic reading of an original written script by stock ElevenLabs voices (Nathan and Lauren).

## Project Description

This project transforms a written narrative, a coach's end-of-season advisory reflection adapted from Task 5, into synthetic audio using free AI voice-generation tools. Two distinct voice presets from the same tool were used as the two iterations, and each output was critically evaluated and tested against three independent AI-detection/provenance methods.

## Repository Contents

| File | Description |
|---|---|
| `Source script.md` | The written narrative used as the script for both audio attempts |
| `Process log.md` | Detailed log of tools, settings, generation attempts, what worked, and what failed for each attempt |
| `Artifacts/` | The two synthetic audio files (labeled AI-generated) |
| `Evaluation.md` | Critical evaluation of each artifact: where it holds up, where it fails, and whether it would fool a casual listener |
| `Detection & Provenance.md` | Results of three detection/provenance checks run on both files, with tools and URLs used |

## Tools Used

- **ElevenLabs** (free tier): text-to-speech generation, https://elevenlabs.io
- **humantext.pro**: acoustic AI-voice detector, https://humantext.pro/ai-voice-detector
- **UncovAI**: acoustic AI-voice detector, https://uncovai.com/audio-detection
- **Content Credentials Verify**: C2PA metadata check, https://verify.contentauthenticity.org

## Process Summary

1. Adapted the Task 5 coach-advisory narrative into a standalone script (`Source script.md`)
2. Generated two audio attempts from the same script in ElevenLabs, using two different voice presets to test whether voice/tone choice affects delivery quality and detectability:
   - **Attempt 1:** Nathan, Natural Narrator
   - **Attempt 2:** Lauren, Empathetic and Encouraging
3. Critically evaluated both outputs by ear against consistent criteria (pronunciation, emotional range, pacing/pauses, breathing, emphasis)
4. Ran both files through two acoustic AI-voice detectors and one C2PA provenance check
5. Documented findings honestly, including where the artifacts failed to sound human

## How to Reproduce

1. Create a free account at [elevenlabs.io](https://elevenlabs.io)
2. Go to Text to Speech, paste in the script from `Source script.md`
3. Select a voice preset and generate; download the MP3, recording the exact settings used (see `Process log.md` for the settings used in this project)
4. Repeat with a second, distinctly different voice preset, again recording the settings
5. Listen to both closely against the criteria in `Evaluation.md` and document your own observations
6. Upload each file to the three detectors listed above and record the results

## What I Learned

- ElevenLabs' free tier embeds a real, cryptographically signed C2PA credential by default, naming the tool and issuer directly. This made provenance verification trivial for these specific files, but that signal is only as strong as the generating tool's choice to include it, and likely wouldn't survive re-encoding or screen recording.
- Acoustic detectors agreed with the C2PA result on both files but gave no reasoning behind their scores, just a confidence percentage.
- Voice/style choice (narrator vs. empathetic) had a real effect on how convincingly the emotional beats of the script landed, but no effect at all on whether detectors flagged the audio as synthetic.
- The clearest tell across both voices, on close listening, was not word-level pronunciation but the rhythm of speech. Missing breath pauses and inconsistent pacing around commas and paragraph breaks were the most consistent signs of synthetic delivery, more than any single mispronounced word.
