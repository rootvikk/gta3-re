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

A machine-readable CSV will be generated in `evidence/` and summarized here.
Addresses and names are observations from Ghidra; subsystem assignments are
inferences until corroborated by call graphs, strings, or runtime behavior.
