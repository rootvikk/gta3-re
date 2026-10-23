# Function Map

Initial inventory is populated from REA's `binary_overview`,
`list_procedures`, and `list_strings` evidence for the target hash recorded in
`docs/environment.md`.

## Columns

| Column | Meaning |
| --- | --- |
| `address` | Provider address for the procedure entry |
| `name` | Provider name (`FUN_...` means unnamed) |
| `external` | Imported/external procedure |
| `thunk` | Provider-classified thunk |
| `thunk_target` | Resolved thunk destination, when known |
| `notes` | Analyst notes, subsystem guess, confidence |

## Baseline inventory (2026-10-23)

| Fact | Value |
| --- | --- |
| Target | `gta3.exe` |
| SHA-256 | `203c9520ab53baf1f42bdd378ca2e66d27a790d196b2fd434db9d6049b9f2796` |
| Format / architecture | PE / `x86` (32-bit) |
| Entry point | `0x5c1e70` |
| Segments | 14 |
| Procedures | 4,441 total |
| Internal procedures | 4,270 |
| Externals / imports | 171 |
| Thunks | 5 |
| Named non-`FUN_` entries | 6 |
| Unnamed (`FUN_*`) entries | 4,264 |
| Strings | 3,477 |

Machine-readable inventories: `evidence/function-inventory.csv` (4,441 rows)
and `evidence/string-inventory.csv` (3,477 rows). Counts:
`evidence/function-inventory-summary.json`.
Evidence: `ev_6b2900f26ac203443d9a079f5380677cc8f4d2022ceec9d99fcc85ba2b9b755e`
(`list_procedures`) and
`ev_7b10d76409e81bfa9e171fddda77bc71a3dfd1876e0b6445b93c0cdb676a45e3`
(`binary_overview`).

Addresses and names are Ghidra observations. Subsystem assignments remain
inferences until corroborated by call graphs, strings, or runtime behavior.
The lack of symbols means most functions will stay `FUN_*` until named by
analysis; that is expected, not an analysis failure.

## Confirmed anchor functions (preliminary)

Full analysis and evidence IDs: `docs/subsystem-triage.md`.

| Address | Function | Observed role | Subsystem | Confidence |
| --- | --- | --- | --- | --- |
| `0x405c80` | `FUN_00405c80` | CdStream/IMG init; `MODELS\GTA3.IMG` | Streaming / asset I/O | High |
| `0x48e7e0` | `FUN_0048e7e0` | Loads `DATA\GTA3.DAT` and `loadsc0` | Data loading | High |
| `0x588490` | `FUN_00588490` | `main.scm` script system | Scripting | High |
| `0x546db0` | `FUN_00546db0` | Parses `HANDLING.CFG` | Vehicles / config | High |
| `0x52c3c0` | `FUN_0052c3c0` | GXT language/text loading | Text / localization | High |
| `0x581cb0` | `FUN_00581cb0` | `Direct3DCreate8`, device creation | Rendering / D3D8 | High |
| `0x580f30` | `FUN_00580f30` | `DirectDrawCreateEx`, display mode | Rendering / display | High |
| `0x5830d0` | `FUN_005830d0` | `DirectInput8Create` | Input | High |
| `0x54e000` | `FUN_0054e000` | `CPlane::CreateIncomingCesna` | Vehicles / entities | High |
| `0x5426e0` | `FUN_005426e0` | `CCarGenerator::DoInternalProcessing` | Vehicles / world | High |
| `0x5656f0` | `FUN_005656f0` | 3D audio provider selection | Audio | High |
| `0x566530` | `FUN_00566530` | Miles audio startup; `AUDIO\HEAD.WAV` | Audio | High |
| `0x47a230` | `FUN_0047a230` | Frontend/menu/HUD texture loading | Frontend / UI | High |
| `0x440cb0` | `FUN_00440cb0` | Script opcode dispatcher (camera/vehicle commands) | Scripting | Medium-high |
| `0x48bd50` | `FUN_0048bd50` | Init orchestrator (GXT, surface data, audio provider) | Boot / init | Medium |

These are 15 anchors out of 4,441 procedures, not a complete subsystem map.
Two anchors correct earlier string-only labels: `FUN_0048bd50` is an
initialization orchestrator rather than an audio-only routine, and
`FUN_00440cb0` is a script command dispatcher rather than the camera engine.
