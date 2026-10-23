# GTA III Reconstruction

Local, evidence-driven reconstruction of Grand Theft Auto III from the shipped
binary, using REA and Ghidra as the analysis stack. This is a clean
reconstruction effort, not a port of an existing reimplementation project.

## Target

- Executable: `C:\Users\Viraj\Desktop\Grand Theft Auto 3\gta3.exe`
- SHA-256: `203c9520ab53baf1f42bdd378ca2e66d27a790d196b2fd434db9d6049b9f2796`
- Size: 2.27 MB
- Format: PE (architecture to be confirmed by REA)
- PE version resource: none observed
- Original install: read-only reference, never modified

The install also contains CLEO, Modloader, ASI loaders, and graphics/input
wrappers. Those are separate from `gta3.exe`; static analysis targets the
executable hash above.

## Ground rules

- The original game directory is never modified.
- No copyrighted game code or assets are committed to this repository.
- `game-data/` is a local reference only and is gitignored.
- Reconstruction claims must cite REA Evidence or an explicit runtime
  observation.
- Decompiler output is pseudocode and inference, not original source.

## Layout

| Path | Purpose |
| --- | --- |
| `src/` | Reconstructed C++ source, split by subsystem |
| `include/` | Public headers shared across subsystems |
| `tools/` | Asset parsers, build scripts, REA helpers |
| `evidence/` | REA evidence bundles and decompilation exports (large, gitignored) |
| `docs/` | Environment notes, function map, progress ledger, unknowns |
| `game-data/` | Local reference to the original install (gitignored) |
| `third_party/` | Third-party libraries and dependencies |
| `build/` | Generated build output (gitignored) |

## Status

Toolchain ready. Target identified. Evidence baseline in progress. See
`docs/progress.md`.
