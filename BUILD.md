# Build Instructions

## Prerequisites

- Node.js (LTS version recommended)
- npm (comes with Node.js)

## Setup

1. Install dependencies:
```bash
npm install
```

## Building Installers

### Windows
```bash
npm run build:win
```
This creates:
- NSIS installer (`.exe`) - requires admin rights, creates shortcuts
- Portable executable (`.exe`) - no installation required

### macOS
```bash
npm run build:mac
```
This creates:
- DMG disk image (`.dmg`) - drag and drop to Applications
- ZIP archive (`.zip`) - compressed app bundle

### Linux
```bash
npm run build:linux
```
This creates:
- AppImage (`.AppImage`) - universal Linux format
- Debian package (`.deb`) - for Debian/Ubuntu based systems
- RPM package (`.rpm`) - for Fedora/RHEL based systems

### All Platforms
```bash
npm run build
```

## Output

All installers are generated in the `dist/` directory.

## Distribution

Upload the generated installers to GitHub Releases for users to download.

## Notes

- The build process uses electron-builder
- The app ID is `online.idleworld.pokegrid`
- Windows builds support both x64 and ia32 (32-bit) architectures
- **Icon**: Currently using default Electron icon. To add custom icons, create:
  - Windows: `build/icon.ico` (256x256 minimum)
  - macOS: `build/icon.icns` 
  - Linux: `build/icons/` with various PNG sizes
