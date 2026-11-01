# Moon Palace Cancún: an Agent World expansion pack (v1.0.0)

A beach-resort island for the Phish · Riviera Maya run, built by Keystone Claude (Claude Opus 5.5) for Smarth Vader and Daniel. It's owned by Daniel (see `LICENSE`).

## What's in it
- **A beach stage** with its back to the sea. It has a white sail roof, an LED wall, line arrays, moving beams and a four-piece band.
- **Sand sections** that match Show Buddies: *Beach pit / front*, *Beach middle* and *Back by soundboard*, plus *Pool & lobby* and a *Meet on Messenger 💬* kiosk. A Riviera Maya fan is seated in the section they posted.
- **The resort**: terraced hotel blocks with lit windows, a lobby palapa, a pool, palms, palapas with loungers, and tiki torches.
- **Delay towers and a soundboard tent.** Their positions come from Keystone Claude's layout search (`src/architect.js` in the Claude Edition). There is also a coverage heat map you can show on the sand.
- **A zip line** from Show Island. In the Claude Edition, agents ride it.
- **The moon for the show night.** Phase is a mean-motion estimate (about ±0.5 day). For N3 (Fri Jan 29, 2027) it gives a last-quarter moon, about 50% lit, rising roughly 00:15–01:12 local, after the show. It is drawn low over the sea.
- Two residents (Lifeguard Luz, Host Mateo) and Rule Book chapter MP (ocean after dark; water, shade and sunscreen; first meetups at Pool & lobby).

## Use it in any three.js world
```js
import { installMoonPalace, moonPhase } from './moon-palace-cancun.js';
const pack = await (await fetch('pack.json')).json();
const mp = installMoonPalace({ THREE, scene, pack, at: new THREE.Vector3(100, 0, -110), facing: 0, connectFrom: null, makeLabel: null });
// every frame:
mp.update(dt, t, id => energy /* {level, low, mid, high, bpm, beat} or undefined */, 'dusk' /* 'day'|'dusk'|'night' */, camera);
mp.applyDesign({ towers: [{ x: -8, z: 12 }, { x: 8, z: 12 }], foh: { x: 0, z: 18 } }); // venue-local metres
```
Venue-local axes: the stage is at z = −14 facing +z, and house right is +x. `mp.seat(section, i)` returns a seat position for the i-th fan in a section. `mp.spots` has named world positions (pit, middle, back, pool, lobby, messenger, station).

## Honest notes
- This is an artistic model of a beach-resort show. It is not a survey of the real resort, and it is not affiliated with the resort or with any band.
- Sound coverage and the delay-tower layout are **modeled** (inverse-square, cardioid speakers, delay timing, straight sightlines). They are not measured at the real venue.
- No show dates are hard-coded except the default moon night. Dates come from Show Buddies.
