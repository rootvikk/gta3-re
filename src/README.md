# Source

Reconstructed source lives here, organized by subsystem once triage establishes
boundaries. Do not add code copied from existing reimplementation projects.

Suggested initial split, subject to evidence:

- `core/` — startup, memory, files, timers
- `game/` — world, missions, state
- `entities/` — peds, vehicles, objects
- `render/` — graphics and scene submission
- `audio/` — music, SFX, streams
- `input/` — keyboard, mouse, gamepad
- `script/` — mission script VM and opcodes
- `frontend/` — menus, HUD, text
- `rw/` — RenderWare-facing code
