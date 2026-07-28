# Release Pipeline

## Overview

This project uses GitHub Actions for automated releases. The pipeline handles version bumping, tagging, release creation, and building installers for all platforms.

## How to Create a Release

### Using GitHub Actions (Recommended)

1. Go to the **Actions** tab in your GitHub repository
2. Select the **Release** workflow
3. Click **Run workflow**
4. Choose the branch (usually `main`)
5. Select the version type:
   - **patch**: 1.1.3 → 1.1.4 (bug fixes, small changes)
   - **minor**: 1.1.3 → 1.2.0 (new features, additions)
   - **major**: 1.1.3 → 2.0.0 (breaking changes, major rework)
6. Click **Run workflow**

### What the Pipeline Does

The automated pipeline will:

1. **Bump version**: Automatically increments the version in `package.json`
2. **Commit change**: Commits and pushes the version change to `main`
3. **Create tag**: Creates and pushes a git tag (e.g., `v1.1.4`)
4. **Create release**: Creates a GitHub Release as a draft
5. **Build installers**: Builds installers for Windows, macOS, and Linux
6. **Upload artifacts**: Uploads the installers as workflow artifacts

### Publishing the Release

After the workflow completes:

1. Go to the **Releases** section in your repository
2. Find the draft release (it will be marked as "Draft")
3. Review the release notes and version
4. Click **Publish release**
5. Download the installer artifacts from the workflow run page

### Downloading Installers

The installers are available as artifacts in the workflow run:

- **windows-installer**: Contains `.exe` files for Windows
- **macos-installer**: Contains `.dmg` files for macOS
- **linux-installer**: Contains `.AppImage` files for Linux

You can download these from the workflow run page under "Artifacts".

## Manual Release Process

If you prefer to create releases manually:

1. Edit `package.json` and bump the version
2. Commit the change: `git commit -am "chore: bump version to X.Y.Z"`
3. Create a tag: `git tag vX.Y.Z`
4. Push the tag: `git push origin vX.Y.Z`
5. Build installers locally:
   ```bash
   npm run build:win    # Windows
   npm run build:mac    # macOS
   npm run build:linux  # Linux
   ```
6. Go to GitHub Releases and create a new release
7. Upload the installer files from the `dist/` folder

## Version Guidelines

- **Patch (X.Y.Z)**: Bug fixes, small improvements, documentation updates
- **Minor (X.Y.0)**: New features, additions, non-breaking changes
- **Major (X.0.0)**: Breaking changes, major rework, significant changes

## Notes

- The pipeline creates releases as **drafts** - you must manually publish them
- Installers are kept as artifacts for 30 days
- The auto-updater in the app will check for new releases from your repository
- Make sure to test the installers before publishing the release
