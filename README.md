# Solitaris

**[▶ Jouer maintenant](https://jubifox.github.io/solitaris/)**

A single-file Klondike solitaire, deliberately over-juiced: every move blooms,
shakes and rains shards. Around it sits a walkable hub with **ten more games**
in it, a 99-piece skin economy, case opening, an 8-player battle royale against
AI climbers, and a season that turns over every four weeks.

One HTML file. No build step, no dependencies, no server — open it and play.

## Playing

| Action | How |
| --- | --- |
| Move a card | Drag it, or **tap** it to fling it to the best legal spot |
| Draw | Click the deck (`Space` / `S`) |
| Undo | `Z` |
| New deal | `N` |
| Auto-resolve | `A`, once every tableau card is face up |
| Mute | `M` |
| Walk in the hub | Arrows / `WASD`, or click where you want to go |
| Enter a building | Click it, or stand in its doorway and press `Enter` |
| Open / leave the hub | `H` / `Esc` |
| Leave a hub game | `Esc` (again to go back outside) |

Build the tableau down in alternating colours, foundations up by suit.
Standard Klondike rules, draw one, unlimited redeals.

## What's in it

**Juice.** Spring-physics card movement, 3D flips, shockwave rings, particle
bursts, screen shake, brief slow-motion on foundation plays, chromatic
aberration on impact, bloom, scanlines, a custom cursor with a trail, and a
full card cascade on the win. A combo multiplier (up to ×15) escalates every
chained scoring move.

**Economy.** Two currencies: shards earned by playing, and premium gems.
**99 cosmetics** across three slots — 35 card faces, 33 sleeves, 31 tables —
in five rarity tiers, four of them season-exclusive. Forty-eight are animated
(fire, water, frost, lightning, petals, a cyclone eye, an accretion disc,
clockwork gears, aurora curtains…), rendered as pre-baked 30-frame sprite loops
so they cost one blit per card at runtime.

**Cases.** Two crates with published odds, openable ×1, ×5 or ×10. Every open
starts with the crate itself — a shaded box turning on its axis, winding up
through three latch clacks before the lid flies off. Single opens then run a
64-tile carousel whose fillers are rolled from that crate's own odds, with
rarity glowing behind each tile, ticks pitched to the strip's speed and a
damped rock-back onto the marker. Multi-opens flip a grid of tiles one at a
time. Either way the pull is shown turning under a rarity beam. Duplicates
convert to shards automatically.

**Hub.** The game opens here: a plaza you walk a character around — arrows or
WASD, or click where you want to go — with a doorway for each part of the game.
You start facing Solitaire Hall, a few steps from a dealt table. The Arena is
battle royale, The Market is skins, The Vault holds your unopened crates, and
the Hall of Records has your run on a board beside it. Three more doorways lead
to the games below. Walk into a doorway and press `Enter` to go in — or just
click the building and your character walks over and steps through. `H` reopens
the hub, `Esc` leaves it.

**Ten more games**, in three venues off the plaza. They all share your wallet
and your wardrobe: the card games deal with whichever deck and sleeve you have
equipped, every venue sits on your table felt, and shards won anywhere spend in
the Market. Each keeps its own personal best.

*The Card Room*

- **Freecell** — eight columns, four cells. Click a card, then click where it
  goes; runs move together when you have the free cells to carry them, and
  anything that can never be needed again goes home on its own. `A` sends
  everything safe home at once.
- **Pyramid** — twenty-eight cards taken away in pairs that add to thirteen.
  Kings go alone. Stock, waste and two redeals.
- **Blackjack** — the one game played with your own shards. Stake 25 to 250,
  hit, stand or double; dealer stands on 17, blackjack pays 3:2.
- **Texas Hold'em** — a 120-shard buy-in for a seat against three opponents,
  1000 chips each, blinds rising every six hands. Real hand evaluation and
  proper side pots, so a short stack only ever wins what it covered.

*The Arcade*

- **Minesweeper** — 16×16, forty mines. The field is laid after your first
  click, so it is never a mine and never a bare number. Right-click or `F`
  flags; clicking a satisfied number opens round it.
- **Slide Puzzle** — fifteen tiles and a gap, shuffled by walking the gap so
  the board is always solvable. Click or arrow keys.
- **Sudoku** — generated fresh each time and pared back only as far as a single
  answer allows. Wrong digits are refused rather than left to rot.

*The Coliseum*

- **Light Cycles** — a 62×40 grid against a rider that counts the room left
  through each opening before it turns. Speeds up as you go.
- **Dice Royale** — thirteen boxes, three rolls a turn, against a rival filling
  in its own sheet beside yours. Hold dice by clicking them or with `1`–`5`.
- **Prism Break** — ninety seconds of match-three, cascades multiplying as they
  chain, board reshuffled rather than left dead.

**Seasons.** Solitaire is here all year; everything else rotates on a 28-day
season. The current season puts three of the ten games forward and pays double
on them, and puts one skin in the Market that leaves again when the season
turns — though anything you have bought stays yours. The hub names the season
and its picks, and the Hall of Records counts how many venues you have beaten.

**Battle royale.** You plus seven AI climbers on the same seeded deal. The
lowest score is cut every 20 seconds until one is left. Placement pays out in
shards, gems and free cases.

Progress lives in `localStorage`, so it is per-browser and never leaves the
machine.

## Performance

Everything renders to canvas through a cached pipeline: card faces are baked
to sprites once per skin change instead of being redrawn per frame, the table
background is drawn at half resolution and refreshed on an interval derived
from its own measured cost, and bloom recomputes at 60 Hz even when the game
runs at 120.

Because the table is refreshed on an interval rather than per frame, it is
double-buffered and crossfaded between refreshes, so an animated table reads as
a continuous pan instead of a slideshow. Tables that do not animate are drawn
once and left alone.

The frame time is sampled continuously and the effect tier steps itself down
(Max → Calm → Potato) if the machine can't keep up, adjusting particle caps,
sprite resolution, bloom and post-processing. The **FX** button overrides it;
current fps and tier are shown under the shard counter.

`prefers-reduced-motion` is honoured — it starts in the calmest tier.

## Credits

27 of the cosmetics are canvas ports of designs from
[solitaire-deluxe](https://github.com/jubifox/solitaire-deluxe) (MIT, same
author), which builds its skins in CSS. They were reimplemented as canvas
renderers rather than copied.

Typefaces are Cinzel, Oswald and IBM Plex Mono, loaded from Google Fonts.

## Layout

    index.html    the whole game: markup, styles, engine, catalogue

Deliberately one file. It is meant to survive being emailed, dropped on a USB
stick, or opened straight off a network share.

## Licence

MIT
