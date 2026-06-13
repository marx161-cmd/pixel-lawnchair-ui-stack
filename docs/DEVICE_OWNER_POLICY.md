# Device Owner And Policy Layer

Snapshot date: 2026-06-13.

The UI tweak stack is separate from the Device Owner stack, but the phone's actual operating setup uses both.

## Intended Layering

- Dhizuku holds the active Device Owner receiver.
- OwnDroid provides the practical automation/policy management interface.
- Tasker and related automation can call into this layer for policy actions, presentation mode, kiosk entry/exit, or input-mode restoration.

## Observed Live State

Active Device Owner:

- package: `com.rosan.dhizuku`
- admin: `com.rosan.dhizuku/.server.DhizukuDAReceiver`
- version: `2.11.2`, versionCode `18`
- organization-owned device flag: true

OwnDroid:

- package: `com.bintianqi.owndroid`
- version: `8.1`, versionCode `44`
- installer observed: `com.looker.droidify`

## Relationship To The UI Stack

The Lawnchair/Iconify/PixelXpert patches do not currently require Device Owner privileges. Keep the policy layer documented as an adjacent capability stack, not as a mandatory dependency for basic UI hooks.

Use this layer for:

- kiosk / lock-task behavior
- status-bar and keyguard policy controls
- policy-managed app restrictions
- privileged automation where Device Owner is cleaner than root

Do not mix this layer into the root/module install order unless a specific policy action is required.
