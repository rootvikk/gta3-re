# Version Identification

Target: `C:\Users\Viraj\Desktop\Grand Theft Auto 3\gta3.exe`

SHA-256: `203c9520ab53baf1f42bdd378ca2e66d27a790d196b2fd434db9d6049b9f2796`

Analysis date: 2026-10-23

## Verdict

**GTA III 1.0 — strong identification. The executable appears to be the common
2.27 MB (2,383,872-byte) v1.0 build with PE timestamp 2002-04-30. The exact
distribution variant (retail disc versus digital/unprotected) and whether the
EXE itself has been modified remain unconfirmed.**

This is a strong inference, not a hash match against a known-clean reference
binary. See [Anomalies and open questions](#anomalies-and-open-questions) for
what would settle it.

## Observed PE metadata

| Field | Value |
| --- | --- |
| File size | 2,383,872 bytes (2.27 MiB) |
| Format | PE32, `i386` (`0x014C`), GUI subsystem |
| PE header offset | `0x80` (minimal DOS stub) |
| COFF timestamp | `1020186132` = **2002-04-30 17:02:12 UTC** |
| Linker version | **2.50** (anomalous; see below) |
| Image base | `0x400000` |
| Size of image | `0x582000` |
| Size of code | `0x1E9000` |
| Section alignment / file alignment | `0x1000` / `0x1000` |
| Subsystem version | 4.0 |
| DLL characteristics | `0x0000` (no ASLR, no NX compatibility) |
| PE sections | 13 (`14` REA segments including the header segment) |
| Entry point | `0x5c1e70` |
| Version resource | None observed |

Section names, in order:

```text
.text  _rwcseg  .rdata  .exc  .rsrc  .data  .CRT
.idata  .tls  _rwdseg  .bss  .edata  .reloc
```

The `_rwcseg` and `_rwdseg` sections are RenderWare code/data segments. They
are a strong GTA III/RenderWare fingerprint.

## String evidence

Representative strings from the 3,477-string inventory:

| Address | String | Meaning |
| --- | --- | --- |
| `0x5ec0d0` | `MODELS\GTA3.IMG` | GTA III model archive |
| `0x5f57c4` | `DATA\GTA3.DAT` | GTA III data definitions |
| `0x6108a0` | `data\main.scm` | GTA III mission script |
| `0x6013d4` | `HANDLING.CFG` | Vehicle handling configuration |
| `0x600414` | `AMERICAN.GXT` | GTA III text/localization file |
| `0x5f1b1c` | `AUDIO\HEAD.WAV` | GTA III audio asset |
| `0x5f4e38` | `MILES FAST 2D POSITIONAL AUDIO` | Miles Sound System provider |
| `0x60217c` | `CPlane::CreateIncomingCesna(void)` | GTA III class debug string |
| `0x600f68` | `CCarGenerator::DoInternalProcessing ...` | GTA III class debug string |
| `0x5efc6e` | `#<CTheScripts::UpdateObjectIndices ...` | GTA III class debug string |

The binary also contains many RenderWare source identifiers of the form
`//RenderWare/dev/rwsdk/...`, confirming RenderWare SDK integration.

`queryid\1.1` at `0x6178b4` is the **GameSpy query protocol version**, not the
game version. It must not be read as GTA III 1.1.

## Import profile

| DLL | Imports |
| --- | ---: |
| `KERNEL32` | 66 |
| `MSS32` | 55 |
| `USER32` | 37 |
| `WINMM` | 4 |
| `ADVAPI32` | 3 |
| `OLE32` | 3 |
| `DINPUT8` | 1 |
| `D3D8` | 1 |
| `DDRAW` | 1 |
| **Total** | **171** |

This is the classic GTA III PC import profile: Miles Sound System (`MSS32`),
Direct3D 8, DirectDraw, DirectInput 8, and Win32. There is no `DSOUND` import.

## External corroboration

These are historical references, not shipped-artifact evidence. They are
recorded to show why the version inference is strong, but they are not part of
the REA bundle.

- GTAForums, *US gta3.exe v1.0 filesize (Retail Disc)* (March–April 2024):
  <https://gtaforums.com/topic/996145-us-gta3exe-v10-filesize-retail-disc/>
  - Community reports identify **2.27 MB (2,383,872 bytes)** as the common
    `gta3.exe` v1.0 and note that SilentPatch targets it.
  - A separate **3.22 MB (3,382,235-byte)** first-release retail-disc variant
    is also reported, with build date **2002-04-30**.
  - The thread does not publish a SHA-256 for either variant.
- GTA.com.ua, *Original gta3.exe (1.0 & 1.1)*:
  <https://gta.com.ua/en/files/gta3/36>
  - Lists original 1.0 and 1.1 executables. The archive was not downloaded or
    analyzed.

The target hash itself was not found in public search results. No published
hash match is available.

## Inference

1. The size, PE timestamp, RenderWare segments, and GTA III-specific strings
   identify the code as a 2002 GTA III PC build.
2. The 2,383,872-byte size is the size the community associates with the common
   v1.0 executable, and the PE timestamp is consistent with the 1.0 gold build.
3. The official 1.1 release is a later patch; no 1.1-specific evidence has been
   found in this binary.
4. The target therefore appears to be **GTA III 1.0**, most likely the common
   2.27 MB unprotected/digital variant rather than the 3.22 MB retail-disc
   wrapper.

## Anomalies and open questions

### Linker version 2.50

The optional header reports linker **2.50**, a minimal DOS stub, and no Rich
header. A normal MSVC 6.0-linked executable reports linker 6.0. Possible
explanations, none confirmed:

- the executable was produced or rebuilt by a nonstandard toolchain;
- the PE header was modified when a protection wrapper was removed or the
  binary was repackaged;
- the file is a digital re-release or community-rebuilt v1.0 executable that
  preserves the original code/build timestamp.

This is **not** enough evidence to call the binary patched, but it is enough to
avoid treating the hash as a canonical retail-disc hash.

### Retail versus digital provenance

The 2.27 MB and 3.22 MB variants both appear to carry 1.0 code. The 3.22 MB
variant is associated with the first retail disc and may include a protection
wrapper. The 2.27 MB variant is the commonly distributed one and is the one
analyzed here. Its exact origin (Steam/GOG/Rockstar Launcher downgrade,
unprotected rip, or re-release) is unknown.

The forum thread also contains an ambiguous report of a **2022-10-01** date for
a 2.27 MB file. That report does not establish the PE timestamp of this binary:
the analyzed file's COFF timestamp is **2002-04-30 17:02:12 UTC**. It may
describe a file-system date or a different repackaging, so it is not treated as
a version indicator here.

### Modded install

The install contains CLEO, Modloader, ASI loaders, `_noDEP.asi`,
`d3d8.dll`, `ddraw.dll`, `dinput8.dll`, `rwd3d9.dll`, and `steam_appid.txt`.
These are outside `gta3.exe` and do not by themselves change its bytes, but
they mean the runtime observed from this folder is not a clean vanilla runtime.

## What would settle the identification

1. Compare SHA-256, file size, PE timestamp, section table, and selected code
   bytes against known-clean 1.0 and 1.1 executables from original media or a
   trusted archive.
2. Check 1.1-specific code or string differences.
3. Establish the provenance of the 2.27 MB distribution.
4. Determine whether the EXE has been patched by any of the installed mod
   components.

Until then, use the label **“GTA III 1.0 (probable)”** in reconstruction notes,
and keep the exact build/provenance as an open unknown.
