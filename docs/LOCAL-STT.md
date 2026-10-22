# Transcription on this Mac

Sidekick can transcribe your meetings on your Mac with [whisper.cpp](https://github.com/ggml-org/whisper.cpp). The
audio never leaves it. Sidekick still needs an AI key for the coaching (cards, debriefs, reviews), unless you point it
at a local server (below).

## Set it up

1. Open Settings › Transcription (or choose it during onboarding).
2. Pick **On this Mac** and a model. Sidekick downloads it once and keeps it on your Mac.
3. Start listening as usual. Imported recordings use the same transcription.

If your copy of Sidekick doesn't include the on-device helper, the option reads "On this Mac (not in this build)" and
everything else works as before.

## Models

| Model | Size | Use |
|---|---|---|
| Large v3 turbo (q5) | about 550 MB | the default; handles several languages, including bilingual meetings |
| Small (q5) | about 190 MB | faster, less accurate |
| Base (q5) | about 60 MB | older Macs |

Sizes are approximate; the app shows the real size before it downloads. A download is only used once it is complete.
Models live in `~/Library/Application Support/MeetingHUD/models/`.

## Privacy

- The transcription helper only accepts connections from your own Mac and reads a model file from disk.
- With a cloud AI key, only the coaching text goes to your provider. With a local server, nothing leaves the Mac.
- Meeting audio is temporary and is deleted once the after-meeting steps finish ([Your progress is never touched](/docs/data-safety)).

## Speed and accuracy

We haven't measured transcription speed or accuracy on different Macs yet, so Sidekick makes no promises about them.
Larger models are slower and more accurate; if cards feel late on your Mac, try the smaller model.

## A local AI server for cards and reviews (experimental)

Settings › Transcription › Advanced takes an OpenAI-compatible address, for example Ollama's
`http://127.0.0.1:11434/v1` or LM Studio's. The server must support structured output, and you choose which of its
models write the live cards and which write everything else. Small models often return answers the review cannot read,
which is why this isn't the default.
