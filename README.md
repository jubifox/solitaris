# Solitaris

**[▶ Jouer maintenant](https://jubifox.github.io/solitaris/)**

A single-file Klondike solitaire, deliberately over-juiced: every move blooms,
shakes and rains shards. Ships with a 95-piece skin economy, case opening and
an 8-player battle royale against AI climbers.

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
| Walk in the hub | Arrows / `WASD`, or click |
| Enter a building | Stand in its doorway, `Enter` |
| Open / leave the hub | `H` / `Esc` |

Build the tableau down in alternating colours, foundations up by suit.
Standard Klondike rules, draw one, unlimited redeals.

## What's in it

**Juice.** Spring-physics card movement, 3D flips, shockwave rings, particle
bursts, screen shake, brief slow-motion on foundation plays, chromatic
aberration on impact, bloom, scanlines, a custom cursor with a trail, and a
full card cascade on the win. A combo multiplier (up to ×15) escalates every
chained scoring move.

**Economy.** Two currencies: shards earned by playing, and premium gems.
**95 cosmetics** across three slots — 34 card faces, 32 sleeves, 29 tables —
in five rarity tiers. Forty-six are animated (fire, water, frost, lightning,
petals, a cyclone eye, an accretion disc, clockwork gears, aurora curtains…),
rendered as pre-baked 30-frame sprite loops so they cost one blit per card at
runtime.

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
You start facing Solitaire Hall, a few steps from a dealt table; The Arena is
battle royale, The Market is skins, The Vault holds your unopened crates, and
the Hall of Records has your run on a board beside it. Walk into a doorway and
press `Enter` to go in. `H` reopens the hub, `Esc` leaves it.

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
