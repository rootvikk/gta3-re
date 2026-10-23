# Subsystem Triage

Target: `gta3.exe`

SHA-256: `203c9520ab53baf1f42bdd378ca2e66d27a790d196b2fd434db9d6049b9f2796`

Analysis date: 2026-10-23

## Scope and method

This is a **preliminary** triage of 15 anchor functions out of 4,441
procedures. Anchors were selected from distinctive strings, import thunks, and
class-prefixed debug strings, then confirmed by decompiling the containing
procedure. It is not an exhaustive subsystem boundary map.

Evidence is REA/Ghidra static analysis of the shipped executable. Function
roles are inferences from API calls, strings, and control flow; addresses,
body sizes, and called APIs are observations. No runtime behavior was observed.

## Evidence legend

| ID | Address | Function | Evidence ID |
| --- | --- | --- | --- |
| E1 | `0x405c80` | `FUN_00405c80` | `ev_94b62a975bff89804633afb07764e7152e372d03d4775757b2bc154d2ae6ac58` |
| E2 | `0x48e7e0` | `FUN_0048e7e0` | `ev_c5a7c9656f570fa89448949df48efe77cc7b4918cc7c601f1939f62b2893638c` |
| E3 | `0x588490` | `FUN_00588490` | `ev_01885d85c82552776f2c2f6601a466bcf99bed1b137c56f339e41cad148d1eaf` |
| E4 | `0x546db0` | `FUN_00546db0` | `ev_80588f9353e8f988b7ac3b5e7e3843d9cc9d5254886428592d34e4513f723fef` |
| E5 | `0x52c3c0` | `FUN_0052c3c0` | `ev_77eca36eab8012326e28a6c4556e943f9d4116959facd0a6b543f0a4dd77f3a6` |
| E6 | `0x581cb0` | `FUN_00581cb0` | `ev_a9fadc4aae44eb7bef5d2c45e231fe41841e3eb1dcd81778021acacb927e33c2` |
| E7 | `0x580f30` | `FUN_00580f30` | `ev_35c270e4aff7f7d0fd8dfaa736845e483fec3b08261a48f56f7b30f595f6c84b` |
| E8 | `0x5830d0` | `FUN_005830d0` | `ev_17910581e8ada7e944298308a7affe3ca2f59fc5f3ee5c6b895b1c09dd03b298` |
| E9 | `0x54e000` | `FUN_0054e000` | `ev_2364a94cc1734594653b857eb8448bbd48497b8b02098ae967747d601f38678f` |
| E10 | `0x5426e0` | `FUN_005426e0` | `ev_3050dd45336e1d4a0edf5a8a4c65e098f0c0a009ced228a79d3801cf936cf7c5` |
| E11 | `0x5656f0` | `FUN_005656f0` | `ev_8c780f912579e23c8b515f685a06b1b877d545262907dc70a5462191c087d14c` |
| E12 | `0x566530` | `FUN_00566530` | `ev_8d195db664e7b3b29e6f6ba994e5da5c4863b73ae58a8fde0ddd5e481e1df18c` |
| E13 | `0x47a230` | `FUN_0047a230` | `ev_6345db8133da2a2fd9030299010e52e6563fd35b864ed93f28a07e70fbc1b193` |
| E14 | `0x440cb0` | `FUN_00440cb0` | `ev_afcb86a7f9f2046f06d03726f696fdd8e1382170ab38ce891e37d945dddcbdec` |
| E15 | `0x48bd50` | `FUN_0048bd50` | `ev_c04c31414dda0ba1ea435273995abb4014d4761daf4ba43788923f85cb1e550a` |

## Anchor summary

