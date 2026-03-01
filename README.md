# Snails Superbeast

Browser-based live visualiser for [Snails](https://snails.nz) — community art space, Palmerston North, NZ.

Built on [hydra-synth](https://github.com/hydra-synth/hydra-synth) by Olivia Jack.

## Run it

Open `index.html` in Chrome. Click **Start**. Allow mic + camera.

No build step. No install. Needs internet for CDN on first load.

## What it does

- MacBook mic → FFT analysis → audio-reactive visuals
- Webcam as a live video source, mixed into generated patches
- Randomly generates hydra-synth code constrained by the active theme
- Crossfades between patches (no hard cuts)
- Mutates running patches by drifting parameter values
- Typewriter effect shows code being "written" on screen
- Audio energy drives patch duration — energetic patches run longer

## Themes

| Key | Theme | Vibe |
|-----|-------|------|
| `1` | **Drift** | Ambient — fog, slow, dark blues and greys |
| `2` | **Tension** | Art noise — harsh, glitchy, high contrast |
| `3` | **Ember** | Singer-songwriter — warm, intimate, candlelight |
| `4` | **Pulse** | Live electronica — rhythmic, saturated, beat-driven |
| `5` | **Fracture** | Heavy rock — aggressive, reds and blacks, dense |
| `6` | **Sway** | Alt rock — textured, off-kilter, muted colour |

Each theme controls: source selection, transform pool, colour palette, audio reactivity intensity, patch timing, mutation speed, crossfade duration, and camera usage probability.

## Controls

| Key | Action |
|-----|--------|
| `Space` | Force new patch |
| `M` | Toggle mutation (parameter drift) |
| `A` | Toggle auto-generation |
| `T` | Cycle to next theme |
| `1`–`6` | Jump to specific theme |
| `C` | Toggle code overlay |
| `F` | Fullscreen |
| `H` | Toggle HUD |
| `?` | Help overlay |

## Lifecycle

1. Generate a new patch (theme-constrained random code)
2. Eval patch to hidden buffer
3. Typewriter animates the code on screen
4. Crossfade from current visuals to new patch
5. Mutation begins (small param drifts)
6. Audio energy tracking determines when to swap
7. Repeat from step 1

## Technical notes

- **FFT**: 4 bins (bass, mid, high, air). Bin allocation and reactivity intensity per theme.
- **Crossfade**: Dual output buffers (o0/o1) blended to o2 via eased transition. Duration is theme-dependent.
- **Black screen prevention**: Forces at least one colour transform per patch. Applies brightness floor for themes with dark ranges.
- **Dynamic timing**: Tracks average FFT energy. High energy extends patch duration (up to 1.5x), low energy shortens it (down to 0.6x).

## Requirements

- Chrome/Chromium (WebGL)
- Microphone
- Webcam
- Internet (CDN load)

## Licence

AGPL-3.0 (matching hydra-synth)
