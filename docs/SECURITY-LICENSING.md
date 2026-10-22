# Licensing and tamper resistance

Sidekick is free, so the licence protects a badge and the beta channel, not the app. Nothing that runs on a Mac is
uncrackable; the only value that is truly protected is what a server decides. These are the measures in place.

| Measure | Status |
|---|---|
| Owner unlock is signed with a private key that never ships, and is tied to one Mac | on |
| Supporter tokens are signed by our supporter service, tied to one Mac, expire after 14 days and renew daily | live |
| Supporter keys are issued and revoked by our payment provider; there are no online accounts or passwords on our server | live |
| Payment webhooks and keys refuse requests until fully configured; keys, feedback and supporter lookups are rate-limited | live |
| The local licence cache is signed, so edits are detected | on |
| The licence code is compiled to native code | on |
| The app is hardened against debugging and code injection (Electron fuses, ASAR integrity) | on |
| Developer ID signing, notarization and hardened runtime | needs the Apple account |

## Permissions after a reinstall

macOS forgets microphone and calendar access when an app's signature changes, which can happen when you reinstall a
build that isn't signed with a Developer ID. Sidekick notices: it checks at startup, every 10 minutes while idle and
before you listen, and shows "Sidekick lost … access" with an "Allow again" button. It never asks macOS on its own.
