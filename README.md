# 🎨 CHROMATIC NOISE — Colour Noise Studio

> A single-file web audio application for generating, shaping, and exploring all eight colours of acoustic noise — with tremolo, dynamics compression, and a real-time spectrum visualiser.

---

## ✨ Features

| Feature | Details |
|---|---|
| **8 Noise Colours** | White · Pink · Violet · Blue · Green · Grey · Brown · Black |
| **Tremolo Engine** | Speed (0.1s–10s per cycle) · Strength (1–100%) via sine LFO |
| **Compressor** | Off · Default · Min · Max — with live dB gain-reduction metering |
| **Spectrum Analyser** | Real-time frequency bar visualiser, colour-matched per noise type |
| **Single File** | Zero dependencies, zero build steps — one `.html` file |
| **AudioWorklet** | Dedicated audio thread per noise type, no dropouts |

---

## 🔊 Noise Colour Reference

### ⬜ White Noise
**Spectrum:** Flat — equal power at every frequency  
**Character:** Bright, dense, hissy — like untuned radio static  
**Use cases:** Sleep masking · Focus sessions · Tinnitus relief · Equipment testing · Office sound masking

### 🩷 Pink Noise
**Spectrum:** −3 dB per octave (equal power per octave)  
**Character:** Warm, balanced — resembles steady rainfall or a forest stream  
**Use cases:** Deep sleep · Memory consolidation · Speaker break-in · EQ reference · Meditation

### 🟣 Violet / Purple Noise
**Spectrum:** +6 dB per octave (inverse Brownian)  
**Character:** Intensely bright, airy, sibilant — saturated with treble energy  
**Use cases:** High-frequency tinnitus masking · Audiology testing · Upper-range hearing assessment · Dithering

### 🔵 Blue Noise
**Spectrum:** +3 dB per octave (inverse pink)  
**Character:** Bright and airy, noticeably reduced bass presence  
**Use cases:** Audio & image dithering · Halftone printing · Anti-aliasing · High-frequency masking

### 🟢 Green Noise
**Spectrum:** Mid-band emphasis centred ~500 Hz — "nature's frequency"  
**Character:** Organic, calming — resembles a forest floor or coastal shoreline  
**Use cases:** Nature soundscapes · Deep relaxation · Anxiety reduction · Biophilic design

### ⬛ Grey Noise
**Spectrum:** Equal-loudness weighted (inverse Fletcher–Munson)  
**Character:** Perceptually flat — sounds uniform because it corrects for human hearing sensitivity  
**Use cases:** Psychoacoustic research · Equal-loudness assessment · Acoustic calibration · Therapeutic design

### 🟫 Brown Noise
**Spectrum:** −6 dB per octave (Brownian motion / 1/f²)  
**Character:** Rich, heavy, bass-dominated — like distant thunder or heavy rainfall  
**Use cases:** Deep focus · ADHD support · Sleep induction · Storm ambience · Anxiety regulation

### 🖤 Black Noise
**Spectrum:** Power → 0 (near-silence with sporadic soft transients)  
**Character:** The absence of sound — anechoic chamber, deep space noise floor  
**Use cases:** Mindfulness · Ultra-deep meditation · Sensory awareness training · Sleep onset

---

## 🎛️ Controls

### Tremolo
The tremolo engine uses a **sine LFO** modulating a GainNode, producing a natural amplitude oscillation:

```
gain = (1 − strength) ↔ 1.0   at   frequency = 1 / speed_seconds
```

- **Speed** — period of one full tremolo cycle in seconds (0.1s = very fast flutter, 10s = slow swell)
- **Strength** — modulation depth as a percentage of full gain swing

### Compressor Presets

| Mode | Threshold | Ratio | Attack | Release | Character |
|---|---|---|---|---|---|
| **Off** | — | — | — | — | Fully bypassed |
| **Default** | −24 dB | 4:1 | 3 ms | 250 ms | Gentle, transparent |
| **Min** | −10 dB | 2:1 | 20 ms | 500 ms | Light touch |
| **Max** | −40 dB | 20:1 | 0.1 ms | 100 ms | Hard limiting |

The **dB GR** (gain reduction) meter reads live from the Web Audio `DynamicsCompressorNode.reduction` property.

---

## 🚀 Usage

No install. No npm. No bundler.

```bash
# Option 1 — open directly
open chromatic-noise.html

# Option 2 — serve locally (avoids AudioWorklet CORS restrictions in some browsers)
npx serve .
# or
python3 -m http.server 8080
```

Then navigate to `http://localhost:8080/chromatic-noise.html`

> ⚠️ **Note:** AudioWorklet requires a secure context (`https://` or `localhost`). Opening the file directly via `file://` may work in Chrome but not all browsers. A local server is recommended.

---

## 🧠 Technical Architecture

```
AudioWorkletNode (np)       ← dedicated audio thread, no main-thread dropouts
        ↓
  GainNode (tremolo)        ← LFO-modulated amplitude
        ↓
DynamicsCompressorNode      ← optional, bypassed when mode = "off"
        ↓
  GainNode (master)         ← overall volume
        ↓
  AnalyserNode              ← feeds spectrum visualiser canvas
        ↓
  AudioContext.destination
```

Each noise colour is synthesised inside the `AudioWorklet` using dedicated algorithms:

- **White** — direct PRNG output
- **Pink** — Paul Kellet's 7-stage IIR filter on white noise
- **Brown** — integrated white noise (random walk)
- **Blue** — first-difference of white noise
- **Violet** — second-difference of white noise
- **Green** — state-variable bandpass filter (~500 Hz)
- **Grey** — IIR-approximated inverse equal-loudness weighting
- **Black** — near-zero white noise with rare stochastic transients

---

## 🌐 Browser Support

| Browser | Support |
|---|---|
| Chrome / Edge 66+ | ✅ Full |
| Firefox 76+ | ✅ Full |
| Safari 15+ | ✅ Full |
| Mobile Chrome (Android) | ✅ Full |
| Mobile Safari (iOS 15+) | ✅ Full |

---

## 📁 File Structure

```
chromatic-noise.html    ← the entire application (HTML + CSS + JS)
README.md               ← this file
```

---

## 🤝 Contributing

Pull requests welcome. Some ideas for contribution:

- [ ] Additional noise colours (Red, Orange, Velvet)
- [ ] Binaural beat layer
- [ ] Timer / sleep schedule
- [ ] Export to WAV
- [ ] Preset save/load via localStorage
- [ ] EQ panel per noise type
- [ ] iOS PWA support with background audio

---

## 📄 Licence

MIT — do whatever you like with it.

---

<p align="center">Made with the Web Audio API &nbsp;·&nbsp; Single file &nbsp;·&nbsp; Zero dependencies</p>

