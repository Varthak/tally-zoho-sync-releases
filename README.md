# Tally Zoho Sync — releases

Public download and update feed for the **Tally Zoho Sync** desktop app (Varthak). This repository holds
**no source code**; the app's source lives in a private repository. Every release here is created
by that repository's CI, never by hand.

## Channels

| Channel | Tag | GitHub release type | Who it is for |
|---|---|---|---|
| Production | `vX.Y.Z` | Latest | Customers |
| UAT | `vX.Y.Z-uat.N` | Pre-release | Internal QA and acceptance testing |
| Development | `vX.Y.Z-dev.N` | Pre-release | Developers |

Each installed app follows only its own channel: a UAT build never offers a Development or Production
release, and the reverse.

## Assets in every release

| File | Purpose |
|---|---|
| `TallyZohoSync-Setup-<version>.exe` | Windows installer (per-user, no admin rights needed) |
| `SHA256SUMS.txt` | SHA-256 of every installer in the release |
| `*.sig` | Ed25519 signature the app verifies before installing an update |
| `update-<channel>.json` | Update manifest the app reads: version, notes, download URL, checksum, signature |

## Verifying a download by hand

```powershell
Get-FileHash .\TallyZohoSync-Setup-<version>.exe -Algorithm SHA256
```

Compare the hash with the matching line in `SHA256SUMS.txt`.

Installers are not yet Authenticode-signed, so Windows SmartScreen may warn on first install. Updates
are still verified by the app with the release signing key before they run.
