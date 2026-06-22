# TeleWeb 2000

A Y2K-era novelty desk phone simulator. Press the keypad for authentic DTMF tones, then hit **"Pick up and make a call"** to be connected to a random utility company's on-hold recording.

Yes, it works.

[Play it here](https://cbrunnkvist.github.io/teleweb-2000/)

![TeleWeb 2000 Screenshot](screenshot.png)

## Features

- **Random-duration US ringback tone** — 440 Hz + 480 Hz, 2 seconds on / 4 seconds off, plays for a random 1–6 seconds before each call "connects"
- **Real-time DTMF tones** — Web Audio API sine wave generation with proper frequency pairs
- **In-browser GSM 06.10 decoder** — libgsm compiled to WebAssembly; the `.gsm` recordings are decoded entirely client-side
- **66 utility company IVR samples** — call centers from Anaheim to Montana, all circa 2018–2020
- **Responsive scaling** — fits vertically on any viewport like a real desk phone should
- **LCD scanlines** — character-cell display with typewriter effect and scrolling marquee

## Architecture

Single HTML file. No build step. No dependencies. 71 files total, 3.5 MB of hold music.

| Component | Size | What |
|---|---|---|
| `index.html` | ~30 KB | UI, CSS, JavaScript |
| `gsm_decoder.wasm` | 16 KB | libgsm compiled via Emscripten |
| `gsm_decoder.js` | 13 KB | Emscripten WASM glue |
| `gsm/*.gsm` | ~3.5 MB | 66 on-hold recordings |

## Technical details

- Call flow: dial → **1–6 seconds of random-duration US ringback** (440+480 Hz) → typewriter "Call in progress..." → random utility company IVR plays → "CALL COMPLETED" → auto-hangup

## License

The interactive exhibit was created by [@cbrunnkvist](https://github.com/cbrunnkvist). The code is mine.

The IVR recordings are on-hold messages captured from US utility company phone lines. Their original recorder — whoever you are, somewhere on the internet — did the legwork of collecting and sharing these in GSM format around 2019. You deserve credit and I'd love to know who you are.

The libgsm WASM build inherits the original TU Berlin libgsm copyright.
