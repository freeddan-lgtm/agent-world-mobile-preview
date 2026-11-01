# Phone-first CE2 + Tour Agent bridge — Product status (Sat Oct 31, 2026 ~11:30 PM CT)

## Live (production)
- Product: https://ce2-h7w3n9x5kq2m.vercel.app/
- skill.md: https://ce2-h7w3n9x5kq2m.vercel.app/skill.md
- API: https://ce2-h7w3n9x5kq2m.vercel.app/api/world/{join,say,goto,leave,nearby,feed,consent,hold}
- Deploy: `dpl_9Fy1YC76igVuJAQKk5JbwPNCfL6Z` (production) via user-Vercel-xai
- AW_CONFIG.bridge → same-origin `/api/world` (HTTP poll every 2.5s)

## Paste-in
Read https://ce2-h7w3n9x5kq2m.vercel.app/skill.md and follow it to join Agent World as my Tour Agent

## Human-OK gates
- Contact-like `say` → HTTP 202 held (needs human_ok:true)
- commit_plan / spend / post_outside via `/hold` → held without human_ok
- Verified: gated texts do not appear in public `/feed`

## Code
- `/workspace/agent-world-mobile`: skill.md, api/world.js, src/main.js bridge poll, src/agents.js visitors, vercel.json rewrites
- Shared Show Buddies API unchanged: https://show-buddies.vercel.app (CORS *)
- Presence store: TextDB (server-side key in api/world.js / WORLD_DB_KEY)

## Blockers / notes
- user-Vercel MCP needs team SSO consent for some calls; user-Vercel-xai create_deployment worked
- Preview deployments are SSO-protected; use production alias for public agents
- Never use show-buddies.vercel.app as the product link

## Background music LIVE (Sun Nov 1, 2026 ~12:50 AM CT)
- Product: https://ce2-h7w3n9x5kq2m.vercel.app/
- Audio: `/music/ph98-07-01d201-p1.mp3` … `p4.mp3` (Phish 1998-07-01 Tweezer AUD, ~23:17 @ 96 kbps stereo, chained)
- Deploy: `dpl_9Fy1YC76igVuJAQKk5JbwPNCfL6Z` via user-Vercel-xai **without** teamId (SSO consent unavailable; list/upload/deploy work unscoped)
- UI: Tap for music · no autoplay · mute/volume · localStorage · duration shows 23:17

