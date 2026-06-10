# LaFinteca World Cup Album — Minigames

**Date:** 2026-06-10
**Status:** Approved

## Goal
Add a minigames experience reachable from the album cover, served at
`lafintecaworldcup.com/minigames/`, with two games built on the existing card art.

## Structure & routing
- New `minigames/index.html` — one self-contained, zero-build file.
- Three views toggled by URL hash: portal (`#`), memory (`#memory`), guess (`#guess`).
- **Relative paths only** (`minigames/` from the cover, `../assets/...`, `../` back to
  the album) so the same files work on the custom domain *and* the
  `github.io/lf-worldcup/` project URL.
- Reuses `../assets/cards/*.png` (45 players) and `../assets/card-back.png` — no copies.
- Branding matches the album: black bg, lavender `#C3ABFF` + lime `#BFFE43`, IBM Plex
  type, frosted glass, card aspect 400/496.

## Cover button
A branded pill `Play the Minigames →` placed below the cover logo in `index.html`,
linking to `minigames/` (relative). Independent of the pending new cover logo.

## Portal view
Title + two tiles (*Memory*, *Who is this player?*) + "← Back to album" link.

## Game 1 — Memory
- 20 tiles / 10 pairs; 10 random players chosen per game.
- Tiles start face-down (`card-back`); click flips. Two matching player cards stay
  face-up; non-matches flip back after ~0.8s. Input locked during evaluation.
- Already-matched / already-flipped tiles ignore clicks.
- **Count-up timer** starts on first flip, stops when all 10 pairs are matched →
  "Solved in M:SS".
- Buttons: **Play again** (reshuffle) · **Back to portal**.

## Game 2 — Who is this player?
- 5 rounds. Each round picks a random card (no repeats within a game).
- **Progressive blur reveal:** the card starts heavily blurred (~18px → reads as a
  colored silhouette) with its name banner masked, and sharpens to clear over ~6s.
  (A true cut-out silhouette isn't possible — the photos are full-bleed with
  backgrounds — so a tunable blur is the practical equivalent.)
- On the left, 4 name buttons: 1 correct + 3 random distinct distractors, shuffled.
- **Speed/clarity scoring:** a "Worth" meter counts down 5 → 1 as the blur clears.
  Select a name → **Lock in** → awards the current Worth if correct (0 if wrong),
  reveals the face + name, colors the options. **Next** advances.
- Scoring tiers (max 25 over 5 rounds): ≥21 & all correct "Legendary eye", ≥18
  "Sharp eye", ≥12 "Solid", ≥7 "Not bad", else "Keep practicing".
- After round 5: **results board** showing the 5 cards — correct in color, wrong in
  grayscale (B&W) — plus total points and correct count. Buttons: **Play again** ·
  **Back to portal**.

## Data
A JS array `PLAYERS = [{file, name, country}, …]` for the 45 cards. Names read from the
printed card banners and proofed by the user before launch.

## Decisions
- 4 options per guessing question.
- Memory grid: 4×5 on mobile, 5×4 on desktop (responsive).
- Single-file hash-routed views (not separate pages) — shared CSS/data in one place,
  still deep-linkable.

## Out of scope
- Leaderboards / persistence / accounts.
- Sound.
- Difficulty levels.
