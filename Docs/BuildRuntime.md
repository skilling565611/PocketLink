# Build / Runtime Architecture

## Purpose

Define the V4 Phase 1 baseline for version information, EXE metadata, build behavior, path handling, and config loading.

## Version / Build Info

PocketMedic should expose build information from one lightweight source that can be used by the terminal UI, diagnostics, and packaged EXE metadata.

Recommended fields:

```text
AppName=PocketMedic
Version=4.0.0-dev
BuildChannel=Dev
BuildDate=Generated at build time
BuildSource=Source or EXE
```

Rules:

- Keep version data separate from installer definitions.
- Display build info in diagnostics without requiring network access.
- Allow source runs to work even when generated build metadata is missing.
- Do not store secrets, machine-specific paths, or tokens in build metadata.

## EXE Metadata

Packaged builds should identify themselves clearly in Windows properties and diagnostic output.

Recommended metadata:

```text
ProductName=PocketMedic
FileDescription=PocketMedic PC Utility
CompanyName=PocketMedic Local
InternalName=PocketMedic
OriginalFilename=PocketMedic.exe
```

Rules:

- Keep metadata generic and non-sensitive.
- Do not include usernames, machine names, token values, or private paths.
- Use the same version value shown inside the app when practical.

## Build.bat Improvements

Build.bat should stay Windows-native, app-folder relative, and easy to read.

Expected flow:

1. Resolve the script directory with `%~dp0`.
2. Run a quick Python syntax check.
3. Build the EXE with PyInstaller.
4. Copy required config/docs/helper files beside the EXE.
5. Print the output folder and any follow-up manual steps.

Rules:

- Do not require global PATH changes.
- Do not download dependencies during normal builds.
- Do not auto-run generated EXEs or installers after build.
- Keep InstallRunner.bat beside PocketMedic.exe when installer execution is enabled.

## Path Handling Fixes

Runtime path handling should separate bundled resources from external app-folder files.

Path types:

```text
BundledResources = files packaged inside the EXE
AppBase = folder containing PocketMedic.exe, or project root when running from source
ExternalData = Installers/, EXE/, PortableTools/, PocketMedic_Data/
```

Rules:

- Use bundled-resource lookup only for packaged internal files.
- Use the EXE-adjacent app folder for external installers and helper scripts.
- Do not depend only on the current working directory.
- Do not use PyInstaller temp extraction paths for external installer discovery.
- Keep OneDrive and USB installer paths as later fallback locations.

## Config Loading Enhancements

Config loading should support both source and packaged runs without becoming heavy.

Expected priority:

1. EXE-adjacent config override
2. Project/source config
3. Bundled default config
4. Built-in safe defaults

Rules:

- Missing config should produce a clear warning and safe defaults.
- Invalid config should not crash the app before diagnostics can report the issue.
- External override config should never be bundled with secrets.
- Machine profiles and app definitions should remain modular files where possible.

## Phase 1 Done Criteria

- Build/version fields are documented and ready for implementation.
- EXE metadata expectations are defined.
- Build.bat responsibilities are clear.
- Resource paths and external paths are treated as separate systems.
- Config priority is documented for source and EXE runs.
