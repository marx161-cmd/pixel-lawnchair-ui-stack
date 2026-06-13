# Publishing Checklist

Snapshot date: 2026-06-13.

## Ready To Publish As-Is

- High-level README.
- Compatibility matrix.
- Root/module manifest.
- Device Owner / policy-layer notes.
- Installation outline.
- Iconify FOSS v8 patch export.
- PixelXpert compatibility patch export.
- Patched Iconify FOSS APK artifact.
- Patched PixelXpert APK artifact.
- Upstream license texts for Iconify, PixelXpert, and Lawnchair.
- Plain `SHA256SUMS.txt` for staged files.

## Publish With Caution

Iconify APK:

- `artifacts/Iconify-v8.0.0-foss-lawnchair-pxcompat-release.apk`
- debug-signed
- upgrade-compatible with the local test phone because the currently installed local Iconify FOSS build uses the same signer
- for public release, prefer source-first publishing or sign with a deliberate release key and document that it will not upgrade over differently signed builds

PixelXpert APK:

- `artifacts/PixelXpert-canary-489-lawnchair-iconify-compat-release.apk`
- debug-signed
- same package/versionCode/versionName as the installed local patched stack
- for public release, prefer source-first publishing or sign with a deliberate release key and document that it will not upgrade over differently signed builds

## Still Needed Before A Proper Public Release

- Test the newly staged Iconify and PixelXpert artifacts together after the next controlled phone update window:
  - package install/upgrade behavior
  - Vector scopes
  - SystemUI hook startup logs
  - Lawnchair gestures and recents
- Decide Lawnchair source/artifact baseline:
  - current upstream `16-dev`
  - known GitHub Actions artifact
  - or the currently installed `16.0.0 (7361d44)`
- Document the Dhizuku / OwnDroid split clearly:
  - Dhizuku is Device Owner
  - OwnDroid handles automation/policy management
  - neither is required for the basic Lawnchair/Iconify/PixelXpert hook path
- Audit redistribution terms before bundling third-party binaries:
  - APatch
  - Zygisk Next
  - Vector
  - QuickSwitch fork
  - YABP
  - OwnDroid
- Add upstream links for every dependency.
- Add a recovery section with exact module-disable commands once tested on the target build.
- Validate on the active May or June 2026 Pixel build before claiming current-version compatibility.

## Recommended Repo Shape

```text
README.md
docs/
patches/
artifacts/
licenses/
SHA256SUMS.txt
```

Do not publish raw phone snapshots, package dumps, app data, Vector databases, logs, or private device inventory. Keep public docs to sanitized component names, versions, hashes, and reproducible commands.

## Source Branches

- Iconify: `https://github.com/marx161-cmd/Iconify/tree/codex/iconify-v8-lawnchair-port`
- PixelXpert: `https://github.com/marx161-cmd/PixelXpert/tree/codex/pixelxpert-iconify-compat`

The integration repo should link to these branches as the corresponding source for staged APKs.
