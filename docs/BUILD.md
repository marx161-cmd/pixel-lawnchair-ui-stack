# Build Notes

Snapshot date: 2026-06-13.

## Iconify FOSS v8 Port

Worktree:

- local Iconify checkout
- branch: `codex/iconify-v8-lawnchair-port`
- upstream: `https://github.com/Mahmud0808/Iconify.git`
- fork branch: `https://github.com/marx161-cmd/Iconify/tree/codex/iconify-v8-lawnchair-port`
- base commit: `42920a5d9907520546e116adf9787098f94c7cd4`

Patch:

- `patches/iconify-v8-foss-lawnchair-pxcompat.patch`

Build command:

```sh
ANDROID_HOME=/path/to/android-sdk ANDROID_SDK_ROOT=/path/to/android-sdk bash ./gradlew :app:assembleRelease
```

SDK note:

- point `ANDROID_HOME` and `ANDROID_SDK_ROOT` at the Android SDK directory that contains `platforms/` and `build-tools/`
- Gradle installed/used Android SDK Platform 37

Output:

- `artifacts/Iconify-v8.0.0-foss-lawnchair-pxcompat-release.apk`

Verification performed:

- APK package is `com.drdisagree.iconify.foss`
- versionName is `8.0.0`
- versionCode is `26`
- APK Signature Scheme v2 verifies
- signer matches installed local FOSS Iconify test build
- dex contains `com.drdisagree.iconify.xposed.InitHook`
- `InitHook` has a public zero-argument constructor
- `initZygote`, `handleLoadPackage`, and `handleInitPackageResources` exist
- source diff passed `git diff --check`

## PixelXpert Patch

Worktree:

- local PixelXpert checkout
- branch: `canary`
- fork branch: `https://github.com/marx161-cmd/PixelXpert/tree/codex/pixelxpert-iconify-compat`
- local HEAD during snapshot: `0a8b78d7de1e526f51d15cf57ac0b6375ce20b8c`
- upstream canary observed: `ec63a31b`

Patch:

- `patches/pixelxpert-current-canary-compat.patch`

Patch surface:

- compatibility preference helper changes
- quick settings preference screen gate
- status bar settings preference screen gate
- strings for the compatibility mode UI

Build command:

```sh
ANDROID_HOME=/path/to/android-sdk ANDROID_SDK_ROOT=/path/to/android-sdk bash ./gradlew app:assembleRelease
```

Local SDK notes:

- root `local.properties` may be needed with `sdk.dir=/path/to/android-sdk`
- `Submodules/RangeSliderPreference/local.properties` may also need the same SDK path if it contains a stale local path
- these `local.properties` changes are ignored/local build plumbing and are not part of the source patch
- `platforms;android-36` and `build-tools;36.1.0` were installed locally for this build

Output:

- `artifacts/PixelXpert-canary-489-lawnchair-iconify-compat-release.apk`

Verification performed:

- APK package is `sh.siava.pixelxpert`
- versionName is `canary-489`
- versionCode is `489`
- APK Signature Scheme v2 verifies
- signer is Android Debug certificate matching the local patched test stack
- SHA-256 is `3f78c9fc678d97f9b6c7d0a8c42087b47462fbd57aacfb85c0d8d09c8aa1a3c8`

## Lawnchair

Worktree:

- local Lawnchair checkout
- branch: `16-dev`
- local HEAD during snapshot: `892bff907ab7114571e506bcfb1ce67d3c732a67`
- upstream observed: `4ad961363c`

No local Lawnchair source patch was present. The stack depends on Lawnchair being installed and selected as HOME, plus QuickSwitch keeping Quickstep plumbing compatible.