| ID | Function | Body bytes | Observed role | Subsystem | Confidence |
| --- | --- | ---: | --- | --- | --- |
| E1 | `FUN_00405c80` | 303 | CdStream/IMG initialization; `cdvd_stream`, `MODELS\GTA3.IMG`, buffered/async/sync loading | Streaming / asset I/O | High |
| E2 | `FUN_0048e7e0` | 29 | Loads `DATA\GTA3.DAT` and `loadsc0` | Data/asset loading | High |
| E3 | `FUN_00588490` | 6,190 | `main.scm` script system; 75 callees | Scripting | High |
| E4 | `FUN_00546db0` | 1,107 | Parses `HANDLING.CFG`; config parser calls | Vehicles / configuration | High |
| E5 | `FUN_0052c3c0` | 432 | Selects and loads `AMERICAN/FRENCH/GERMAN/ITALIAN/SPANISH.GXT` | Text / localization | High |
| E6 | `FUN_00581cb0` | 200 | `Direct3DCreate8`, device creation | Rendering / D3D8 | High |
| E7 | `FUN_00580f30` | 97 | `DirectDrawCreateEx`, display mode setup | Rendering / display | High |
| E8 | `FUN_005830d0` | 49 | `DirectInput8Create` | Input | High |
| E9 | `FUN_0054e000` | 248 | `CPlane::CreateIncomingCesna`, creates a plane entity | Vehicles / entities | High |
| E10 | `FUN_005426e0` | 1,218 | `CCarGenerator::DoInternalProcessing`, vehicle spawning | Vehicles / world | High |
| E11 | `FUN_005656f0` | 515 | 3D audio provider selection: Miles, EAX, Dolby Surround | Audio | High |
| E12 | `FUN_00566530` | 2,160 | `AIL_startup`, digital driver, `AUDIO\HEAD.WAV` | Audio | High |
| E13 | `FUN_0047a230` | 513 | Frontend/menu/HUD TXD and sprite loading | Frontend / UI | High |
| E14 | `FUN_00440cb0` | 7,289 | Script opcode dispatcher for camera/vehicle/game commands | Scripting | Medium-high |
| E15 | `FUN_0048bd50` | 354 | Initialization orchestrator: GXT, surface data, audio-provider selection | Boot / init | Medium |

## Subsystems

### 1. Boot, init, and core data

- **E15 `FUN_0048bd50`** is a broad initialization orchestrator, not an
  audio-only function. It calls E5 (GXT text initialization), loads
  `DATA\SURFACE.DAT`, calls several other subsystem initializers, and selects
  the Miles audio provider. Exact class ownership is unknown; it may be a game
  or file-loader initialization routine.
- **E2 `FUN_0048e7e0`** is a small wrapper that loads `DATA\GTA3.DAT` and the
  `loadsc0` asset. It is a concrete entry point for data-definition loading.
- The CRT entry point is `0x5c1e70`. `WinMain` and the full init order have not
  yet been identified.

**Unknown:** the call graph from entry point to E15, initialization order, and
which routine owns global game state.

### 2. Streaming and asset I/O

- **E1 `FUN_00405c80`** initializes the `CdStream` path and the GTA III IMG
  archive. It references `cdvd_stream`, `MODELS\GTA3.IMG`, and the buffered,
  async, and sync streaming modes.
- **E2 `FUN_0048e7e0`** loads `DATA\GTA3.DAT` and `loadsc0`.
- RenderWare is present: `_rwcseg`/`_rwdseg` sections and many
  `//RenderWare/dev/rwsdk/...` source identifiers.
- Asset strings are abundant (`MODELS`, `ANIM`, `TXD`, `DFF`, `IFP`, `COL`),
  but many have no direct code xref because they are reached through pointer
  tables.

**Unknown:** IMG directory parsing, TXD/DFF/COL/IFP loaders, streaming
scheduler, and the boundary between GTA III asset code and RenderWare.

### 3. Rendering and display

- **E6 `FUN_00581cb0`** calls `Direct3DCreate8` and creates the D3D8 device.
- **E7 `FUN_00580f30`** calls `DirectDrawCreateEx` and sets a display mode.
- D3D8 and DirectDraw are both imported; the game likely uses DirectDraw for
  display mode enumeration and D3D8 for rendering.
- RenderWare supplies the rendering pipeline, but no RenderWare renderer
  function is anchored yet.

**Unknown:** renderer initialization, world/entity rendering, camera engine,
font/sprite rendering, and the D3D8/RenderWare boundary.

### 4. Input

- **E8 `FUN_005830d0`** is a thin `DirectInput8Create` wrapper.
- `DINPUT8` has exactly one import; `WINMM` has four, likely timing or legacy
  input support.

**Unknown:** keyboard/mouse/joystick device enumeration, action mapping, force
feedback, and the Win32 message pump.

### 5. Audio

- **E11 `FUN_005656f0`** selects and configures a 3D audio provider. It uses
  `AIL_open_3D_provider`, `AIL_set_3D_provider_preference`, EAX 3, and Dolby
  Surround strings.
- **E12 `FUN_00566530`** starts Miles (`AIL_startup`), opens a digital driver,
  configures sample handles, and opens `AUDIO\HEAD.WAV`.
- `MSS32` is the largest non-Win32 import group (55 functions). There is no
  `DSOUND` import.
- **E15** also references `MILES FAST 2D POSITIONAL AUDIO`, but it is an
  initialization orchestrator, not the audio subsystem itself.

