# Clue Deduction Engine

Single-file static web app (`index.html`) — real-time deduction tracker for the Clue board game. No build tools, no dependencies, no server.

## Architecture

Everything lives in `index.html`: HTML structure, embedded `<style>`, and embedded `<script>`. This is intentional — keeps deployment trivial (GitHub Pages, Vercel, or just open the file) and works fully offline after first font load.

## Edition System

Supports two editions toggled via a switch in the header:
- **Simpsons** — Homer/Marge/Bart/Lisa/Smithers/Krusty, themed weapons and Springfield rooms
- **Classic** — Scarlet/Mustard/White/Green/Peacock/Plum, traditional weapons and rooms

Edition data is stored in the `EDITIONS` object. `loadEdition(name)` swaps the active `SUS`, `WPN`, `RMS`, `SHORTCUTS`, `DIST`, `BOARD_POS` arrays. Switching editions resets the game.

## Key Data Structures

- `EDITIONS` — contains all card names, distances, board layout, and secret passages per edition
- `SUS`, `WPN`, `RMS` — current edition's suspects/weapons/rooms (set by `loadEdition`)
- `ALL` — combined array of all current cards; `CAT` — maps card name to category (`s`/`w`/`r`)
- `DIST` — 9x9 room distance matrix (step counts, secret passage = 1)
- `BOARD_POS` — `[col, row, colSpan, rowSpan]` for the 3x4 CSS grid board
- `G` — game state object (players, knowledge matrix, suggestions, solution, turns, etc.)

## Core Engine

The constraint propagation engine (`propagate()`) runs after every logged suggestion:
1. Card held by one player → ruled out for all others
2. Card ruled out for ALL players → it's the solution
3. Soft constraints ("player has at least one of [A,B,C]") → resolves when narrowed to one
4. Known solution in a category → remaining cards must be distributed among players

## Tabs

- **Setup** — player count, names, characters, starting rooms, hand selection
- **Matrix** — knowledge grid (players x cards) with auto-propagated states
- **Log Suggestion** — record suggestions/responses + show advisor (minimizes info leakage)
- **Board** — visual room map with dice roll reachability and player tokens
- **Analysis** — probability heatmap, valid combo count, optimal next suggestion

## Deployment

GitHub Pages: Settings > Pages > Deploy from branch > main > / (root)
Vercel: `vercel` CLI or link the GitHub repo

## Conventions

- All UI rendering is done via innerHTML string building (no framework)
- Card keys use `ck(name)` → lowercase, spaces to hyphens
- Player colors: `PCOLS` array, indexed by player position
- Voice input uses Web Speech API with fuzzy matching (`fuzzyFind`)
