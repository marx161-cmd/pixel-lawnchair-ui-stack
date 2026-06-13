# Pixel Lawnchair UI Stack

This is a staged integration package for running a Lawnchair-based Pixel UI stack with APatch root, Zygisk, Vector/LSPosed-compatible hooks, patched Iconify FOSS, and patched PixelXpert.

The goal is not to provide a one-click root package. The goal is to document a known-good shape and keep the patch surface reproducible so other people can build, inspect, and adapt it.

Status on 2026-06-13:

- Device used for validation: Pixel 10 Pro (`blazer`)
- Android baseline used for live checks: Android 16, `CP1A.260405.005`, security patch `2026-04-05`
- May 2026 OTA was staged but not active on the test device during this documentation pass
- No install, reboot, OTA activation, or module mutation was performed while creating this package

## What This Stack Does

- Uses Lawnchair as HOME while keeping Pixel Launcher/Quickstep plumbing available through QuickSwitch.
- Lets Iconify target Lawnchair with a dynamic overlay component.
- Lets PixelXpert and Iconify coexist by hiding overlapping controls behind a compatibility mode.
- Uses Vector as the LSPosed-compatible hook engine on top of Zygisk Next and APatch.
- Keeps the Device Owner / policy automation layer documented as related infrastructure, but not a hard dependency for the UI hooks.

## Contents

- `artifacts/`
  - locally built APKs that are intentionally staged for testing or release
- `patches/`
  - patch exports to carry onto upstream source trees
- `docs/`
  - build, install, compatibility, and module notes
  - Device Owner / policy-layer notes
  - publishing checklist
- `licenses/`
  - upstream license texts for included source patch targets

## Current Artifact

Public APKs staged here:

- `artifacts/Iconify-v8.0.0-foss-lawnchair-pxcompat-release.apk`
- `artifacts/PixelXpert-canary-489-lawnchair-iconify-compat-release.apk`

Iconify is:

- package: `com.drdisagree.iconify.foss`
- version: `8.0.0`
- versionCode: `26`
- signer: Android Debug certificate matching the currently installed local Iconify FOSS test build

PixelXpert is:

- package: `sh.siava.pixelxpert`
- version: `canary-489`
- versionCode: `489`
- signer: Android Debug certificate matching the local patched test stack

Do not assume that debug signing is appropriate for a public release. For a real release, publish source and reproducible build instructions first, or sign with a deliberate project key and document upgrade implications.

Iconify and PixelXpert are GPLv3 projects in the checked local source trees. Publishing patches/forks is allowed. Publishing APKs is also allowed if the corresponding source, patches, build instructions, and license notices are provided.

## Source Branches

- Iconify fork branch: `https://github.com/marx161-cmd/Iconify/tree/codex/iconify-v8-lawnchair-port`
- PixelXpert fork branch: `https://github.com/marx161-cmd/PixelXpert/tree/codex/pixelxpert-iconify-compat`

These branches are best-effort integration branches. They are not upstream releases and are not promised to track future Android, Iconify, PixelXpert, or Pixel SystemUI changes automatically.

## Dependency Summary

Core UI path:

- APatch
- Zygisk Next
- Vector
- QuickSwitch fork
- Lawnchair
- patched Iconify FOSS
- patched PixelXpert

Useful but not core to the UI patch:

- Yet Another Bootloop Protector
- Device Owner / policy automation stack: Dhizuku and OwnDroid
- systemless hosts
- other user-specific LSPosed modules

See `docs/MODULES.md` for the pinned versions from the validated device.
See `docs/DEVICE_OWNER_POLICY.md` for the Dhizuku / OwnDroid policy layer.

## Publishing Recommendation

Publish this as an integration guide plus patches, not as a bundled root image or module pile.

Recommended public release shape:

- a Git branch or fork for the Iconify FOSS patch
- a Git branch or fork for the PixelXpert compatibility patch
- optional APK artifacts with clear signing notes
- a compatibility matrix
- a module/version manifest with upstream links and hashes
- a recovery section explaining how to disable modules if SystemUI or launcher hooks break
- a clear warning that this integration branch is best-effort and not continuously maintained upstream

Avoid redistributing third-party root/module zips until each project license and preferred distribution method is checked.

Do not publish raw phone snapshots, package dumps, app data, Vector databases, logs, or private device inventory. Keep public docs to the sanitized component matrix and reproducible commands.

See `docs/PUBLISHING.md` for the remaining release checklist.
