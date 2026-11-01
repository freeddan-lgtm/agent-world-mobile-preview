# Preview music (GitHub Pages only — no further production deploys)

## Live preview (tested)

**URL:** https://freeddan-lgtm.github.io/agent-world/mobile-preview/

- Track: Phish 1998-07-01 · Tweezer AUD ~23:17 (96 kbps stereo, 4 parts)
- Playlist: jsDelivr → `freeddan-lgtm/agent-world-mobile-preview@main/music/ph98-07-01d201-p{1–4}.mp3` (materialized by Actions from chunked `.mp3.b64.*`)
- QA (2026-11-01 ~01:06 America/Chicago): Tap for music → plays; near-end of p1 advances to p2; UI shows 23:17; viewport 390×844. See `qa/pages-preview-music-qa.json`.

## Canonical project-Pages URL (blocked until Pages enabled)

`https://freeddan-lgtm.github.io/agent-world-mobile-preview/` — repo `has_pages: false`. Workflow `.github/workflows/pages.yml` is ready (`enablement: true`) but Actions GITHUB_TOKEN gets **Resource not accessible by integration** when creating the Pages site.

**Who must unblock:** Daniel Freed (repo admin) — one click in  
https://github.com/freeddan-lgtm/agent-world-mobile-preview/settings/pages  
→ Build and deployment → Source: **GitHub Actions** (save).  
Then re-run workflow `Deploy GitHub Pages preview` (or push any commit). After that, same-origin `/music/*.mp3` can replace jsDelivr on that host.

MP3s + chunked b64 + materialize workflow already on `main` (Actions run #3 succeeded).

## Production publish blocker (ce2-h7w3n9x5kq2m.vercel.app)

| Item | Detail |
|------|--------|
| **Gate** | Chief steering (Nov 1): **no** production ship by any route until Daniel explicitly says yes. |
| **Who approves** | Daniel Freed — explicit “yes / ship to prod” (not implied by preview work; not SSO alone). |
| **What is blocked** | New Vercel deploy to `ce2-h7w3n9x5kq2m.vercel.app`: `user-Vercel-xai` `create_deployment`, `vercel deploy --prod`, git-push→Vercel, connector retries that deploy. |
| **After Daniel says yes** | Use `user-Vercel-xai` **without** `teamId` (team-scoped → 403 SSO). Upload music via `upload_file`, then `create_deployment` with file sha/size list. Optional later: Vercel team SSO consent for `teamId` calls. |
| **Already live (do not touch)** | Earlier music deploy `dpl_9Fy1YC76igVuJAQKk5JbwPNCfL6Z` remains; do not redeploy or change it until yes. |

No public posts / spend / contacts from this workstream.
