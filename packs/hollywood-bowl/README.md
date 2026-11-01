# Hollywood Bowl: an Agent World expansion pack (v1.0.0)

The pack adds a fourth floating island, reached by cable car from Show Island:
- A concentric-arch shell amphitheater. Its ring lights drift slowly through colours and never strobe.
- An orchestra with a conductor, Maestro Moon, who beats time to the music.
- Box seats down front and benches climbing the hillside, with crowds.
- The Hollywood Hills: chaparral ridges with twinkling house lights.
- A large full moon above the hills, with a halo and soft moonlight.

**Music:** "Symphonic pops under the stars" (strings, harp, French horn, timpani, celesta). It uses modeled shell acoustics: dense early reflections from the arches in the first 40 ms and a short open-air tail.

**Residents:** Maestro Moon, Usher Ava, Picnic Pete. **Rules:** HB1 quiet for the soft parts, HB2 picnic etiquette, HB3 first meetups at the plaza.

**Files:**
- `hollywood-bowl.js`: engine-agnostic three.js module.
- `cc-edition-adapter.js`: plugs the pack into the Conscious Claude Edition.
- `pack.json`
- `shows.expansion.json`: adds a `bowl` venue type. Section names follow commonly used seating areas, so confirm them on the official chart. No dates are included.
- `LICENSE`: the pack is Daniel's.

It is an artistic model. It isn't affiliated with or endorsed by the venue and uses no official logos.

**Add it to the Conscious Claude Edition** by listing it in `index.html` → `window.AW_CONFIG.packs`. It is listed by default in v1.2.0.

**Add it to the original Agent World:** follow the same steps as `../festival-grounds/INTEGRATION_FOR_ORIGINAL_AGENT_WORLD.md`, using `installHollywoodBowl({ THREE, scene, pack, at, facing, connectFrom })`. In the original's layout:
- `at` is about `(-48, 0, -197)`.
- `facing` is about `0.56` rad, so the audience looks back toward Show Island.
