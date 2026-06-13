# Installation Outline

This is a high-risk rooted Pixel stack. Treat this as an outline, not a generic beginner one-click guide.

## Preconditions

- Bootloader unlocked
- matching stock boot images available for rollback
- APatch root already understood and working
- ADB/fastboot access available
- recovery plan for disabling modules if SystemUI or launcher crashes
- current full OTA or factory image for the device build

## Recommended Order

1. Establish root baseline with APatch.
2. Install Zygisk Next.
3. Install Vector.
4. Reboot and confirm hook framework is alive.
5. Install QuickSwitch fork.
6. Install Lawnchair.
7. Configure QuickSwitch/Quickstep provider as needed for the device.
8. Make Lawnchair the HOME app.
9. Install patched PixelXpert and assign scopes.
10. Install patched Iconify FOSS and assign scopes.
11. Enable compatibility mode in the patched apps before turning on overlapping UI tweaks.
12. Reboot once and verify SystemUI, HOME, gestures, recents, and lockscreen.

## Expected Scopes

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

## Recovery Notes

If SystemUI or launcher breaks after enabling modules:

- boot into a state where ADB works
- disable the newest module first
- if needed, disable Iconify and PixelXpert together and re-enable one at a time
- keep QuickSwitch/Lawnchair changes separate from SystemUI hook changes while debugging

If Android refuses to install an APK:

- check package name
- check signing certificate
- check versionCode monotonicity
- check whether the existing package is FOSS vs stock package id

## OTA Notes

For A/B OTA updates on rooted Pixels:

- do not press the updater restart button until the inactive slot boot image has been patched appropriately
- confirm active/inactive slot before flashing
- after bootloader anti-rollback increments, bring both slots forward before treating the phone as settled

