# Function Map

Initial inventory is populated from REA's `binary_overview` and
`list_procedures` evidence for the target hash recorded in
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

Machine-readable inventory: `evidence/function-inventory.csv` (4,441 rows).
Counts: `evidence/function-inventory-summary.json`.
Evidence: `ev_6b2900f26ac203443d9a079f5380677cc8f4d2022ceec9d99fcc85ba2b9b755e`
(`list_procedures`) and
`ev_7b10d76409e81bfa9e171fddda77bc71a3dfd1876e0b6445b93c0cdb676a45e3`
(`binary_overview`).

Addresses and names are Ghidra observations. Subsystem assignments remain
inferences until corroborated by call graphs, strings, or runtime behavior.
The lack of symbols means most functions will stay `FUN_*` until named by
analysis; that is expected, not an analysis failure.
