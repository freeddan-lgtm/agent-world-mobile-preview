# Preview music (GitHub Pages only)

Full ~23:17 Phish 1998-07-01 Tweezer AUD for https://freeddan-lgtm.github.io/agent-world-mobile-preview/

## How audio lands on Pages

GitHub Contents API / MCP rejects binary and large single files. Pipeline:

1. Encode each 96 kbps MP3 part as base64 ASCII.
2. Split each `.mp3.b64` into ~1.4 MB chunks: `music/ph98-07-01d201-p{N}.mp3.b64.{01..}`
3. Push chunks via `create_or_update_file` (one commit each).
4. Workflow `.github/workflows/materialize-music.yml` concatenates sorted chunks, `base64 -d` → `music/ph98-07-01d201-p{N}.mp3`, commits the MP3s.
5. Pages serves the MP3s with CORS `*` and `Accept-Ranges: bytes` (see `_headers` / Pages defaults).

Playlist in `src/main.js`: `MUSIC_PARTS = [p1,p2,p3,p4]`, chained on `ended`. UI shows ~23:17. No autoplay — Tap for music.

## Production gate (do not ship until Daniel says yes)

Production URL `https://ce2-h7w3n9x5kq2m.vercel.app/` already has music from an earlier deploy (`dpl_9Fy1YC76igVuJAQKk5JbwPNCfL6Z`). **Chief steering: no further production publishes by any route** until Daniel explicitly approves.

### Exact blocker for a *new* production publish

| Item | Detail |
|------|--------|
| **Who must approve** | Daniel Freed (explicit "yes" / ship-to-prod). Chief of Staff gate — not SSO alone. |
| **What approval means** | Permission to run a new Vercel deployment that changes live `ce2-h7w3n9x5kq2m.vercel.app`. |
| **After approval** | Use `user-Vercel-xai` `create_deployment` **without** `teamId` (team-scoped calls → 403 SSO). Upload music parts via `upload_file` then deploy with file sha/size list. Alternative paths (git-push→Vercel, CLI, connector retries) are also blocked until the same Daniel yes. |
| **Optional later** | Vercel team SSO consent would unlock `teamId`-scoped connector calls; not required for file deploy without teamId. |
| **Not required for preview** | GH Pages preview does not need Vercel or Daniel prod approval. |

Do **not** git-push-trigger Vercel, run `vercel deploy --prod`, or retry deploy connectors until Daniel says yes.
