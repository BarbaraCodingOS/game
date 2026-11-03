# Northreach IV — implementation and limits

The user's 25 KB V4 brief is the task specification. Forty environment uploads
were downloaded. Archive paths/symlinks were checked, files were extracted without
executing their helper scripts, and available kit manifest hashes were verified.
47 selected self-contained GLBs are embedded in the runtime. Original authored
node transforms are retained in templates and baked once for static material
batching. The world includes 216+ prop instances plus instanced trees/undergrowth.

## Implemented

- Shared geometry/material batches, 1,150 supplied oak/alder trees, rendered-tree
  distant cards with dither transitions, forest understory, reeds, heather and
  laurel. Instance buffers update by movement thresholds rather than every frame.
- 59 cached terrain sections, built asynchronously at startup from the same
  triangle height field used by physics. Sea-floor-only sections are skipped;
  visible sections are frustum culled. Terrain is ready before entering the world.
  Structures and models are preloaded, so gameplay doesn't wait for them to fetch.
- Small curved grass blades, clustered growth/bare patches, wind, local bending
  with a short recovery trail, distance fade and a bounded LRU patch cache. The
  queue is prioritized toward player velocity and processed with a per-frame
  generation budget. This is a finite 1.2 km map, not an infinite streamed world.
- Photographic ground surfaces blended by slope/elevation/trails, triplanar rock,
  source-material PBR assets, environment illumination, soft sun shadows and
  two/three cascades at High/Ultra. High offers GTAO and restrained bloom. Distance
  cards/grass are excluded from the AO normal pass to avoid opaque-card artifacts.
- Reflective water with Fresnel, multi-scale normal waves, height-field depth
  color and foam. Reflections use a bounded 512 px target; water settings control
  refresh rate. These are planar reflections, not ray tracing or screen refraction.
- Sky/cloud motion, 20-minute daylight cycle, mist/rain settings, night illumination,
  animated gull silhouettes, ambient wind, and surface-dependent procedural steps.
- Imported modular village/shops, functional well/bell, named keeper/fisher/ferry
  NPC interactions, stronghold ruins, mountain grotto, mooring/pier, ships, caches,
  lookout, coastguard relic and optional driftwood quest. Indoor wall/deck support
  uses geometry, not whole-assembly solid boxes. There are no furnished dungeon
  networks, vehicle sailing controls or crowd simulation.
- Light three-hit combo, heavy attack, input buffer, actual timed hit windows,
  attack arcs/heights, obstruction checks, stagger, enemy pursuit/return/telegraph,
  dodge invulnerability, facing-dependent block, healing and death/checkpoint
  recovery. The Hollow King accelerates below half health. Enemies are awakened
  effigies/wisps with procedural motion, not newly mocapped humanoids.
- Five sequential, playable story chapters driven by persistent event flags.
  Early discoveries count when their chapter becomes current. Main/side objectives
  and rewards are idempotent. The ferryman makes the northern region accessible.
- Minimal contextual HUD, cinematic in-engine title scene, Continue/New Game,
  journal/map/inventory, persistent settings and rebindable action/movement keys.
  New Game asks before replacing the local save; settings remain independent.
- Versioned V4 saves, V3 migration when accessible in the browser origin, validated
  snapshots, previous-good-save backup, automatic safe-position saves, checkpoint
  altitude and graceful storage-denied behavior. Local-file origins may separate
  saves by path; moving files/changing browsers does not guarantee save migration.

## Character limitation

Every uploaded Lost Warrior .rar/.blend file exceeds the download tool's 32 MiB
transfer cap. They could not be transferred or inspected. A self-contained GLB
under that cap, with textures and desired clips, is needed to replace the current
character. The working Mixamo rig remains for player/NPCs with original locomotion
clips. Playback speed follows actual displacement; combat/guard/aerial/draw poses
are procedural. Full foot IK, dedicated start/stop/landing/combat clips, and a Lost
Warrior retarget are not claimed.

## Verification and performance

See validation.md and performance.json. Cloud tests use software rendering; this
is not the user's Mac GPU, and a stable 60 FPS on that hardware has not been
established. High/Ultra are deliberately scalable and cost more than Low/Medium.

## Skills applied

The uploaded game-dev collection at /workspace/gamedev-skills informed Three.js
GLB loading/materials, measured performance work, game feel, RPG event objectives,
and versioned saves. Three.js remains pinned to r187. Source metadata and licenses
are preserved in asset-manifest.json and ASSET-CREDITS.txt, including individual
uploads explicitly marked pending license clearance; no blanket CC0 is asserted.
