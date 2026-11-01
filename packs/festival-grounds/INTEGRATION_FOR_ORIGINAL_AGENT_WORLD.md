# Adding Festival Grounds to the original Agent World (Show Buddies)

The original app is a three.js r160 scene. Its built bundle (`app.js`) exposes `window.AW3D`, but the scene object isn't exposed, so the steps below go into **the source** before it is bundled.

## 1. The island (about 5 lines)
Where the scene is set up (next to the code that builds Show Island and its `VENUES`):
```js
import { installFestivalGrounds } from './packs/festival-grounds/festival-grounds.js';
const fgPack = await (await fetch('/packs/festival-grounds/pack.json')).json();
// Show Island centre in the original is about (0, 0, -122) with radius ~25. Put the pack past the RM/Goose gap:
const a = 2.58, at = new THREE.Vector3(Math.sin(a) * 93, 0, -122 + Math.cos(a) * 93);
const from = new THREE.Vector3(Math.sin(a) * 22.5, 0, -122 + Math.cos(a) * 22.5);
const fg = installFestivalGrounds({ THREE, scene, pack: fgPack, at, connectFrom: from /*, makeLabel: (html) => yourCSS2DLabel(html) */ });
```
In the render loop, add `fg.update(dt, t);`. Without an audio engine, the crowds still bob gently.

For clicks, add `fg.pickables` to the list of objects you raycast against. A hit carries `userData.pick = { kind: 'pack-venue', pack: 'festival-grounds', id }`.

If you leave out `makeLabel`, the pack draws its own sprite labels. To match your HUD style, pass a function that returns your CSS2D label.

## 2. Venue data
Merge `shows.expansion.json` into `shows.json`:
- Add its four `venueTypes` entries (amphitheater, festival, club, campground) to your existing `venueTypes`.
- Append the `bands`, and add show dates only from official tour pages.

`sb.js` already reads `venueType` for sections and meetup spots, so new shows pick these up automatically. In the original, new bands appear on the **🎸 Other bands** stage. To give them their own stage, map `venueType` → pack venue id (for example `amphitheater` → `fg-amph`).

## 3. Optional: music
Take `src/audio.js` from the Conscious Claude Edition:
```js
const audio = new AudioEngine(); for (const v of fg.venues) if (v.venue.music) { STYLES[v.id] = v.venue.music; audio.register(v.id, v.pos); }
// on a user tap: audio.enable();   every frame: audio.update(camera); fg.update(dt, t, id => audio.stages.get(id)?.energy);
```
Lights and crowds then follow the music.

## 4. Removing it
Call `fg.dispose()` and drop the `venueTypes`/`bands` you added. Nothing else in the original changes.

*Untested against the original source.* That source wasn't available to me, so I wrote these steps from the public bundle's structure. The pack module itself is tested in the Conscious Claude Edition.
