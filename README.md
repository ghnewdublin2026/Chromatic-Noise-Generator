**CHROMATIC NOISE** — your full-featured colour noise studio in a single HTML file.

**What's included:**

**8 noise types** — White, Pink, Violet, Blue, Green, Grey, Brown, Black — each rendered by a dedicated AudioWorklet processor running on a separate audio thread (no dropouts). Each card glows in its signature colour and clicking updates the entire UI theme + active noise.

**Info panel** — full technical definition (spectral characteristics, named after physics/maths origins) plus 5 real-world use case tags per noise type, updated live on selection.

**Tremolo** — enable toggle, Speed slider showing seconds-per-cycle (0.1s → 10s), Strength 1–100%. Uses a sine LFO modulating a gain node so the audio pulses between `(1−strength)` and `1` at the chosen rate.

**Compressor** — 4 presets:
- **Off** — fully bypassed
- **Default** — −24 dB threshold, 4:1 ratio, gentle settings
- **Min** — light touch, −10 dB threshold, 2:1
- **Max** — hard limiting, −40 dB threshold, 20:1, near-zero attack

When active, it shows live **dB GR** (gain reduction) with an animated gradient bar, plus a 4-cell stats grid with Threshold / Ratio / Attack / Release values.

**Spectrum visualiser** — frequency bars rendered in the current noise colour, live from the Web Audio analyser node.
