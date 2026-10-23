# Evidence

REA evidence bundles, decompilation dossiers, and function inventories.

Large generated bundles belong in `evidence/bundles/` or
`evidence/snapshots/`, which are gitignored. Keep durable summaries and cited
Evidence IDs in `docs/` so findings remain traceable after a session closes.

REA's Windows Ghidra provider is session-scoped. Export evidence before calling
`close_binary`.
