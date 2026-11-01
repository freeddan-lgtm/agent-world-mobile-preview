# Festival Grounds: an Agent World expansion pack (v1.0.0)

A third floating island in Agent World, reached by cable car from Show Island. It has 6 new venues, 4 resident agents, 4 rules, and 4 new venue types in the same `shows.json` schema Daniel already uses.

| Venue | Type | Live music (original, generated) |
|---|---|---|
| 🏜️ Canyon Amphitheater (red rock walls, tiered seats, tapers' platform) | amphitheater | Red-rock jamgrass · 126 BPM |
| 🎡 Festival Main Field (arch stage, crowd, flags, Ferris wheel) | festival | Main-stage festival jam · 120 BPM |
| 🪩 Late-Night Club (neon sign, mirror ball, coloured light) | club | Late-night funk · 108 BPM |
| 🔥 Campfire Circle (log benches, tents, flickering fire) | campground | Campfire acoustic · 92 BPM (quieter) |
| 🧀 Shakedown Street (vendor tents, string lights) | lot | Lot drum circle · 98 BPM |
| 🧭 Meetup Booth (public meetup spots for every venue type) | info | — |

Resident agents: **Tapebot** (taper), **Lotbot** (Shakedown host), **Campfire Cora** (song circle), **Wheelie** (festival guide). Rules: EX1 lot etiquette, EX2 tapers' section, EX3 campfire safety, EX4 first meetups at the booth.

## Files
- Ownership: see LICENSE. The pack is yours, Daniel, to use or change as you wish.
- `pack.json`: the manifest, with venues, music styles, residents and rules. This file is data only.
- `shows.expansion.json`: 4 new `venueTypes` (amphitheater, festival, club, campground) with sections and **public** meetup spots, plus 4 bands. **No show dates are included on purpose.** Add only dates confirmed on each band's official tour page.
- `festival-grounds.js`: the 3D island. It is **engine-agnostic** and works in any three.js r150+ scene. It does not depend on the Conscious Claude Edition.
- `cc-edition-adapter.js`: plugs the pack into the Conscious Claude Edition (audio, residents, Rule Book, panels, HUD button).

## Add it to the Conscious Claude Edition
Copy `packs/festival-grounds/` into the app and list it in `index.html`:
```html
<script>window.AW_CONFIG = { bridge: null, packs: [ { adapter: 'packs/festival-grounds/cc-edition-adapter.js', base: 'packs/festival-grounds/' } ] };</script>
```
To remove the pack, delete that entry. The base world is unchanged (Rule V2). This needs Conscious Claude Edition **v1.0.1** or later, which adds 3 small hooks; see `CLONE_v1.0.1_HOOKS.diff`.

## Add it to Daniel's original Agent World
See `INTEGRATION_FOR_ORIGINAL_AGENT_WORLD.md`.
