# Pianorad 1926 – Fitch Edition  
**Cmajor Emulation of the World’s First Vacuum-Tube Polyphonic Synthesizer**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)  
[![Cmajor](https://img.shields.io/badge/Powered%20by-Cmajor-FF6B00.svg)](https://cmajor.dev)

A faithful software recreation of the **1926 Pianorad** designed by Hugo Gernsback and built by Clyde J. Fitch at Radio News Laboratories.  
This is **not** a modern wavetable or subtractive synth — it is a literal 25-voice parallel LC-tank oscillator engine, exactly as the original hardware worked: one Audion triode + fixed honeycomb coil + mica capacitor per key.

Pure sine waves are **not** the final goal. The historic “exquisite pureness better than a flute” tone is only the starting point. The real 1926 character lives in the **mastering chain** — the tube warmth, voltage sag, narrow AM bandwidth, and WRNY radio air that made the instrument sound alive when broadcast from station WRNY.

## Historical Context
- June 12, 1926: Public debut at WRNY’s first anniversary broadcast (Ralph Christman playing live).  
- 25 independent vacuum-tube oscillators (no frequency dividers, no shared master clock).  
- Mechanical iron-core filter + top-mounted exponential horn speaker.  
- Artists could play in absolute studio silence while listeners heard the performance miles away via radio.  
- Only surviving technical details come from *Radio News* Nov/Dec 1926 issues (no patent, no full schematic ever published).

This Cmajor patch revives that exact parallel-oscillator architecture with modern tube-drift and shared B+ voltage-sag modeling.

## Features
- True 25-note polyphony (one oscillator per key — hardware limit respected)  
- Per-voice LC resonance math: `f = 1 / (2π√(LC))` with real-time drift & sag modulation  
- Audion triode saturation (tanh soft-clip)  
- Shared 90 V B+ “voltage sag” that affects pitch and amplitude as chords grow denser  
- Slow tube-age drift (filament warm-up wander)  
- WRNY broadcast simulation (narrow 4–6 kHz bandwidth + 1920s static)  
- Mechanical horn filter (variable cutoff)

## Installation & Requirements
1. Download the **Cmajor** runtime & plugin host from [cmajor.dev](https://cmajor.dev)
2. Clone or download this repo
3. Open `Pianorad_Fitch_Edition.cmajor` in the Cmajor Patch Player or load it as a VST3/AU/AAX inside your DAW via the official Cmajor wrapper
4. Route a MIDI keyboard (2-octave range is perfect)

## Patch Parameters (Hardware-Accurate)
| Group       | Parameter              | Range          | Default | What it does (1926 equivalent)                              |
|-------------|------------------------|----------------|---------|-------------------------------------------------------------|
| Hardware    | Tube Condition (Drift) | 0.0 – 0.15     | 0.03    | Filament age wander (slow sine modulation on C)             |
| Hardware    | B+ Voltage Sag (IMD)   | 0.0 – 0.6      | 0.18    | Shared power-rail drop when many voices play                |
| Tone        | Audion Saturation      | 0.0 – 2.5      | 0.9     | Triode grid/plate curve (tanh shaping)                      |
| Tone        | Horn Mechanical Filter | 800 – 9000 Hz  | 4200 Hz | Iron-core damping / exponential horn resonance              |
| Output      | WRNY 1926 Broadcast    | On/Off         | Off     | 5 kHz low-pass + vintage radio crackle                      |
| Output      | Master Volume          | 0.0 – 2.0      | 0.85    | Final gain stage                                            |

## Recommended Mastering Chain  
**“1926 WRNY Character Chain”**  
(The pure sine is only the raw oscillator. These effects turn it into the real Pianorad sound.)

Apply this chain **after** the Pianorad patch on a dedicated bus or master track. Keep everything subtle — the goal is 1920s radio, not modern loudness.

### 1. Tube Saturation / Harmonic Exciter (first in chain)
- **Softube Saturation Knob** (free) or **FabFilter Saturn 2** (Tube mode)  
  Settings:  
  - Drive: 15–30 %  
  - Mix: 25–40 % wet  
  - Keep Highs: On  
  - Focus: Even harmonics only (for classic triode warmth)

### 2. Analog Tape / Glue Stage
- **Softube Tape** or **Chow Tape Model** (free) or **Waves J37**  
  Settings:  
  - Input: –6 dB  
  - Saturation: 8–12 %  
  - Flutter: 0.15 %  
  - High-frequency bias roll-off: –2 dB @ 8 kHz

### 3. Vintage EQ & Bandwidth Limiting (the “horn” sound)
- **FabFilter Pro-Q 3** (or stock DAW EQ)  
  Curve:  
  - High-pass: 100 Hz, 12 dB/oct  
  - Low-pass: 5 200 Hz, 18 dB/oct (mimics 1926 AM transmitter)  
  - Gentle bell boost: +2 dB @ 2.8 kHz, Q=1.2 (horn presence)

### 4. Light Optical Compression
- **PSP Vintage Warmer** or **Waves CLA-2A** or **FabFilter Pro-C 2**  
  Settings:  
  - Ratio: 3:1  
  - Attack: 25 ms  
  - Release: 300 ms  
  - Gain reduction: never more than 3–4 dB on loudest chords

### 5. Radio Air & Noise Layer (the WRNY atmosphere)
- **iZotope Vinyl** (free) or **Waves Retro Fi**  
  Settings:  
  - Dust/Crackle: 8–12 %  
  - Hiss: –55 dB (high-passed at 6 kHz)  
  - Wow: 0.08 %  
  - Mix: 7–14 % (automate on/off for “transmission” sections)

### 6. Final Gentle Limiter
- **FabFilter Pro-L 2** or stock limiter  
  Settings:  
  - Ceiling: –1.0 dB  
  - Style: “Vintage” or “Punchy”  
  - True Peak: On  
  - Target loudness: –12 to –10 LUFS (leave headroom — this is 1926, not 2026)

**Quick “One-Click” Preset Tip**  
Many users combine steps 1–2 into **Black Box HG-2** or **UAD Oxide** and steps 3–5 into **Waves Retro Fi** (set to “1920s Radio” preset) for a 3-plugin chain that sounds astonishingly close to the original WRNY broadcasts.

## Demo Recordings
(coming soon — add your own!)  
- Pure chords (dry)  
- Full WRNY chain (broadcast style)  
- Silent Studio mode (main out muted, only headphone bus)

## How to Contribute
- Fork the repo  
- Add variants (Pure Sine branch, Staccatone mono mode, etc.)  
- Submit pull requests for new parameters or improved sag modeling  
- Share your DAW project files or audio demos

## License
MIT — free for any use, commercial or non-commercial. Credit is appreciated but not required.

## References & Further Reading
- *Radio News*, November 1926, pp. 492–495 (Gernsback article)  
- *Radio News*, December 1926, p. 655 (“How to Build the Pianorad” by Clyde J. Fitch)  
- Cmajor documentation: https://cmajor.dev  
- Original photos & history: Electronic Music History archives

---

Made with love for electronic music history by **@TheRealla**  
Star the repo if you enjoy the sound — every star helps this obscure 1926 instrument reach more synth enthusiasts!
