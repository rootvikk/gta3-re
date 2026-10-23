# Known Unknowns

Track unresolved questions separately from findings. Update entries with the
evidence that resolves them.

| ID | Unknown | Status | Evidence / next step |
| --- | --- | --- | --- |
| U-001 | Exact GTA III build/version of `gta3.exe` | Partially resolved | **GTA III 1.0 (strong inference).** 2,383,872 bytes, PE timestamp 2002-04-30 17:02:12Z; community reports 2.27 MB as common v1.0. Exact retail/digital variant open; no published hash match. Next: compare clean 1.0/1.1 binaries. |
| U-002 | Whether the executable has been patched or modified | Open | Linker 2.50, minimal DOS stub, no Rich header; 2.27 MB variant versus reported 3.22 MB retail-disc variant; mods exist outside the EXE. Next: compare header/code against clean 1.0 and audit installed patches. |
| U-003 | Effect of CLEO/Modloader/ASI components on runtime behavior | Open | Runtime observation, separate from static `gta3.exe` analysis |
| U-004 | Subsystem boundaries (render, audio, game, script, AI, physics) | Partially resolved | 15 anchor functions mapped in `docs/subsystem-triage.md` out of 4,441 procedures. Next: exhaustive call-graph map. |
| U-005 | Native asset formats used by this install | Open | Inventory `Models/`, `Audio/`, `Scripts/`; do not infer from names alone |
| U-006 | Feasible build/runtime target for reconstruction | Open | Toolchain and dependency decision after subsystem triage |
| U-007 | Location of the actual camera engine | Open | `FUN_00440cb0` is a script opcode dispatcher, not the camera engine. Next: find camera update/render functions and their callers. |
| U-008 | Whether GameSpy/network code is reachable | Open | GameSpy strings present, no direct code xref, no `WS2_32`/`WSOCK32` imports. Next: trace string tables and export usage. |
| U-009 | Cause of the linker-2.50 / minimal-DOS-stub header | Open | Optional header bytes report linker 2.50; MSVC 6.0 would normally report 6.0. Next: compare with known 1.0 and 3.22 MB retail headers. |
| U-010 | Provenance of the 2.27 MB versus 3.22 MB v1.0 executables | Open | Community reports both as 1.0; 3.22 MB is associated with first retail disc, 2.27 MB with the common/digital build. Next: obtain trusted metadata, not game files. |
