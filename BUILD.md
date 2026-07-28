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

## Auto-updater Configuration

The app includes **optional** automatic update functionality via `electron-updater`. To enable it:

1. **GitHub Releases**: The updater checks for new releases on GitHub
2. **Publish configuration**: Already configured in `package.json` under `build.publish`
3. **GitHub Token**: For automated publishing, set `GH_TOKEN` environment variable:
   ```bash
   export GH_TOKEN=your_github_personal_access_token
   npm run build:win -- -p always
   ```

### How Auto-updater Works

- **Opt-in only**: Auto-check is **disabled by default** - user must explicitly enable it
- **Manual check**: Users can always check via "🔄 Verificar atualizações" button in the menu
- **User control**: Updates are never downloaded automatically - user must confirm
- **Data preservation**: User data (logins, settings) are preserved in `userData` directory
- **Installation**: Updates are installed on app quit if already downloaded

### Release Process (Automated)

Use the GitHub Actions workflow for automated releases:

1. Go to **Actions** tab in your GitHub repository
2. Select **Release** workflow
3. Click **Run workflow**
4. Choose branch (usually `main`)
5. Select version type:
   - **patch**: 1.1.3 → 1.1.4 (bug fixes)
   - **minor**: 1.1.3 → 1.2.0 (new features)
   - **major**: 1.1.3 → 2.0.0 (breaking changes)
6. Click **Run workflow**

The workflow will:
- Automatically bump version in `package.json`
- Commit and push the version change
- Create and push git tag
- Create GitHub Release (as draft)
- Build installers for Windows, macOS, and Linux
- Upload installers as artifacts

7. Go to **Releases** section
8. Find the draft release
9. Review and click **Publish release**
10. Download the installer artifacts from the workflow run

### Manual Release Process

If you prefer manual releases:

1. Bump version in `package.json`
2. Create a git tag: `git tag v1.1.4`
3. Push tag: `git push origin v1.1.4`
4. Build with publish: `npm run build:win -- -p always` (or other platforms)
5. Upload generated files to GitHub Release (or let electron-builder do it with GH_TOKEN)

### User Data Preservation

The auto-updater preserves:
- Encrypted login credentials (`accounts.enc`)
- User settings and preferences
- Error logs
- All data in `app.getPath('userData')`
