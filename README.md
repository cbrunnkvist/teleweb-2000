# TeleWeb 2000

A Y2K-era novelty desk phone simulator. Press the keypad for authentic DTMF tones, then hit **"Pick up and make a call"** to be connected to a random utility company's on-hold recording.

Yes, it works.

[Play it here](https://cbrunnkvist.github.io/teleweb-2000/)

![TeleWeb 2000 Screenshot](screenshot.png)

## Features

- **Authentic US ringback tone** — 440 Hz + 480 Hz, 2 seconds on / 4 seconds off, generated on the fly via Web Audio API before the "call connects"
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

- Call flow: dial → **6 seconds of authentic US ringback** (440+480 Hz) → typewriter "Call in progress..." → random utility company IVR plays → "CALL COMPLETED" → auto-hangup

## License

The code is mine. The recordings are public-domain hold messages recorded from utility company phone lines. The libgsm WASM build inherits the original TU Berlin libgsm copyright.
