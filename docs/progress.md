# Progress

Updated: 2026-10-23

## Milestones

- [x] Toolchain ready: REA 6.4.0 + Ghidra 12.1.4
- [x] Project workspace created
- [x] Target identified and hashed
- [x] Open target in REA
- [x] Confirm architecture (`x86`), entry point (`0x5c1e70`), and 14 segments
- [x] Export binary overview evidence
- [x] Build initial function inventory (4,441 procedures)
- [x] Identify version family: GTA III 1.0 (strong inference; exact provenance open)
- [x] Preliminary subsystem triage (15 anchor functions)
- [ ] Exhaustive subsystem boundary map
- [ ] Reconstruct first subsystem
- [ ] Establish a buildable test harness

## Current focus

Expand the preliminary triage into an exhaustive map. Priorities: the
boot/init chain from `0x5c1e70`, RenderWare asset loaders, audio, the script
opcode table, and the actual camera engine. Resolve the 2.27 MB versus 3.22 MB
distribution provenance and the linker-2.50 anomaly before treating the hash
as a canonical v1.0 reference.

## Completed this session

- Version 1.0 identified from PE timestamp and size, with external
  corroboration. Exact distribution variant remains open.
- 15 anchor functions decompiled across boot/init, streaming, rendering,
  input, audio, scripting, text/frontend, and vehicles.
- String inventory exported: `evidence/string-inventory.csv` (3,477 rows).
- Evidence bundle refreshed: 81 records, 22,457,656 bytes.
- New reports: `docs/version-identification.md` and
  `docs/subsystem-triage.md`.
