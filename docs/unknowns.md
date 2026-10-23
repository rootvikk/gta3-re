# Known Unknowns

Track unresolved questions separately from findings. Update entries with the
evidence that resolves them.

| ID | Unknown | Status | Evidence / next step |
| --- | --- | --- | --- |
| U-001 | Exact GTA III build/version of `gta3.exe` | Open | PE metadata, string search, comparison with known builds |
| U-002 | Whether the executable has been patched or modified | Open | Compare file regions, imports, and entry code against a clean reference |
| U-003 | Effect of CLEO/Modloader/ASI components on runtime behavior | Open | Runtime observation, separate from static `gta3.exe` analysis |
| U-004 | Subsystem boundaries (render, audio, game, script, AI, physics) | Open | Call graph and string-reference triage |
| U-005 | Native asset formats used by this install | Open | Inventory `Models/`, `Audio/`, `Scripts/`; do not infer from names alone |
| U-006 | Feasible build/runtime target for reconstruction | Open | Toolchain and dependency decision after subsystem triage |
