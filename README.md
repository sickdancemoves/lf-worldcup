# LaFinteca World Cup Album 2026

An interactive, horizontal-swipe trading-card album for the LaFinteca World Cup 2026
collection — built in the LaFinteca brand system (lavender `#C3ABFF` + lime `#BFFE43`,
IBM Plex type, frosted glass, atmospheric grain and gradient blobs).

🔗 **Live:** https://sickdancemoves.github.io/lf-worldcup/

## What it is

A single-page album you flip through like a sticker book. Eight spreads:

| # | Spread | Contents |
|---|--------|----------|
| 1 | **Cover** | Title lockup + a 2-3-2 diamond of hero cards |
| 2 | 🇦🇷 Argentina | 6 players |
| 3 | 🇧🇷 Brasil | 9 players (inverted-pyramid grid) |
| 4 | 🇺🇦 Ukraine I | 8 players |
| 5 | 🇺🇦 Ukraine II | 9 players |
| 6 | 🌎 Rest of the World I | 5 players |
| 7 | 🌎 Rest of the World II | 6 players |
| 8 | **Back** | Edition colophon |

**43 cards · 6 squads · 12 nations.**

## Navigating

- **Arrows** ‹ › on screen, or the **← → / ↑ ↓** keys
- The **nav bar** buttons jump to any spread
- **Swipe** left/right on touch devices
- The **dots** at the bottom are clickable

## Tweaks panel

Click **✦ Tweaks** (bottom-left) to open three expressive mood controls — each one
reshapes several properties at once rather than pushing a single pixel:

- **Atmosphere** — `Clean` strips the haze/grain flat · `Balanced` (default) · `Electric` cranks every blob, grain and header haze up
- **Card vibe** — `Minimal` drops the glass + glow · `Glass` · `Holographic` (default) adds a multi-colour hover glow and stronger lift
- **Accent** — `Lavender` cools everything purple · `Dual` (default) · `Lime` makes lime the dominant accent

## Tech notes

Pure static site — open `index.html` or serve the folder; no build step.

- The grid sizes itself from each card's true `400×496` aspect so images are shown
  whole (`object-fit: contain`), never cropped. Container aspect is computed in JS
  from `data-cols` / `data-rows`.
- Atmosphere is layered with CSS pseudo-elements: a tiled grain overlay
  (`assets/grain-texture.png`, `mix-blend-mode: overlay`) plus lavender/lime radial
  gradient blobs per page.
- The tweaks panel is a React + Babel-standalone component (`tweaks-panel.jsx`) that
  maps each choice onto a `body` class (`atmos-*`, `cards-*`, `accent-*`). The default
  `cards-holo` class is baked onto `<body>` so the intended look holds even if the CDN
  scripts are blocked.

## Provenance

Recreated from the **World Cup Album v8** prototype mocked up in
[Claude Design](https://claude.ai/design). The 16 MB prototype embedded every card as
inline base64; here those are extracted to real files under `assets/cards/` (deduped by
content hash) and the 4K grain texture is downscaled to a light tiling source — same
look, a fraction of the weight.

```
index.html              the album
tweaks-panel.jsx         reusable tweaks shell (React, in-browser Babel)
assets/grain-texture.png tiled grain overlay
assets/cards/            45 player/hero card images
```
