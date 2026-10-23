# Environment

| Component | Value |
| --- | --- |
| OS | Windows 11 Home Single Language |
| REA | 6.4.0 |
| Ghidra | 12.1.4, `C:\Users\Viraj\Tools\ghidra_12.1.4_PUBLIC` |
| Java | 27 (64-bit JDK), `C:\Program Files\Java\jdk-27` |
| Target | `C:\Users\Viraj\Desktop\Grand Theft Auto 3\gta3.exe` |
| Target SHA-256 | `203c9520ab53baf1f42bdd378ca2e66d27a790d196b2fd434db9d6049b9f2796` |

## Observed install contents

The target folder includes `gta3.exe`, `Audio`, `Models`, `Movies`, `Mp3`,
`Scripts`, `Icons`, plus CLEO/Modloader and ASI loader components:
`III.CLEO.asi`, `Modloader/`, `_noDEP.asi`, `d3d8.dll`, `ddraw.dll`,
`dinput8.dll`, and `rwd3d9.dll`.

These components change runtime behavior but are not part of the analyzed
executable. Findings about `gta3.exe` describe that exact hash; findings about
modded runtime behavior require separate runtime evidence.

## Analysis constraints

- REA's Windows Ghidra provider is read-only and session-scoped.
- Ghidra imports are ephemeral and discarded on `close_binary`.
- Preserve evidence before closing a session.
- Decompiled output is pseudocode, not compilable original source.
