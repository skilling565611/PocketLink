# Audacity Integration

## Purpose

Add Audacity as an optional installable application within PocketMedic's App Installer system.

## Application Definition

```text
[Audacity]:{
    Name=Audacity
    Category=Audio / Media Tools
    InstallType=EXE
    RecommendedForControlPrime=true
    RecommendedForArcticPrime=true
    HeavyApp=false

    InstallerPatterns={
        audacity*.exe
        Audacity*.exe
        audacity-win*.exe
    }

    SearchLocations={
        Installers/
        EXE/
        PortableTools/
        PocketMedic_Data/Installers/
        OneDrive/PocketMedic/Installers/
        USB/Installers/
    }

    Notes={
        Lightweight audio editor
        Useful for recording/editing sound
        Install only from local/OneDrive/USB EXE source
        Do not use winget by default
    }
}
```

## Expected Installer Status Output

```text
Audacity
Installed: No
Installer Found: Yes
Source: Local
Status: READY FROM EXE
```

## Rules

- Never auto-install without confirmation.
- Only use actual installer EXE files.
- Do not use winget by default.
- Treat installed detection separately from installer readiness.

## Future Expansion

Potential future PocketMedic integrations for Audacity:

- Launch Audacity from PocketMedic tool launcher
- Detect portable Audacity builds
- Associate with media/editing workflow presets
