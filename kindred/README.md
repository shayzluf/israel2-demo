# KINDRED — Daily Match (mockup)

> *Find the humans you didn't know were yours.*

Single-file interactive HTML mockup of the Daily Match — the 90-second ritual that is KINDRED at MVP. Built to feel like the most beautiful thing on the user's phone today.

---

## Run it

```bash
open index.html
```

Or any static server (`python3 -m http.server 8000`, `npx serve`, etc.). The page is self-contained — no build step, no dependencies.

For the best feel: **viewport size ≈ 430 × 932** (iPhone-shaped). On desktop the stage renders as a phone frame; on mobile it's full-bleed.

## Controls

- **Tap to begin** on the open screen → Web Audio initializes (browser requires a user gesture). The Discovery Chord plays.
- **Tap a reaction** (`moves me / stops me / unsettles me / cold`) on each prompt. The 7th prompt is a diptych — tap a side to choose.
- The Hold scene plays automatically (~2.2s) before Drop 1.
- **Tap CONTINUE / SEE YOUR MATCH** at the bottom of Drop 1 / Drop 2.
- **Show your Constellation** on the Match Card simulates the share moment.
- The replay (↻) icon resets to the open scene.
- **Spacebar / Enter** advances scenes for desktop demo.
- **R** resets.
- **Audio toggle** in the top-right (gold = on).

## What's in here

```
gameoflife/
├── index.html          single-file mockup (1.5K LOC, vanilla JS)
├── prompts/            9 Imagen-4-generated curated images (.png, ~13 MB total)
├── _gen.py             prompt generator script (Imagen 4 batch, parallel)
├── _retry02.py         single-prompt retry (used to clear a safety filter)
├── .env                GEMINI_API_KEY (gitignored — yours)
└── README.md           this file
```

## What's working

- **Lattice background** — procedural SVG hex grid, radial fade, gentle breathing pulse.
- **Open scene** — countdown to 5 AM (live ticking), breathing orb with rotating ring, ambient chord on tap.
- **7-prompt cycle** — Imagen-generated visuals, slow Ken Burns drift, glassmorphic 4-emoji reaction palette, progress dots.
- **Diptych choice** prompt for the 7th prompt.
- **Hold scene** — Canvas particle convergence, ~80 dots flowing inward to form your Constellation.
- **Drop 1** — kinetic count-up to 1,234,902 humans, twin reveal pill.
- **Drop 2** — six-country bar viz of the cross-cultural surprise, italic Bridge moment.
- **Match Card** — the hero. Two procedural Constellations (gold = you, teal = your twin), kinetic 91% count-up, italic Bridge moment in violet, KINDRED wordmark, share bar.
- **Web Audio Discovery Chord** — Cmaj7 sawtooth pad through a low-pass sweep + sine bell layer + synthetic 3.2s reverb impulse. No samples.
- **Procedural Constellations** — deterministic seeded RNG, Poisson-disc-ish placement, mutual k=2 nearest-neighbor connections, soft anchor halos, gentle staggered SVG twinkle animations.
- **Audio toggle** in the corner.

## Design rationale (the 3 micro-decisions worth flagging)

1. **Refraction violet (#9D6BFF) is used exactly once.** The Bridge moment in italic Instrument Serif. Used in only one place across the entire mockup — the alignment % gradient ends in teal, the Constellation lines never use it, the reaction palette doesn't reach for it. Scarcity is the point: when violet appears, your eye lands on it and you read what it says.

2. **The Discovery Chord is not Cmaj — it's Cmaj7.** The added 7th (B) is what gives it the *ache.* A plain major chord would feel triumphal; Cmaj7 feels found. The bell layer (C5, E5, G5, B5) enters 0.9–1.4s after the pad, with staggered onsets, so the chord *blooms* rather than starts.

3. **Constellations are connected by mutual k=2 nearest-neighbor lines, not Delaunay.** Delaunay triangulation produces a structurally complete graph that looks like a net. Mutual k=2 produces something sparser, more selective, more *constellation-like* — patterns you read into rather than patterns the algorithm imposes.

## What's not here yet (next pass)

- The Constellation Evolution Drop animation (a new star appearing in your Constellation between Hold and Drop 1).
- Subtle haptic feedback (`navigator.vibrate`) on reactions for mobile.
- Match Card share rendering as a real PNG export (right now, share is a "saved to your story" toast).
- Real-time Pulse Card showing votes coming in worldwide on the open scene.
- Localization (Hebrew, Arabic, Portuguese strings + RTL).
- The Drop 2 visualization currently uses a horizontal bar chart — the brief allows a stronger one-fact visualization (a sunset color-strip with reaction dots, perhaps).

## Generated with

- **Google Imagen 4** (`imagen-4.0-generate-001`) for the 9 prompts. Slot 02 (child laughing) tripped the safety filter on the first pass — retried with a "from behind, no face" reframe.
- **Web Audio API** for all sound (no audio files in the bundle).
- **Vanilla CSS / SVG / Canvas** — no React, no Tailwind, no third-party libraries. Total page weight under 14 MB (mostly Imagen imagery; HTML is 52 KB).

## The "What's that?" test

A friend sees your screenshot of the Match Card. They ask "what's that?" and you say:

> *"It's like Wordle but it tells you who you're secretly like across the world."*

If the friend has to ask "is it civic? political?" the design failed. Right now: it doesn't.
