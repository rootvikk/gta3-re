# Evidence Log

All REA entries refer to target SHA-256
`203c9520ab53baf1f42bdd378ca2e66d27a790d196b2fd434db9d6049b9f2796`.

## REA evidence

| Date | Evidence ID | Operation | Subject | Confidence | Authority |
| --- | --- | --- | --- | --- | --- |
| 2026-10-23 | `ev_7b10d76409e81bfa9e171fddda77bc71a3dfd1876e0b6445b93c0cdb676a45e3` | `binary_overview` | target | derived | shipped-artifact |
| 2026-10-23 | `ev_6b2900f26ac203443d9a079f5380677cc8f4d2022ceec9d99fcc85ba2b9b755e` | `list_procedures` | target | observed | shipped-artifact |
| 2026-10-23 | `ev_76e8c549605babcb886c053ea7d0e866e087fc08b4d9e9ad8ba663307190600e` | `list_strings` | target | observed | shipped-artifact |
| 2026-10-23 | `ev_94b62a975bff89804633afb07764e7152e372d03d4775757b2bc154d2ae6ac58` | `analyze_function` | `FUN_00405c80` (`0x405c80`) | observed | shipped-artifact |
| 2026-10-23 | `ev_c5a7c9656f570fa89448949df48efe77cc7b4918cc7c601f1939f62b2893638c` | `analyze_function` | `FUN_0048e7e0` (`0x48e7e0`) | observed | shipped-artifact |
| 2026-10-23 | `ev_01885d85c82552776f2c2f6601a466bcf99bed1b137c56f339e41cad148d1eaf` | `analyze_function` | `FUN_00588490` (`0x588490`) | observed | shipped-artifact |
| 2026-10-23 | `ev_80588f9353e8f988b7ac3b5e7e3843d9cc9d5254886428592d34e4513f723fef` | `analyze_function` | `FUN_00546db0` (`0x546db0`) | observed | shipped-artifact |
| 2026-10-23 | `ev_77eca36eab8012326e28a6c4556e943f9d4116959facd0a6b543f0a4dd77f3a6` | `analyze_function` | `FUN_0052c3c0` (`0x52c3c0`) | observed | shipped-artifact |
| 2026-10-23 | `ev_a9fadc4aae44eb7bef5d2c45e231fe41841e3eb1dcd81778021acacb927e33c2` | `analyze_function` | `FUN_00581cb0` (`0x581cb0`) | observed | shipped-artifact |
| 2026-10-23 | `ev_35c270e4aff7f7d0fd8dfaa736845e483fec3b08261a48f56f7b30f595f6c84b` | `analyze_function` | `FUN_00580f30` (`0x580f30`) | observed | shipped-artifact |
| 2026-10-23 | `ev_17910581e8ada7e944298308a7affe3ca2f59fc5f3ee5c6b895b1c09dd03b298` | `analyze_function` | `FUN_005830d0` (`0x5830d0`) | observed | shipped-artifact |
| 2026-10-23 | `ev_2364a94cc1734594653b857eb8448bbd48497b8b02098ae967747d601f38678f` | `analyze_function` | `FUN_0054e000` (`0x54e000`) | observed | shipped-artifact |
| 2026-10-23 | `ev_3050dd45336e1d4a0edf5a8a4c65e098f0c0a009ced228a79d3801cf936cf7c5` | `analyze_function` | `FUN_005426e0` (`0x5426e0`) | observed | shipped-artifact |
| 2026-10-23 | `ev_8c780f912579e23c8b515f685a06b1b877d545262907dc70a5462191c087d14c` | `analyze_function` | `FUN_005656f0` (`0x5656f0`) | observed | shipped-artifact |
| 2026-10-23 | `ev_8d195db664e7b3b29e6f6ba994e5da5c4863b73ae58a8fde0ddd5e481e1df18c` | `analyze_function` | `FUN_00566530` (`0x566530`) | observed | shipped-artifact |
| 2026-10-23 | `ev_6345db8133da2a2fd9030299010e52e6563fd35b864ed93f28a07e70fbc1b193` | `analyze_function` | `FUN_0047a230` (`0x47a230`) | observed | shipped-artifact |
| 2026-10-23 | `ev_afcb86a7f9f2046f06d03726f696fdd8e1382170ab38ce891e37d945dddcbdec` | `analyze_function` | `FUN_00440cb0` (`0x440cb0`) | observed | shipped-artifact |
| 2026-10-23 | `ev_c04c31414dda0ba1ea435273995abb4014d4761daf4ba43788923f85cb1e550a` | `analyze_function` | `FUN_0048bd50` (`0x48bd50`) | observed | shipped-artifact |

The bundle contains 81 records, including repeated `xrefs`,
`resolve_containing_procedure`, and two repeated `analyze_function` calls for
`0x405c80` and `0x48e7e0`. The table lists one canonical analysis per anchor;
repeated records are retained in the bundle but are not separate findings.

## Artifacts

- Bundle: `evidence/bundles/gta3-203c9520-baseline.rea.json`
  (22,457,656 bytes, 81 records, refreshed 2026-10-23; gitignored)
- Function inventory: `evidence/function-inventory.csv` (4,441 rows)
- String inventory: `evidence/string-inventory.csv` (3,477 rows)
- Summary: `evidence/function-inventory-summary.json`
- Reports: `docs/version-identification.md`, `docs/subsystem-triage.md`

## External references

These are not part of the REA bundle and are not shipped-artifact evidence.
They are recorded only as corroboration for the version inference.

| Date accessed | Reference | Use |
| --- | --- | --- |
| 2026-10-23 | GTAForums, *US gta3.exe v1.0 filesize (Retail Disc)*, <https://gtaforums.com/topic/996145-us-gta3exe-v10-filesize-retail-disc/> | Community reports 2,383,872 bytes as the common v1.0; reports a 3,382,235-byte retail-disc variant with 2002-04-30 build date |
| 2026-10-23 | GTA.com.ua, *Original gta3.exe (1.0 & 1.1)*, <https://gta.com.ua/en/files/gta3/36> | Lists original 1.0 and 1.1 executables; archive not downloaded or analyzed |

## Notes

- `binary_overview` is a derived summary: segment counts, procedure count, and
  string count over the imported program.
- `list_procedures` and `list_strings` are observed provider inventories used
  for the CSVs.
- `analyze_function` dossiers can be large; `FUN_00588490` and `FUN_00440cb0`
  exceed the MCP response budget. Their retained Evidence IDs above are the
  durable record and can be read with `inspect_analysis_view`.
- The REA session was left open after export. The bundle is the durable record;
  closing the session discards the ephemeral Ghidra program.
- Addresses, body sizes, calls, and strings are observations. Subsystem labels
  and version labels are inferences unless explicitly marked otherwise.
