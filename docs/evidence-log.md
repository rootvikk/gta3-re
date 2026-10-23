# Evidence Log

All entries refer to target SHA-256
`203c9520ab53baf1f42bdd378ca2e66d27a790d196b2fd434db9d6049b9f2796`.

| Date | Evidence ID | Operation | Confidence | Authority |
| --- | --- | --- | --- | --- |
| 2026-10-23 | `ev_7b10d76409e81bfa9e171fddda77bc71a3dfd1876e0b6445b93c0cdb676a45e3` | `binary_overview` | derived | shipped-artifact |
| 2026-10-23 | `ev_6b2900f26ac203443d9a079f5380677cc8f4d2022ceec9d99fcc85ba2b9b755e` | `list_procedures` | observed | shipped-artifact |

## Artifacts

- Bundle: `evidence/bundles/gta3-203c9520-baseline.rea.json` (1,000,659 bytes, 2 records)
- Function inventory: `evidence/function-inventory.csv` (4,441 rows)
- Summary: `evidence/function-inventory-summary.json`

## Notes

- `binary_overview` is a derived summary: segment counts, procedure count, and
  string count over the imported program.
- `list_procedures` is the observed provider inventory used for the CSV.
- The REA session was left open after export. The bundle is the durable record;
  closing the session discards the ephemeral Ghidra program.
- Addresses and names are observations. No subsystem labels have been assigned
  or corroborated yet.
