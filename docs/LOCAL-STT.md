# Transcription on this Mac

`[stt] provider = "local"` transcribes with [whisper.cpp](https://github.com/ggml-org/whisper.cpp) on the Mac: the
audio never leaves it. The helper listens on 127.0.0.1 only and reads a model file from disk. Sidekick still needs an
AI key for the coaching (cards, debriefs, reviews, the interview), unless you point it at a local server (below).

## How it fits together

| Piece | File | What it does |
|---|---|---|
| Helper | `backend/native/whisper/build.sh` → `bin/whisper-server` | whisper.cpp's HTTP server, Metal, static, arm64, macOS 14.2+ |
| Supervisor | `backend/hud/local_stt.py` `WhisperServer` | starts the helper once with the chosen model, reuses it, stops it on quit |
| Live stream | `LocalSTT` | one decode per utterance (the VAD already cuts them); finals in order; whisper's silence phrases dropped |
| Batch | `LocalClips` via `batch_stt` | imported recordings; post-meeting re-transcription is skipped when live was already local |
| Models | Settings › Transcription, onboarding | downloaded on request into `~/Library/Application Support/MeetingHUD/models/` |

## Building the helper

```bash
make whisper
```

It needs git and the Xcode Command Line Tools. cmake comes from your PATH or from PyPI through `uvx`. It downloads
whisper.cpp at the tag in `build.sh` (`WHISPER_TAG` overrides it; check the project's releases before a release
build). `scripts/bundle-backend.sh` copies the binary into the app (`WHISPER=1` builds it first), and
`hud/scripts/sign-helpers.cjs` signs it with the same identity as the audio helper. A build without it shows
"On this Mac (not in this build)" and everything else works.

## Models

| Key | File | Approx. size | Use |
|---|---|---|---|
| `large-v3-turbo-q5_0` | `ggml-large-v3-turbo-q5_0.bin` | 550 MB | default; multilingual (the bilingual case) |
| `small-q5_1` | `ggml-small-q5_1.bin` | 190 MB | faster, less accurate |
| `base-q5_1` | `ggml-base-q5_1.bin` | 60 MB | older Macs |

Downloads come from `SIDEKICK_MODEL_BASE_URL` (default: the whisper.cpp model repository on Hugging Face), are written
to a `.part` file and renamed only when complete. The sizes above are approximate; the app shows the real size from
the server.

## Measurements (to do on real hardware)

Nothing below has been measured yet, and the README and the app make no speed or accuracy claims until it is.

| Mac | Model | Real-time factor | Card latency added | WER on the bilingual fixture |
|---|---|---|---|---|
| M1 8 GB | small-q5_1 | | | |
| M1 8 GB | large-v3-turbo-q5_0 | | | |
| M2/M3 16 GB+ | large-v3-turbo-q5_0 | | | |

How to measure: `hud doctor` runs a self-test (a phrase synthesized to a file with `say -o`, never played aloud) and
prints the decode time; for meeting-length numbers, run `hud replay` with `FileAudioSource` on recorded WAVs.

## A local AI server for cards and reviews (experimental)

Settings › Transcription › Advanced takes an OpenAI-compatible address, for example Ollama's
`http://127.0.0.1:11434/v1` or LM Studio's. Sidekick uses the Responses API with structured output, so the server must
support both, and `[llm] openai_tick_model` (cards) and `openai_deep_model` (everything else) must name its models. Small models
often return answers the review cannot read; this is why it is not the default.
