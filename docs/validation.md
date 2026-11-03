# Northreach IV 4.1 verification — 2026-11-03

- 29 model tests passed, including humanoid bone aliases, clip roles, safe archive
  paths, root-motion locking and multi-mesh bone sharing/inverse-bind retention.
- Nine browser cases passed together: GLB replacement/export/save/reload/reset;
  a RAR above 32 MiB with a rigged multi-mesh FBX; bad-file recovery; menu/movement/
  jump/pause/checkpoint/map; settings/rebinding persistence; mobile layout/input;
  extracted production startup; and useful missing-script/stylesheet diagnostics.
- The multi-mesh fixture exposed duplicate FBX bone hierarchies. Matching rest
  bones are now shared, their canonical parent chains reconnected and animation
  targets uniquely named. The 20-bone, ten-mesh fixture then imported and played.
- The live preview also passed the three character browser cases. A final native
  file-URL test opened it after High world shadows were enabled and exercised Run
  without shader or rendering errors. Preview materials are independent of world
  cascade defines.
- After final resource cleanup changes, actual Firefox 140.15.0 file-URL testing
  imported a 35,331,784-byte RAR containing FBX plus a PNG texture. Its worker and
  WASM decoder ran offline, applied the player and saved a portable GLB in browser
  storage. Reset restored the normal player without touching journey progression.
- The complete HTML was copied alone into an empty folder with spaces and passed
  native file-URL startup, CSS/WebGL/assets, movement, loot, map, waypoint and High
  rendering checks. No HTTP/HTTPS runtime requests or game-page errors occurred.
- The exact folder ZIP was extracted, its runtime checksums verified and the same
  native file-URL gameplay/High-rendering checks passed. Browser file/origin
  security policies were unchanged. Page logs are scoped to the current document.
- A fallback texture PNG with an invalid checksum was caught and replaced with a
  valid generated pixel. Loaded file buffers and temporary blob URLs are released
  after parsing; they are not retained for the lifetime of the game.
- The large archive/blue humanoid/PNG are authored test fixtures. They are not
  representations of the user's inaccessible Lost Warrior files or shipped as
  the default character. Exact source FBX/texture/animation compatibility remains
  unverified until local import or access to the original source is available.
- The 47 supplied runtime environment GLBs remain byte-identical to their asset
  manifest. Far-tree PNGs were re-rendered at 512×512 with genuine alpha and
  uncropped canopy framing. The graphics were visually checked in actual frames.

The earlier V4 report documents regional storyline/combat integration tests.
This release did not claim a new uninterrupted manual five-chapter playthrough.
Performance and test limits are recorded in performance.json and implementation.md.
