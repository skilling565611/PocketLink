# Installer System Architecture

## Installer Source Priority

1. Local Installers/
2. Local EXE/
3. Local PortableTools/
4. PocketMedic_Data/Installers/
5. OneDrive Installers/
6. USB Installers/

## Rules

- EXE files only
- Never use winget by default
- Never auto-run installers
- Always confirm before launch
- Keep installer EXE execution isolated in InstallRunner.bat unless this rule is explicitly changed later

## Status Types

- INSTALLED
- READY FROM EXE
- MISSING INSTALLER EXE
- WINDOWSAPPS ALIAS ONLY
- NOT READY
