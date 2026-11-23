# Ember Duel — make.fun "Make the best card game"

An original turn-based elemental card duel. You vs **Cinder, the Ash Warden**.
Both start at 30 life. Each round you play one card from your hand of five;
Cinder plays one back. Power = card value (+2 when your suit beats theirs).
The stronger card deals the difference as damage (at least 1). A **Guard**
card blocks all damage that round. Ties deal nothing. First to 0 life loses.

Suits: **Flame > Leaf > Stone > Tide > Flame** (+2 power).
Deck: values 1–9 in each suit, plus 2 Guard cards per suit (44 cards).
Cinder picks its card with a simple best-power strategy.

## How to play

```sh
node serve.ts            # serves game/ on http://localhost:8080
# open http://localhost:8080 in desktop Chrome
```

- Click a card, or press **1–5** to play it.
- **Space / Enter** — start or restart. **P** — pause. **M** — mute. **R** — restart.
- Sounds are tiny generated WebAudio beeps; the game needs no network at all.

## Files (the entry)

- `main.ts` — Node 22 program: copies `game/` and `screenshots/` to `/output`
  and writes `dossier.json` with the vendored make.fun library.
- `vendor/makefun-game.ts` — make.fun's library, copied from the kit unchanged.
- `game/index.html` — the whole game, one self-contained file (canvas, no
  libraries, no network requests).
- `screenshots/` — 4 real renders of the game's own code (1280×720):
  `1-start.jpg` title, `2-play.jpg` mid-game table, `3-win.jpg` victory,
  `4-loss.jpg` defeat.
- `shots.json` — the shot list used to take the screenshots
  (`?shot=start|play|win|loss&seed=1` stages each scene deterministically).
- `serve.ts`, `LICENSE` — from the kit.

The `best-card-game-20261122-1826-kit/` folder and `kit.tar.gz` are the
downloaded kit for reference only — they are **not** part of the entry.

## Test locally

```sh
# rebuild the hand-in bundle and check the dossier
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts
# out/ now holds game/, screenshots/ and dossier.json (makefun/dossier/v1)
node --check <(sed -n '/<script>/,/<\/script>/p' game/index.html | sed '1d;$d')  # JS syntax
```

Screenshots were taken with headless Chromium at 1280×720 from the staged
scenes and verified by eye: title panel, both hands, readable card values and
suits, life totals, win and loss screens all render correctly.

## Submit (do this yourself — Muse cannot submit for you)

Competition: `best-card-game-20261122-1826`, $50 total (1st $12, 2nd $8,
3rd $6, 4th $5, 5th $4, 6th–10th $3 each). **Deadline: 2026-11-23 13:26 WIB**
(06:26 UTC). An AI judge compares games pairwise by screenshots and a source
outline; places go by win rate. No prize is guaranteed.

1. Create a **public** GitHub repo in your own account (created after
   2026-11-22T18:26Z), OSI-approved license, and push `main.ts`,
   `vendor/`, `game/`, `screenshots/` to it.
2. On your own computer, create a make.fun account and a Solana keypair
   (the keypair file contains the private key — never paste it into chat).
3. From a **recorded** agent session on your own computer, run the kit CLI:
   `node cli/makefun.mjs bundle` then `node cli/makefun.mjs submit`
   with the repo URL and commit SHA. Handed-over (unrecorded) sessions are
   ranked but take no paid place.
4. If you place in the top 10, claim the USDC prize to your own Solana
   wallet within the claim window (an EVM `0x…` wallet cannot receive it).
