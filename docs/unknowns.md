# Known Unknowns

Track unresolved questions separately from findings. Update entries with the
evidence that resolves them.

| ID | Unknown | Status | Evidence / next step |
| --- | --- | --- | --- |
| U-001 | Exact GTA III build/version of `gta3.exe` | Open | PE is `x86`, 2.27 MB, no version resource, RenderWare segments `_rwcseg`/`_rwdseg`; exact 1.0/1.1/Steam build not established |
| U-002 | Whether the executable has been patched or modified | Open | Hash recorded; mods exist outside the EXE; no comparison against a clean reference yet |
| U-003 | Effect of CLEO/Modloader/ASI components on runtime behavior | Open | Runtime observation, separate from static `gta3.exe` analysis |
| U-004 | Subsystem boundaries (render, audio, game, script, AI, physics) | Open | 4,441 procedures inventoried; subsystem assignment pending call-graph and string triage |
| U-005 | Native asset formats used by this install | Open | Inventory `Models/`, `Audio/`, `Scripts/`; do not infer from names alone |
| U-006 | Feasible build/runtime target for reconstruction | Open | Toolchain and dependency decision after subsystem triage |
