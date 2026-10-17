# Licensing and tamper resistance

Sidekick is free, so the licence protects a badge and the beta channel, not the app. The measures below are the
standard for desktop software; nothing that runs on a user's Mac is uncrackable, and the only truly protected value
is what a server decides (the licence server's tokens, and paid services like Sync later).

| Measure | Where | Status |
|---|---|---|
| Owner unlock signed with an Ed25519 private key that never ships; device-bound | `backend/hud/license.py`, `hud owner-token` | on |
| Supporter and account tokens signed by the account service, device-bound, 14-day expiry renewed daily; keys minted and revoked by Polar; accounts in Firebase Auth (Google, email link), never a password | `server/account-service` (Cloud Run, Firestore) + `[license] token_url` | live |
| Sign-in claimed with a one-time verifier the browser never sees (device flow with PKCE); refresh secrets stored only as hashes, bound to one Mac | `server/account-service/app.js`, `license.py` `start_signin` | live |
| After the claim the app asks "Signed in as <email>. Is that you?" and stores the session only on Yes (someone holding the sign-in link could finish it with their own account) | `license.py` `confirm_signin`, Settings › Supporter | on |
| Webhooks and keys fail closed until Polar's ids and webhook secret are set; per-address rate limits on sign-in, keys and the supporter lookup | `server/account-service/app.js` | written, tested; live after the next deploy |
| Local cache HMAC-signed (tamper-evident) | `license.json` | on |
| Licence module compiled to native code, not bytecode | `scripts/bundle-backend.sh` (Cython → arm64 .so) | on |
| Electron fuses: no ELECTRON_RUN_AS_NODE, no NODE_OPTIONS, no --inspect, ASAR integrity, app only from ASAR | `hud/package.json` `build.electronFuses` | on |
| Developer ID signing + notarization + hardened runtime | `scripts/notarize.cjs`, `make release` with `CSC_*`/`APPLE_*` | needs the Apple account |

## The signing key

`~/.sidekick/license-signing-key.pem` (and `.pkcs8.b64` for the account service). Back it up in a password manager.
`hud license-keygen --force` rotates it: put the printed public key in `license.py` `PUBLIC_KEY_B64`, replace the
`SIGNING_KEY` secret in Secret Manager and redeploy the account service, and run `hud owner-token` again on your Mac.

## Stable permissions across local builds

Ad-hoc signed builds get a new code signature every time, so macOS forgets microphone and calendar access after each
reinstall. Developer ID signing fixes it for customers. On your own Mac, a self-signed code-signing certificate does
the same: Keychain Access › Certificate Assistant › Create a Certificate…, name "Sidekick Local", type Code Signing.
Then build with `make release CSC_NAME="Sidekick Local"`.

Either way the app watches for it: `hud.system` re-reads the microphone and calendar status (status flags only, never a
prompt) at startup, every 10 minutes while idle and before listening, and shows "Sidekick lost … access" when a
permission it had is gone (docs/PROTOCOL.md › v15).
