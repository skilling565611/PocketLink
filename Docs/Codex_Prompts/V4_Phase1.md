# V4 Phase 1

- Version / Build Info
- EXE Metadata
- Build.bat Improvements
- Path Handling Fixes
- Config Loading Enhancements

## Working Doc

- See `Docs/BuildRuntime.md` for the Phase 1 build/runtime baseline.

## Guardrails

- Keep this phase lightweight and Windows-friendly.
- Preserve source and EXE compatibility.
- Do not restructure installer execution; Phase 2 owns the installer rewrite.
- Keep bundled-resource paths separate from external EXE-adjacent paths.