**Unknown:** radio/MP3 streaming, SFX banks, entity/cutscene audio, and the
mapping from `AIL_*` imports to game-level audio classes.

### 6. Scripting

- **E3 `FUN_00588490`** is the `main.scm` script system: 6,190 bytes, 75
  callees, and a direct reference to `data\main.scm`.
- **E14 `FUN_00440cb0`** is a script opcode dispatcher. Its switch handles
  opcode `400` and `0x191`–`0x1b6`, then calls camera, vehicle, and game
  helpers. It is **not** the camera engine; the `camera` string was only the
  entry point into this command table.
- `CTheScripts::UpdateObjectIndices` exists as a debug string but has no direct
  code xref.

**Unknown:** the full opcode table, interpreter loop, mission hooks, and how
CLEO’s external ASI hooks into this system.

### 7. Text, localization, and frontend

- **E5 `FUN_0052c3c0`** selects a GXT file from the language setting:
  `AMERICAN.GXT`, `FRENCH.GXT`, `GERMAN.GXT`, `ITALIAN.GXT`, `SPANISH.GXT`.
- **E13 `FUN_0047a230`** loads frontend/menu/HUD textures and sprites:
  `MODELS/FRONTEND.TXD`, `MODELS/MENU.TXD`, `frontend`, `LOAD frontend`.
- The binary contains many HUD/menu sprite names (`fe2_mainpanel_ul`,
  `connection24`, `findgame24`).

**Unknown:** font rendering, HUD state, radar, menu state machine, and the
frontend/game transition.

### 8. Vehicles, entities, and world simulation

- **E4 `FUN_00546db0`** parses `HANDLING.CFG` and drives the vehicle handling
  configuration.
- **E9 `FUN_0054e000`** is `CPlane::CreateIncomingCesna`, creating a plane
  entity.
- **E10 `FUN_005426e0`** is `CCarGenerator::DoInternalProcessing`, handling
  vehicle spawning and ground-height checks.

**Unknown:** vehicle physics, AI, pathfinding, population, peds, weapons,
collision, and world-sector streaming. This is the largest uncovered area.

### 9. Network / GameSpy (legacy)

- GameSpy strings are present, including the query template at `0x6178b4`:
  `\gamename\%s\gamever\%s\location\0\validate\%s\final\\queryid\1.1\`.
- No direct code xref was found for the GameSpy error string at `0x617120`.
- The import table has no `WS2_32` or `WSOCK32`; network support may be static,
  legacy, or inactive in this build.

**Unknown:** whether any multiplayer/GameSpy code is reachable in the shipped
single-player executable.

### 10. Debug symbols and naming

- Only four class-prefixed debug strings were found: `CPlane` (two),
  `CTheScripts` (one), and `CCarGenerator` (one).
- The executable has no symbol table and few RTTI/debug names. Most functions
  are `FUN_*`.
- The `FUN_*` names are Ghidra observations, not original symbols.

## Import and string hints

Import groups (171 total): `KERNEL32` 66, `MSS32` 55, `USER32` 37, `WINMM` 4,
`ADVAPI32` 3, `OLE32` 3, `DINPUT8` 1, `D3D8` 1, `DDRAW` 1.

The string inventory (3,477 strings) is heavily weighted toward asset paths
and RenderWare identifiers. Keyword counts are not subsystem sizes: a single
RenderWare source path can match “stream” or “raster” and inflate a category.

## Coverage and limitations

- 15 anchors out of 4,441 procedures; the map is deliberately incomplete.
- Many asset strings have no direct xref because the code uses pointer tables;
  a missing xref does **not** mean the subsystem is absent.
- Two anchors are broader or narrower than their triggering string:
  - E15 is an init orchestrator, not pure audio.
  - E14 is a script opcode dispatcher, not the camera engine.
- Static analysis only; no runtime behavior, timing, or mod interaction was
  observed.
- Ghidra pseudocode is not original source and may contain decompiler
  artifacts.

## Next steps

1. Follow callers/callees from entry `0x5c1e70` and E15 to identify `WinMain`
   and the game initialization order.
2. Map RenderWare asset loaders (TXD/DFF/COL/IFP) and the IMG directory parser.
3. Trace `MSS32` IAT calls to radio, SFX, and cutscene audio code.
4. Recover the script opcode table and interpreter around E3/E14.
5. Find the actual camera engine through update/render functions, not the
   script command string.
6. Map frontend/HUD/text rendering and the menu state machine.
7. Determine whether GameSpy/network code is reachable.
8. Expand the anchor set with call-graph hubs and high-fan-in functions.
