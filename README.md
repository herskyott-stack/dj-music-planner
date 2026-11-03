# Beatmaster DJ — Music Planner & Event Questionnaire v2

Successor to the standalone **Vibe Planner** Lovable app (project 34c647f3-f508-4727-b3b1-6318023810f6, Lovable-only, no GitHub — so it could not be edited in code).

## What v2 is
A single self-contained `index.html` (no build, no backend, no login wall) that a client opens from a link and completes in ~10–15 min:

1. **Your Event** — type, names, date, venue, guests, package, ceremony/rain plan
2. **People & MC** — name pronunciations, grand-entrance order, speeches, MC style, announcements, traditions, sensitive notes
3. **Special Moments** — each moment (ceremony, entrances, first dance, parent dances, cake, bouquet, garter, last dance…) gets its own song/artist/version-link/notes + popular picks + "Surprise us" / "Skipping"
4. **Song Lists** — Must-Play / Play If You Can / Do Not Play with counts, dance-time estimate, must-play cap warning, smart bulk paste (Artist - Song / Song by Artist / numbered, deduped), cross-list conflict detection, playlist links (Spotify/Apple/YouTube)
5. **Your Vibe** — genres tap-cycled Love/Never, eras, clean-only, guest-request policy, energy 1–5, cocktail/dinner vibe, slow sets, volume limits
6. **Timeline** — editable rows + one-tap classic wedding timeline template
7. **Logistics** — load-in, setup-by time, day-of contact, coordinator, photo/video, power, parking, add-ons, final notes, 14-day deadline acknowledgement
8. **Review & Send** — completeness check (missing essentials, conflicts) + auto-built DJ run sheet: Copy / Copy+Email to Jake / Download .txt / Print-PDF

Answers auto-save to the client's browser (localStorage) as they type — nothing uploads until they send the run sheet.

## Verified
- JS syntax checked (node --check)
- Unit-style tests in node: bulk-paste parser (parsing + dedupe), play-vs-do-not-play conflict detection, run-sheet generation (incl. correct date rendering), missing-essentials logic — all pass
- All 8 sections render without errors (node DOM stub)

## To go live (1 tap for Jake)
GitHub repo: `herskyott-stack/dj-music-planner` (index.html pushed, commit sha f5d3c20).
Enable GitHub Pages: repo Settings → Pages → Deploy from branch `main` / root.
Live URL will be https://herskyott-stack.github.io/dj-music-planner/
(Pages API enable returned 403 — token lacks that scope, same as the Embroidery Preview.)

## Later wiring options
- Point a beatmasterdj.ca link (e.g. /planner) at it, or drop the file into the beatmasterdj repo `public/` folder.
- Data model mirrors the existing Vibe Planner sync shape (music / notes / playlists / timeline / addons) so it can POST into `sync-planner-data` later if Jake wants submissions saved to Supabase instead of emailed run sheets.

## v3 (2026-11-03) — "same again, better"
- **Real song search** (Apple Music / iTunes catalogue, no API key): type → results with artwork + exact versions + **30-second previews** → one tap adds to the current list. Also embedded per special moment. Manual add + bulk paste remain as fallbacks; per-box result caches so parallel moment searches can't cross-add.
- **Reorder** any song list with ↑ / ↓.
- **Timeline phases** per row (Pre-Ceremony → Late Night), template carries phases, run sheet prints them.
- **Plan backup / restore** (.json download + file restore) so couples can move devices; v3 auto-migrates v2 saves from the same browser.
- **Share sheet** (Web Share API, copy fallback) + **"Your night in one sentence"** summary in Review.
- Hero now carries Jake's real dance-floor photo from beatmasterdj.ca (hides itself if the asset moves).
- Verified: node logic tests (render all sections/boards, phases, reorder, summary, run sheet) + live iTunes endpoint test + live surface byte-identical to source.
