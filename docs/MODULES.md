# Root And Module Manifest

Snapshot date: 2026-06-13.

This manifest documents the validated stack. It is not a license grant and not a recommendation to redistribute every binary.

## Core Runtime

| Component | Observed version | Role | Publish guidance |
| --- | --- | --- | --- |
| APatch | `11142` | root framework and patched boot path | link upstream and document patching flow |
| Zygisk Next | `1.3.3/731` installed, `1.3.4/746` available | Zygisk implementation for APatch | link upstream; pin known-good version |
| Vector | `v2.0/3026` | LSPosed-compatible hook engine | link upstream/artifact; avoid downgrade to release JSON `3021` |
| QuickSwitch fork | `v4.0.4f`, versionCode `4040` | Quickstep provider plumbing for Lawnchair | link the fork used by this setup |
| Lawnchair | `16.0.0 (7361d44)` | HOME launcher | build/use current trusted upstream artifact |
| Iconify FOSS | staged `8.0.0` patch | UI overlay and SystemUI tweaks | publish source patch and optionally APK |
| PixelXpert | `canary-489` installed | SystemUI/Pixel feature hooks | publish source patch after rebuilding current canary |

## Protective Or Related Modules

| Component | Observed version | Role | Core requirement |
| --- | --- | --- | --- |
| Yet Another Bootloop Protector | `8.138` | bootloop/SystemUI monitor | recommended, not core |
| systemless hosts | `v1.2.2` | hosts file support | not core |
| `fedora43failsafe` | `v1` | local cleanup helper | exclude from public UI stack |
| Shamiko | no module metadata found | root hiding | not core to UI patch |

## Device Owner / Policy Layer

This phone uses a broader Device Owner and policy automation stack:

- Dhizuku
- OwnDroid

Observed live state:

- package: `com.rosan.dhizuku`
- version: `2.11.2`
- admin: `com.rosan.dhizuku/.server.DhizukuDAReceiver`
- organization-owned device flag: true
- OwnDroid package: `com.bintianqi.owndroid`
- OwnDroid version: `8.1`, versionCode `44`

Interpretation:

- Dhizuku is the active Device Owner receiver.
- OwnDroid is the user-facing automation/policy manager layer.
- The Lawnchair/Iconify/PixelXpert UI hooks should still be documented so they can run without making Device Owner a hard dependency.

## Do Not Publish Blindly

Do not bundle these without a license and redistribution audit:

- APatch APKs
- Zygisk Next module zips
- Vector module zips
- QuickSwitch fork zips
- YABP zips
- any module copied directly from `/data/adb/modules`

For a public release, prefer upstream links, exact version pins, hashes, and local reproduction instructions.
