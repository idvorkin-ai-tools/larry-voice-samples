# Larry Voice Catalog — Gemini 3.1 Flash TTS preview

**Date**: 2026-04-16
**Model**: `gemini-3.1-flash-tts-preview`
**Endpoint**: `https://generativelanguage.googleapis.com/v1beta/models/gemini-3.1-flash-tts-preview:generateContent`
**Test phrase**: "Hi Igor, this is Larry testing the Gemini voice catalog at regular pacing."

All audio: 24 kHz mono 16-bit WAV, ~5-7 seconds per clip.

---

## 17/30 voices actually available on preview endpoint

| Voice       | Wall-clock | Notes (from Google catalog + ear)        |
| ----------- | ---------- | ---------------------------------------- |
| Aoede       | 5.21s      | "Warm"                                   |
| Algenib     | 4.78s      | Neutral                                  |
| Algieba     | 5.97s      | Neutral                                  |
| Autonoe     | 4.77s      | Neutral                                  |
| Callirrhoe  | 4.18s      | Fastest gen                              |
| Charon      | 5.32s      | **Current Larry default** — baritone     |
| Despina     | 5.51s      | Smooth                                   |
| Enceladus   | 5.18s      | Male-coded                               |
| Erinome     | 4.24s      | Neutral                                  |
| Fenrir      | 6.75s      | "Excitable baritone" — widest dynamic    |
| Iapetus     | 4.66s      | Neutral-to-cool                          |
| Kore        | 4.38s      | "Firm" — reads feminine in ear           |
| Leda        | 4.70s      | Neutral-warm                             |
| Orus        | 4.88s      | "Lively male"                            |
| Puck        | 5.57s      | "Upbeat" — playful male                  |
| Umbriel     | 4.29s      | Neutral                                  |
| Zephyr      | 5.51s      | Airy                                     |

## 13/30 voices NOT available (preview endpoint silent-rejects)

Achernar, Achird, Alnilam, Gacrux, Laomedeia, Pulcherrima, Rasalgethi, Sadachbia, Sadaltager, Schedar, Sulafat, Vindemiatrix, Zubenelgenubi

Documented in Google's voice catalog, not rolled out to `gemini-3.1-flash-tts-preview` as of 2026-04-16. Might ship later.

---

## Baritone shortlist for Larry

- **Charon** (current default) — deep storyteller
- **Fenrir** — wider dynamic range, good for emphasis
- **Orus** — "lively male" — more active than Charon
- **Puck** — upbeat, playful

## Timing summary

- Mean wall-clock: ~5.1s for ~5-6s of audio (~1:1 realtime)
- Rate limit: 10 req/min on preview tier — parallel bursts hit 429
- Serial pacing at 7s between calls stays within limits

## Reproducibility

All samples generated via:

```bash
bash ~/gits/chop-conventions/.worktrees/gen-tts-skill/skills/gen-tts/gemini-tts.sh \
  "Hi Igor, this is Larry testing the Gemini voice catalog at regular pacing." \
  --voice <VOICE_NAME> \
  --output /tmp/larry-voices-all/<VOICE_NAME>.wav
```

(Note: bash layer has since been ported to Python-only — see PR #138. Equivalent Python call uses `./generate-tts.py --text "..." --voice <VOICE_NAME> --output ...`.)
