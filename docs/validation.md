# Northreach IV verification — 2026-11-03

- 24 physics/combat/progress/settings tests passed in the final model test run.
- All 13 distinct browser cases passed across the full run and targeted retests.
  These cover imported-world startup, menu/continue/new play, movement/jumping,
  climbing/gliding/dodge, timed barrel and enemy hits, rewards/save/reload, actual
  regional quest interactions, final story completion, ferry travel both ways,
  map controls, mobile layout, settings/rebinding, extracted-ZIP startup and
  missing-code/stylesheet diagnostics.
- Story integration uses regional saved-state fixtures for enemy prerequisites;
  it verifies live interactions through all chapter transitions, not a claim of
  one uninterrupted manual playthrough. Enemy combat is separately exercised by
  timed model tests and actual keyboard attacks on a pursuing sentinel.
- Visual review caught and fixed a SkeletonUtils clone/bind-matrix bounds issue
  that scaled the character incorrectly. A browser regression check verifies its
  measured body height is between 1.6 and 2.1 meters (target 1.82 m).
- A nearby bench initially won the final beacon's interaction. Unlit beacons with
  sufficient shards now receive a distance priority; the final sequence retest
  completes Chapter V. Checkpoints store elevation to avoid respawning on roofs.
- Actual ZIP extraction to a path with spaces and file:// launch passed in
  Firefox 140.15.0: styles, WebGL, V4, imported models, movement, barrel loot,
  world map, waypoints and High-detail rendering, with zero HTTP/HTTPS requests
  and no game-page script/rendering errors.
- The final complete single HTML was copied by itself to an otherwise empty
  folder and passed the same real-file test. Reused Firefox sessions delivered
  buffered permission errors from a previous document's realm, despite a scoped
  browsing-context subscription. The harness now checks this document's realm
  and also installs early error/unhandled-rejection listeners. Both final native
  file tests passed with clear page logs and diagnostics. No origin security or
  file-access policies were relaxed.
- Chromium 155 tests the extracted ZIP through a local static server. The cloud's
  managed Chromium file-URL policy is unchanged; Firefox verifies actual file URLs.
- All 47 runtime GLB files match their recorded hashes. Kit archive path checks
  reject traversal/symlinks and supplied manifests were checked where available.
- Oak/alder distant images are 384×512 PNG with genuine transparent pixels.
- The single HTML contains two inline scripts and two inline styles, with no
  external script/stylesheet links. ZIP integrity and runtime checksums match.

Performance data are in performance.json. Software-renderer timing is not a Mac
GPU benchmark. Human listening quality and the user's Brave/device performance
have not been measured. The inaccessible Lost Warrior files and animation/engine
limits are listed in implementation.md.
