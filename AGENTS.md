# OpenClaw Project Context

## Project identity

This repository is the current working copy of **DEEPSEEKER / Backrooms: Lost Signal**, a browser-based first-person liminal-horror game.

Important: the old README text is stale in places. The active implementation is the **Three.js browser game** loaded by `index.html` and `main.js`. The older Godot files are retained but are not the primary runtime.

## Current direction

- First-person Backrooms / liminal-horror experience.
- Large explorable environment with procedural/chunked world generation.
- Horror presentation: darkness/fog, flashlight, ambience, events, entity encounters, jumpscare-oriented presentation.
- Multiplayer foundation exists and is opt-in.
- Maintain a strong low-end performance path. The project already detects weak hardware and supports `?quality=low` / `?quality=potato`.
- Do not casually remove existing systems or assets. Prefer targeted changes that preserve current gameplay.

## Main runtime

- `index.html`: game UI, loading screen, menu/lobby UI, HUD and styling.
- `main.js`: Three.js application bootstrap and orchestration.
- `world.js`: seeded procedural/chunked Backrooms world, geometry, collision/layout and performance settings.
- `player.js`: first-person movement, pointer lock, collision, crouch, sprint/stamina, jump, camera motion and character setup.
- `multiplayer.js`: WebSocket multiplayer, room handling, remote players, shared events and chat.
- `character.js`: player/remote character and flashlight-related visuals/animation.
- `audio.js`: horror/game audio.
- `interaction.js`: world interaction logic.
- `navigation.js`: navigation/path-related systems.
- `computer.js`: in-world computer interaction.
- `securityCameras.js`: security camera system.
- `entityMode.js`: entity/arachnophobia-mode behavior.
- `textures.js`: procedural/shared texture setup.
- `levels.js`: level/state definitions.

## Assets

Important assets live under `assets/`, including:

- Backrooms bacteria models and generated animations.
- Hazmat character models.
- Apartment/house environment asset.
- Spider-Psionic ZIP asset.
- UI SVG assets.

Do not delete or replace binary assets just to simplify a code change.

## Performance expectations

Performance matters a lot. The game is intended to remain playable on weak Intel/integrated-graphics hardware as well as stronger PCs.

Existing low-end logic includes:

- Hardware detection in `main.js` and `world.js`.
- Reduced chunk render/dispose distances on low-end hardware.
- Reduced multiplayer remote-player render distance on low-end hardware.
- Quality query parameters:
  - `?quality=low`
  - `?quality=potato`
  - `?quality=high`

When optimizing, prefer:
- fewer draw calls and expensive per-frame allocations,
- chunk/object culling,
- cheaper lighting/shadows/post-processing on low-end devices,
- disposing unused GPU resources,
- throttling non-critical updates,
- reusing objects/geometries/materials.

Avoid making the game visually sterile just to gain FPS. Preserve the horror atmosphere.

## Controls / gameplay conventions

The current player implementation uses WASD movement, mouse look, sprint, crouch and jump, with stamina and camera movement effects.

Do not invert movement controls or break pointer-lock behavior while editing movement code.

## Multiplayer conventions

Multiplayer is intentionally opt-in. A normal solo URL should not silently join a public room.

Relevant URL parameters include:
- `room`
- `server`
- `seed`
- `quality`

Preserve this opt-in behavior when modifying multiplayer.

## Development rules for OpenClaw

1. Read the relevant existing module before rewriting it.
2. Make the smallest change that solves the requested problem.
3. Preserve working systems, assets, and compatibility unless the task explicitly calls for removal.
4. Test the changed path after edits when practical.
5. For visual/gameplay changes, check the browser build rather than relying only on static code inspection.
6. When a request conflicts with existing architecture, adapt the existing architecture instead of starting a parallel implementation.
7. Do not overwrite `DeepSeeker`; this repository is the separate working copy.

## Source branch reference

This repository was copied from:

`kaydenhaas49-sys/DeepSeeker`
branch:
`feature/foundations-immersion-multiplayer-20261004`

The original DeepSeeker repository should be treated as the upstream/reference project, not modified accidentally.
