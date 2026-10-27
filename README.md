# Plato POS releases

Public Windows installers and update metadata for Plato POS. Application source code is maintained separately.

## Install Plato POS

Download the full `.exe` installer from the [stable Windows release](https://github.com/Mantaray-Digital/plato-pos-releases/releases/tag/unsigned).
Run the installer, pair the computer using its dashboard POS device code, then sign in with a staff PIN. Choose **Set up printers** from the welcome tip, or **Later** to continue to POS. Printer setup remains available in **Settings → Printers**.

The first customer release is **0.4.0**, without a candidate version suffix. It uses the normal Plato POS installation and data profile.

Once installed, use **Settings → General → Check for updates → Download update → Restart and update**. Downloads and restarts require operator action. Normal Quit does not install updates.

When KDS is disabled in the dashboard, new offline orders offer **Cash** only. A configured cash payment method and an open cash shift are required. Disconnected registers use the last synced dashboard value; there is no separate local KDS toggle. Existing saved unpaid orders and dashboard printer names are preserved.

This release is unsigned; Windows may show an unknown-publisher prompt.

## RC update-flow testing

The separate [RC test feed](https://github.com/Mantaray-Digital/plato-pos-releases/releases/tag/unsigned-candidate) advertises **rc.4** to existing **rc.3** test installations through Check for updates. It contains the same setup tip and KDS payment rule. The tip appears after new pairing and staff sign-in, rather than after every launch. Customer installations use the stable release above; the RC test profile stays separate.

## Update channels

Each channel has a permanent release tag. Do not rename or delete these tags.

| Build | Release tag | Metadata asset |
|---|---|---|
| Customer Windows release | `unsigned` | `unsigned.yml` |
| RC update-flow test build | `unsigned-candidate` | `unsigned-candidate.yml` |
| Signed candidate build | `candidate` | `candidate.yml` |
| Signed stable build | `stable` | `latest.yml` |

Only channels with a published build have a release. Signed and unsigned channels are separate; version checks never move installations between candidate and stable.

## Publishing another update

1. Build a strictly newer application version with English and Arabic notes. Run the desktop checks and stage its verified installer, blockmap and metadata using the source repository's release scripts.
2. Upload the versioned installer and blockmap to the matching channel release first. Never replace an existing installer's bytes or remove older installers/blockmaps.
3. Verify their uploaded sizes and hashes, then upload that channel's metadata last. Use `gh release upload <channel> <manifest> --clobber --repo Mantaray-Digital/plato-pos-releases` only for the metadata asset.
4. Run the source repository's `release:verify-feed` command and verify a real installed previous version can check, download and upgrade without losing saved work or duplicating synchronized orders.

Protect repository write access: the unsigned channel verifies download hashes but cannot establish the installer's publisher identity independently of this repository.
