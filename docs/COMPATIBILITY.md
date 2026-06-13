# Compatibility Matrix

Snapshot date: 2026-06-13.

## Validated Device State

- Device: Pixel 10 Pro
- Device codename: `blazer`
- Android: 16
- Build fingerprint: `google/blazer/blazer:16/CP1A.260405.005/15001963:user/release-keys`
- Security patch: `2026-04-05`
- Active slot during checks: `_a`
- Boot state: unlocked / orange
- Gesture navigation mode: `2`

May 2026 OTA state during checks:

- May OTA was staged for inactive slot `_b`
- Booted system was still April 2026
- Treat the updater restart button as an OTA activation action, not a normal reboot

## Installed UI Apps On Validated Device

| Component | Package | Version | Version code |
| --- | --- | --- | --- |
| Lawnchair | `app.lawnchair` | `16.0.0 (7361d44)` | `16000000` |
| Iconify FOSS | `com.drdisagree.iconify.foss` | `7.2.0` | `24` |
| PixelXpert | `sh.siava.pixelxpert` | `canary-489` | `489` |
| APatch app | `me.bmax.apatch` | `166daa0` | `11142` |
| Dhizuku | `com.rosan.dhizuku` | `2.11.2` | `18` |
| OwnDroid | `com.bintianqi.owndroid` | `8.1` | `44` |

## Staged Updates

| Component | Staged version | Notes |
| --- | --- | --- |
| Iconify FOSS | `8.0.0`, versionCode `26` | Built locally with Lawnchair target and PixelXpert compatibility mode |
| PixelXpert | `canary-489`, versionCode `489` | Built locally with Iconify compatibility mode |
| Lawnchair | not staged | Local source has no custom patch; update path is current upstream build/artifact |
| Zygisk Next | `1.3.4/746` available | Device currently has `1.3.3/731` |
| Vector | keep `v2.0/3026` | Public release metadata advertises older `3021`; do not downgrade blindly |

## Expected Scope Configuration

Vector/LSPosed scopes observed on the validated device:

Iconify FOSS:

- `app.lawnchair`
- `com.android.systemui`
- `com.drdisagree.iconify.foss`
- `system`

PixelXpert:

- `android`
- `app.lawnchair`
- `com.android.settings`
- `com.android.systemui`
- `com.google.android.apps.nexuslauncher`
- `com.google.android.dialer`

## Compatibility Notes

- The patched Iconify APK is signed with the same Android Debug certificate as the currently installed local test APK, so it should upgrade in place on this specific test setup.
- The patched PixelXpert APK is signed with the same Android Debug certificate as the local patched stack and has the same SHA-256 as the documented installed `canary-489` APK.
- If a user has a differently signed Iconify FOSS package, Android will reject an in-place update. They must rebuild/sign consistently or deliberately uninstall/reinstall and restore scopes/settings.
- The current Iconify v8 patch was verified to preserve the Xposed `InitHook` class, public zero-arg constructor, and hook lifecycle methods.
- PixelXpert and Iconify both touch SystemUI. The compatibility switches intentionally hide overlapping controls rather than trying to merge two independent hook implementations.
- The broader policy layer uses Dhizuku as active Device Owner and OwnDroid for automation/policy handling.
- This is not yet validated on the active May or June 2026 Pixel build.
