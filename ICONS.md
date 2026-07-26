# Custom Icons

The current `tray.png` is too small for electron-builder (minimum 256x256 required). To add custom icons for the installers:

## Windows

Create a `build/` directory and add `icon.ico` (minimum 256x256):
```bash
mkdir build
# Convert tray.png to icon.ico with 256x256 size
# You can use online tools like https://convertico.com/
```

Then update `package.json`:
```json
"win": {
  "icon": "build/icon.ico",
  ...
}
```

## macOS

Create `build/icon.icns`:
```bash
# Use iconutil or online converters to create .icns file
# Minimum 512x512 recommended
```

Update `package.json`:
```json
"mac": {
  "icon": "build/icon.icns",
  ...
}
```

## Linux

Create `build/icons/` directory with various PNG sizes:
```bash
mkdir -p build/icons
# Create icons in these sizes:
# - 16x16, 24x24, 32x32, 48x48, 64x64, 128x128, 256x256, 512x512
```

Update `package.json`:
```json
"linux": {
  "icon": "build/icons",
  ...
}
```

## Quick Fix (Temporary)

For now, the build uses the default Electron icon. This is functional but not branded.
