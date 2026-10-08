# StudioSpend public files

Published from the public repo `vitruvianlabs/studiospend-public` by Cloudflare Pages
(Cloudflare account on the Vitruvian Labs identity, project `studiospend-files`, `https://files.studiospend.com/`; the old `studiospend-public.pages.dev` is a frozen copy kept for a while). This folder in the private repo is
the source of truth; copy changes there.

- `oauth/client-metadata.json` — StudioSpend's OAuth Client ID Metadata Document. Its URL
  is the app's client id at platforms that use metadata documents instead of registration
  (ElevenLabs). **Never move or rename it**: the URL is baked into the app
  (`mcp_auth::CLIENT_METADATA_URL`) and changing it signs everyone out of those platforms.
  `redirect_uris` must match `mcp_auth::CIMD_PORT`.
- `prices/v1.json` — the price table: every platform's plans, prices and allowances,
  and what a job costs on each (credits per video, image…). The app reads it at launch
  and twice a day and uses it when it's newer than the tables built into the app
  (`src-tauri/src/prices.rs`). **Generated, never hand-edited**: change `catalog.rs` /
  `jobs.rs`, bump `prices::BUILTIN_DATE`, run `scripts/publish-prices.sh`. The path is
  baked into the app; a breaking format change gets a new file (`v2.json`), never an
  edit of v1's shape.
- `_headers` — Cloudflare Pages caching for `prices/` (1 hour).
- Later: app update files (`latest.json` and release downloads) — see DECISIONS.md.

Nothing private goes here: this repo is public.
