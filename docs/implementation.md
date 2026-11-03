# Northreach IV 4.1 — local warrior import and graphics

The five reuploaded Lost Warrior RARs each exceeded the upload-download tool's
32 MiB transfer cap. They were not downloaded or inspected. No exact Lost Warrior
model or animation is claimed to be preinstalled in this release.

## Working import route

Open **Character** from the title or pause menu. Choose LostWarriorFBX.rar,
Animation.rar and Textures.rar together, then **Use this character**. An extracted
folder, individual FBX/texture files or a self-contained GLB can also be selected.
The game processes these files locally; it does not upload them anywhere. There
is no 32 MiB chat-transfer limit on this local route. Guardrails cap individual
inputs at 1 GiB and relevant expanded content at 1.5 GiB to bound browser memory.
Render-only archives and unsupported members are skipped.

A bundled worker and WebAssembly UnRAR decoder extract RAR4/RAR5 data in memory.
Password-protected and split-volume archives report the extracted-folder route.
FBX/OBJ/MTL/GLTF, PNG/JPEG/WebP/BMP/TGA/DDS are supported. Texture references resolve
against selected files, including Windows paths and nested texture folders.
Missing external references never trigger Internet requests. Source rights still
apply. Raw Blender files, PSD/EXR textures and Draco/KTX2 models are not decoded.

The importer keeps authored root transforms and inverse-bind matrices, normalizes
the visible body to 1.82 m, matches humanoid bone/clip names and locks root travel
so animation cannot walk away from collisions. Matching duplicate FBX rest bones
are shared and reconnected to canonical parents; genuinely different rest rigs
remain separate. Bone targets receive unique names to avoid body/clothing naming
collisions. Source clips are used when compatible. Missing recognizable locomotion
can be adapted from the default rig without copying mismatched hip translations.
Unrecognized rigs or static OBJ files may have limited/procedural motion; universal
retargeting, full foot IK and exact Lost Warrior clip compatibility are not claimed.

The Character menu includes a live 3D preview with drag rotation and Idle/Walk/Run/Attack controls. Its separate renderer releases its resources when closed, and preview equipment materials are isolated from the world’s cascaded-shadow state.

The player is replaced immediately after applying the model. Native attack,
block/jump/glide/dodge clips are used when recognized; remaining actions retain
procedural poses. The default character remains for NPCs and until local import.
Facing controls allow quarter turns. A self-contained GLB with textures capped at
2048 pixels is saved in IndexedDB when available. The same model loads on the next
visit in that browser/file origin. Save GLB exports a portable copy. Failed saves
leave the model usable for the session. Journey saves and model storage are
separate; restoring the Coastguard does not erase progress.

## Graphics changes

- Replaced the indoor studio lighting probe with one cached outdoor sky probe.
  AgX tone mapping, a warmer key and cooler sky illumination preserve highlights.
- Added a soft ground-following contact shadow under the player, fading with
  altitude and hidden during swimming. It also works in Low without shadow maps.
- Grass has six curved blades per clump, broader silhouettes and varied height,
  with existing wind, bending, recovery trail, distance fade and cache budget.
- Ground colors are less brown; height-assisted surface blends, texture-derived
  normal relief and shoreline roughness add detail without extra terrain meshes.
- Added 152 instanced, rounded photographic-surface boulders, excluding main paths,
  settlements and the starting clearing. Their collisions share world physics.
- Distant tree images were re-rendered to 512×512 with complete canopy framing and
  matching world-size card geometry; the prior narrow frames cropped wide crowns.
- Graphics reconfiguration drops disposed postprocess references, and applying a
  new player registers its materials with cascaded shadows.

The supplied pixel-fantasy environment style remains visible. Texture relief is
not a new scanned PBR material set, reflections remain planar, and this does not
claim photorealistic/AAA rendering. High/Ultra cost more than Low/Medium.

## Verification

See validation.md and performance.json for the completed checks and measurements.
The authored blue humanoid used to test the import route is a synthetic fixture,
not the user's Lost Warrior, and is not bundled as the default game character.
The exact five uploaded archives still need a local import/playtest or an
accessible source URL before their contents can be verified here.
